---
authors:
  - XIYO
  - XIYO
  - XIYO
  - XIYO
  - XIYO
dates:
  - '2025-03-09T22:09+0900'
  - '2025-03-09T22:02+0900'
  - '2025-03-09T20:42+0900'
  - '2025-02-16T23:12+0900'
  - '2025-02-16T23:11+0900'
messages:
  - ':memo: Cloudflareトークン発行ページのリンク追加とスクリプト説明修正'
  - ':memo: ダブルスラッシュ構文追加'
  - ':memo: 意味が通るように変更'
  - ':art: ACME証明書発行ガイドの明確性向上：言語とフォーマットの改善'
  - ':art: ASUS AC88UルーターでのACME証明書発行自動化ガイドを追加'
title: ACME証明書発行の自動化（ASUS AC88Uルーター）
description: AC88UルーターにNginxをインストールしてSSL証明書を設定しましたが、毎回手動で証明書を発行する過程が整理されていなかったため、この機会に完全に整理した後記を残します。
---
# ACME証明書発行の自動化（ASUS AC88Uルーター）

AC88UルーターにNginxをインストールしてSSL証明書を設定しましたが、毎回手動で証明書を発行する過程が整理されていなかったため、この機会に完全に整理した後記を残します。

> [!NOTE]
> このプロセスはASUS Merlinファームウェアがインストールされたルーターでのみ可能です。

## 使用ドメイン

私は複数のサブドメインを使用しています。

- `xiyo.dev`
- `blog.xiyo.dev`
- `test.xiyo.dev`

このようにサブドメインが多い場合、ワイルドカード（`*.xiyo.dev`）を使用して一度に証明書を発行するのが効率的です。

## 事前知識

ワイルドカードドメインは**HTTP-01方式ではなくDNS-01方式**で認証する必要があります。
この方式はDNSプロバイダーがAPIをサポートしている場合のみ自動化可能です。

> 私は**Cloudflare**を使用しているため、DNS-01方式で証明書発行を自動化できました。  
> 国内ドメインサービスはサポートしていないんですよね...

### Cloudflare APIを使用したDNS認証

GitHub上の[ACMEリポジトリ](https://github.com/acmesh-official/acme.sh)の[`dns_cf`](https://github.com/acmesh-official/acme.sh/blob/master/dnsapi/dns_cf.sh)スクリプトを見ると、DNS-01方式を使用する際に必要な環境変数を確認できます。

```sh
#!/usr/bin/env sh
# shellcheck disable=SC2034
dns_cf_info='CloudFlare
Site: CloudFlare.com
Docs: github.com/acmesh-official/acme.sh/wiki/dnsapi#dns_cf
Options:
 CF_Key API Key
 CF_Email Your account email
 OptionsAlt:
 CF_Token API Token
 CF_Account_ID Account ID
 CF_Zone_ID Zone ID. Optional.
'
```

コードを見ると、2つの方式から1つを選択できます。

1. **Global API Key方式**（`CF_Key` + `CF_Email`使用）
2. **API Token方式**（`CF_Token` + `CF_Account_ID`使用）

- **Global API Key方式**は管理するドメインが多い時に便利で、1つのキーで複数のドメインの証明書を簡単に発行できます。
- **API Token方式**は特定のドメインにのみ権限を付与できるため、セキュリティがより優れています。

トークン発行は[Cloudflareトークン発行ページ](https://dash.cloudflare.com/profile/api-tokens)を参考にしてください。

> [!NOTE]
> 私は`xiyo.dev`以外にも他のドメインがあるため、**Global API Key方式**を使用しました。

---

## 証明書発行プロセス

### 1. SSHでルーターに接続

```sh data-title="terminal"
ssh admin@router-ip
```

### 2. Cloudflare DNSプラグインのダウンロード

AC88Uルーターは基本的にDNSプラグインを提供していないため、直接追加する必要があります。

```sh data-title="terminal"
wget -O /jffs/scripts/dnsapi/dns_cf "https://raw.githubusercontent.com/acmesh-official/acme.sh/master/dnsapi/dns_cf.sh"
```

> `wget`を使用して最新の`dns_cf.sh`スクリプトをダウンロードします。

### 3. Cloudflare APIキーの追加

`dns_cf`スクリプトの2行目に`CF_KEY`と`CF_EMAIL`を追加し、発行されたトークンを入力します。

```sh data-title="dns_cf"
#!/usr/bin/env sh

export CF_Key="my_key" # Added by XIYO // [!code focus]
export CF_Email="my_email" # Added by XIYO // [!code focus]

dns_cf_info=CloudFlare
Site: CloudFlare.com
# 以下省略...
```

> ホームサーバーであり、アクセスするのは私だけなので、スクリプトファイルにキーを追加しました。

### 4. サービス開始時の自動設定追加

ルーターが起動する際に自動的にDNSプラグインをマウントし、証明書更新作業を実行するよう設定する必要があります。

`/jffs/scripts/service-start`ファイルに以下の内容を追加します。

```sh data-title="service-start"
#!/bin/sh

/jffs/scripts/scmerlin startup &  # scMerlin 
ln -s /jffs/.config /home/root/.config # Added by XIYO

# acme.shが参照するディレクトリにDNSプラグインをマウント // [!code focus]
mount --bind /jffs/acme/dnsapi /usr/sbin/dnsapi  # Added by XIYO, for ACME // [!code focus]
# 毎日午前3時に証明書更新を実行 & ログをWeb UI（System Log）に記録 // [!code focus]
cru a AcmeRenew "0 3 * * * acme.sh --cron --home /jffs/.le 2>&1 | logger -t AcmeRenew" # Added by XIYO // [!code focus]
```

該当スクリプトがない場合は作成して実行権限を付与します。

```sh data-title="terminal"
touch /jffs/scripts/service-start
chmod +x /jffs/scripts/service-start
```

> `service-start`は他のサービスをインストールすると自動的に作られていることが多い...

### 5. 手動マウント実行とcronジョブ登録

私はルーターを再起動するつもりがないため、手動でDNSプラグインをマウントし、cronジョブに証明書発行プロセスを登録しました。

```sh data-title="terminal"
mount --bind /jffs/acme/dnsapi /usr/sbin/dnsapi
cru a AcmeRenew "0 3 * * * acme.sh --cron --home /jffs/.le 2>&1 | logger -t AcmeRenew"
```

### 6. 証明書発行

次のコマンドを実行してワイルドカード証明書を発行します。

```sh data-title="terminal"
acme.sh --issue --dns dns_cf \
-d xiyo.dev -d *.xiyo.dev \
--cert-home /jffs/.le \
--reloadcmd "nginx -s reload"
```

> nginxを使用しているため、`reloadcmd`オプションで証明書発行後にWebサーバーの証明書を更新するようにしました。

## まとめ

これでASUS AC88Uルーターで**Cloudflare APIを活用したACME SSL証明書の自動発行と更新**が完璧に動作するようになります。

このプロセスを経ることで、**毎回手動で証明書を発行する必要がなくなり、SSL証明書が自動的に更新**され、Nginxがこれを自動的にロードするようになります。