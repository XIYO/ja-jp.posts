---
title: Oracle Docker Installation Guide
tags:
  - docker
  - oracle
  - database
  - guide
  - installation
---

# Oracle Docker クイックインストールガイド

このガイドでは、Dockerを使用してOracle Database Free Editionを迅速にインストールする方法を説明します。

> [!INFO]
> Oracle Databaseの概念とエディションの詳細については、[Oracle Database概念ガイド](oracle-database-concepts)を参照してください。

## 前提条件

- Docker Desktopがインストール済み
- 最小2GBの空きRAM
- 最小15GBの空きディスク容量

## Oracle Database Free Editionのインストール

### Oracle Database 23c Freeイメージのダウンロード

> [!INFO]
> **Container Registryとは？**
> Dockerイメージを保存・配布するリポジトリです。Docker Hubが最も有名ですが、
> Oracleは独自のContainer Registry（container-registry.oracle.com）を運営しています。
> 
> ほとんどのContainer Registryはログイン後にイメージをダウンロードすることが原則です。
> しかし、OracleはFree Editionを「客寄せ商品」として活用し、ログインなしでもダウンロードできるようにしています。
> 
> Container Registryの詳細については、[Oracle Database概念ガイド](oracle-database-concepts)を参照してください。

開発者向けの最新無料版であるOracle Database 23c Freeをダウンロードします。

ターミナルを開き、以下のコマンドをコピーして貼り付けてください：
```bash
docker pull container-registry.oracle.com/database/free:latest
```
## Oracle Freeコンテナの実行

### 基本的な実行

Oracle Free 23cコンテナを実行します。

ターミナルを開き、以下のコマンドをコピーして貼り付けてください：
```bash
docker run -d --name oracle-free -p 1521:1521 -p 5500:5500 -e ORACLE_PWD=oracle123 container-registry.oracle.com/database/free:latest
```

上記コマンドの各オプションの説明：

**基本実行オプション：**
- `-d`: バックグラウンドで実行
- `--name oracle-free`: コンテナ名を指定
- `-p 1521:1521`: データベースポートのマッピング
- `-p 5500:5500`: Enterprise Manager Expressポートのマッピング

**必須環境変数：**
- `-e ORACLE_PWD=oracle123`: SYS、SYSTEM、PDBAdminユーザーのパスワード設定

**オプション環境変数（必要に応じて追加）：**
- `-e ORACLE_CHARACTERSET=KO16MSWIN949`: 文字セットを変更（デフォルト：AL32UTF8）
- `-e ORACLE_PDB=MYAPP`: PDB名を変更（デフォルト：FREEPDB1）
- `-e ENABLE_ARCHIVELOG=true`: アーカイブログモードを有効化
- `-v oracle-free-data:/opt/oracle/oradata`: データを永続的に保存

> [!INFO]
> **接続情報**
> - **ポート**: 1521（データベース）、5500（Web管理ツール）
> - **デフォルトユーザー**: SYS、SYSTEM（パスワードは上記で設定したoracle123）
> - **データベース名**: FREEPDB1
> 
> 接続文字列の例: `username/password@localhost:1521/FREEPDB1`
> 
> SID、Service Name、PDBなどのOracleの核心概念については、[Oracle Database概念ガイド](oracle-database-concepts)を参照してください。



## コンテナ状態の確認

### ログの確認

oracle-freeコンテナのログをリアルタイムで確認します。

ターミナルを開き、以下のコマンドをコピーして貼り付けてください：
```bash
docker logs -f oracle-free
```

データベースの準備が完了すると、次のメッセージが表示されます：
```
DATABASE IS READY TO USE!
```

### コンテナ状態の確認

ターミナルを開き、以下のコマンドをコピーして貼り付けてください：
```bash
docker ps -a | grep oracle
```

### データベース状態の確認

コンテナが正常に実行されているか確認します。

ターミナルを開き、以下のコマンドをコピーして貼り付けてください：
```bash
docker ps | grep oracle-free
```


## トラブルシューティング

### ポート競合

ポート競合が発生した場合、まず1521ポートを使用しているプロセスを確認します。

ターミナルを開き、以下のコマンドをコピーして貼り付けてください：
```bash
lsof -i :1521
```

**出力例：**

ポートが使用されていない場合（正常）：
```
# 結果なし（空の画面）
```

ポートがすでに使用中の場合：
```
COMMAND   PID      USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
com.docke 642 username  190u  IPv6 0x651391288870c513      0t0  TCP *:ncube-lm (LISTEN)
```

Dockerコンテナ実行時のポート競合エラー：
```
docker: Error response from daemon: failed to set up container networking: 
Bind for 0.0.0.0:1521 failed: port is already allocated
```

ポート競合を解決する2つの方法：

#### 既存コンテナの停止で問題を解決

既存のOracleコンテナを停止して新しく開始します。

ターミナルを開き、以下のコマンドをコピーして貼り付けてください：
```bash
docker stop oracle-free
```

#### 別のポートで問題を解決

複数のOracleを同時に実行するには、別のポートを使用します。

ターミナルを開き、以下のコマンドをコピーして貼り付けてください：
```bash
docker run -d --name oracle-free2 -p 1522:1521 -p 5501:5500 -e ORACLE_PWD=YourPassword123 container-registry.oracle.com/database/free:latest
```