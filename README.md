# WebLogic JMS スターター環境（14.1.2.0）

これは、**Oracle WebLogic 14.1.2.0（14c） + JMS + MySQL + Spring Boot + MDB + Flyway** を使った学習・検証用のスターター環境です。  
送信アプリと受信アプリを WebLogic Managed Server 間で疎結合に構成しています。

---

## ✅ 使用バージョン

- WebLogic: `14.1.2.0-generic-jdk17-ol8-241204`
- JDK: 17（WebLogic同梱）
- OS: Oracle Linux 8（ベースイメージ）
- Spring Boot: 2.7.x（WAR形式）
- MySQL: 8.0
- Flyway: 9.x
- Docker / Docker Compose

---

## 📦 構成概要

| コンポーネント         | 説明                                       |
|------------------------|--------------------------------------------|
| WebLogic Admin Server  | ドメイン作成、JMS構成、JDBC構成、デプロイ |
| Managed Server 1       | Spring Boot Webアプリ（JMS送信）           |
| Managed Server 2       | MDB（JMS受信 → MySQLへ保存）               |
| MySQL                  | メッセージ格納用DB（Flyway対応）          |

---

## 🚀 起動手順

### ① Oracle Container Registry にログイン（初回のみ）

```bash
docker login container-registry.oracle.com
```

- ユーザー名：Oracleアカウントのメールアドレス
- パスワード：Oracleアカウントのパスワード

### ② ライセンスに同意（初回のみ）

🔗 https://container-registry.oracle.com  
→ `middleware > weblogic` を検索 → 「Accept License」

---

### ③ イメージを取得

```bash
docker pull container-registry.oracle.com/middleware/weblogic:14.1.2.0-generic-jdk17-ol8-241204
```

---

### ④ このリポジトリをクローン

```bash
git clone https://github.com/enikumaah1998/weblogic-starter.git
cd weblogic-starter
```

---

### ⑤ 一括起動（初回構成含む）

```bash
docker-compose build --no-cache
docker-compose up -d
```

---

## 🌐 アクセスURL

| 機能 | URL |
|------|-----|
| 送信フォーム | http://localhost:8080/send |
| メッセージ一覧 | http://localhost:8080/list |

---

## 🛠 よく使うコマンド

### ログ確認

```bash
docker logs -f wls-admin
```

### MySQL接続

```bash
docker exec -it mysql-db mysql -u demo_user -p
# パスワード: demo_pass
```

---

## 📄 ライセンス

このリポジトリは学習目的で自由に使用可能です。  
ただし、WebLogicの使用には Oracle のライセンス同意が必要です。