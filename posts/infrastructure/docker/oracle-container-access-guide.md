---
title: Oracle Container Access Guide
tags:
  - docker
  - oracle
  - database
  - guide
  - connection
  - troubleshooting
---

# Oracleコンテナ接続ガイド

## IntelliJ Ultimate DataGrip接続設定

### DataGripでOracleに接続

1. DataGripを実行して新しいデータソースを追加（+）
2. Oracleを選択
3. 次の設定値を入力：

**基本設定：**
- Host: `localhost`
- Port: `1521`
- SID: `FREE`
- User: `system`
- Password: `oracle123`

**Service Name使用時：**
- Connection type: `Service name`
- Service name: `FREEPDB1`

**詳細設定：**
- Driver: Oracle JDBCドライバー自動ダウンロード
- URL: `jdbc:oracle:thin:@localhost:1521/FREEPDB1`

4. 「Test Connection」をクリックして接続を確認
5. 「OK」をクリックして保存

## トラブルシューティング

### Connection refused / IO Error

**症状：** DataGripでOracleエラー（ORA-）ではなく、接続自体が失敗する場合

**発生原因：** DockerやコンテナーのためOracleサーバーにアクセスできない状態

**解決方法：**

1. Docker Desktopが実行中か確認：
```bash
docker version
```
Dockerが実行されていない場合は、Docker Desktopを起動してください。

2. Oracleコンテナーの状態を確認：
```bash
docker ps -a | grep oracle-free
```

3. コンテナーの状態別の対処：
   - **コンテナーがない場合**：新規作成（下記「コンテナーがないか停止している場合」参照）
   - **STATUS: Exited**：`docker start oracle-free`を実行して5分待機
   - **STATUS: Up**：ポートマッピングを確認

4. ポートマッピングの確認：
```bash
docker port oracle-free
```
出力が`1521/tcp -> 0.0.0.0:1521`でない場合は、コンテナーを再作成してください。

### Network adapter could not establish the connection

**症状：** DataGripでネットワーク接続を試みるが失敗

**発生原因：** ファイアウォール、誤ったホスト/ポート設定、またはOracleリスナー未作動

**解決方法：**

1. localhost代わりに127.0.0.1を使用：
   - Host: `127.0.0.1`（localhost代わり）
   - Port: `1521`

2. Oracleリスナー状態確認：
```bash
docker exec oracle-free lsnrctl status
```
リスナーが作動していない場合は、上記「ORA-12541」解決方法を参照

3. 別のポート使用時の設定確認：
```bash
docker ps | grep oracle-free
```
PORTS列で実際のポートマッピングを確認（例：1522->1521）

### ORA-01017: invalid username/password（ユーザー名/パスワードが正しくない）

**発生原因：** 入力したパスワードが実際のデータベースに設定されたパスワードと異なる場合に発生します。

**解決方法：** パスワードを覚えていない場合は、以下のコマンドで再設定してください：

SYSTEMとSYSアカウントのパスワード再設定：
```bash
docker exec -it oracle-free sqlplus / as sysdba -c "ALTER USER system IDENTIFIED BY oracle123; ALTER USER sys IDENTIFIED BY oracle123;"
```

特定のユーザーアカウントのパスワード再設定方法：

形式：`ALTER USER ユーザー名 IDENTIFIED BY 新パスワード;`

例1 - myappユーザーのパスワードをmyapp123に変更：
```bash
docker exec -it oracle-free sqlplus / as sysdba -c "ALTER USER myapp IDENTIFIED BY myapp123;"
```

例2 - scottユーザーのパスワードをtigerに変更：
```bash
docker exec -it oracle-free sqlplus / as sysdba -c "ALTER USER scott IDENTIFIED BY tiger;"
```

### ORA-12541: TNS:no listener（リスナーが応答しない）

**発生原因：** Oracleリスナーサービスが停止したか応答しない場合に発生します。

**解決方法：** リスナーを再起動してください：

```bash
docker exec -it oracle-free bash -c "lsnrctl stop && lsnrctl start"
```

### コンテナーがないか停止している場合

**発生原因：** Dockerコンテナーが存在しないか停止している状態です。

**解決方法：** まずコンテナーの状態を確認して適切な措置を取ってください：

コンテナー状態確認：
```bash
docker ps -a | grep oracle-free
```

コンテナーが停止している場合（STATUS: Exited）：
```bash
docker start oracle-free
```

コンテナーがない場合は新規作成：
```bash
docker run -d --name oracle-free -p 1521:1521 -p 5500:5500 -e ORACLE_PWD=oracle123 container-registry.oracle.com/database/free:latest
```

### コンテナー再起動後の接続不可

**発生原因：** Oracleコンテナーが再起動されると、データベースが自動的に起動しない場合があります。

**解決方法：** データベースが準備完了するまで待機するか、手動で起動してください：

ログ確認（準備完了メッセージ確認）：
```bash
docker logs oracle-free | grep "DATABASE IS READY"
```

手動でデータベース起動：
```bash
docker exec -it oracle-free bash -c "echo 'STARTUP;' | sqlplus / as sysdba"
```