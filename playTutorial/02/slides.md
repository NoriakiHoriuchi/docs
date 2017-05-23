name: inverse
number: 02
layout: true
class: center, middle, inverse
---
# Database IO

PlayFramework Tutorial {{ number }}

Noriaki Horiuchi, 2017

---
layout:false
## Agenda

- Database
    - Install Docker
    - install ScalikeJDBC
    - Use ScalikeJDBC

---
## Install Docker
- [click here and download Docker](https://docs.docker.com/docker-for-mac/install/)
- 5432番ポートが空いていることを確認
    - `sudo lsof -i:5432`
- dockerを起動
- 以下のコマンドを実行（USERNAMEは各自補完してください）

```
mkdir -p postgresql/data

docker run -d --rm --name postgres -p 5432:5432 -v /Users/${USERNAME}/postgresql/data:/var/lib/postgresql/data postgres:9.6.2-alpine

docker ps
```

---
layout:true
## Setup PostgreSQL

---
### Docker イメージに接続する

- postgresql クライアントのインストール

```
brew install postgresql
```

- play_tutorial データベースを作成する

```
psql -h localhost -U postgres
```

- 以下のSQLを発行し、`play_tutorial` に接続する

```
CREATE DATABASE play_tutorial;

\c play_tutorial
```

- 接続確認

```
\d
```

no relationsと表示されればOK

---
layout:true
## Install ScalikeJDBC

---
### ScalikeJDBC と Flyway を使用する
[ScalikeJDBC](http://scalikejdbc.org/) とは
- DBアクセスライブラリ

[Flyway](https://flywaydb.org/) とは
- DBマイグレーションライブラリ

これからやること
- `build.sbt` を変更する
- `application.conf` を変更する

---
### `build.sbt`

`build.sbt` に以下を追記する

```
libraryDependencies ++= Seq(
    ...
    ...
    ... // 以下7行
    "org.postgresql" % "postgresql" % "42.1.1",
    "org.scalikejdbc" %% "scalikejdbc" % "2.5.2",
    "org.scalikejdbc" %% "scalikejdbc-config" % "2.5.2",
    "org.scalikejdbc" %% "scalikejdbc-play-dbapi-adapter" % "2.5.1",
    "org.scalikejdbc" %% "scalikejdbc-test" % "2.5.2" % Test,
    "ch.qos.logback" % "logback-classic" % "1.2.3",
    "org.flywaydb" %% "flyway-play" % "3.1.0"
)
```

---
### `application.conf`

`application.conf` に以下を追記する

```
db {
    ... // 以下4行
    default.driver=org.postgresql.Driver
    default.url="jdbc:postgresql://localhost:5432/play_tutorial"
    default.username=postgres
    default.password=""
}
```

```
play.modules {
    ... // 以下2行
    enabled += "scalikejdbc.PlayDBApiAdapterModule"
    enabled += "org.flywaydb.play.PlayModule"
}
```

---
### Setup Flyway
以下の名前、内容でファイルを作成します

- `conf/db/migration/default/V1_001_1__Create_todos_table.sql`

```
CREATE TABLE todos
(
  id      SERIAL       NOT NULL,
  title   VARCHAR(100) NOT NULL,
  is_done BOOLEAN      NOT NULL DEFAULT FALSE,
  CONSTRAINT pk_todo PRIMARY KEY (id)
);
```

---
### Setup Flyway
ついでにサンプルデータも仕込んでおきます（必要に応じて手動で実行してください）

- `conf/db/sample/default/todos.sql`

```
--- !Ups

INSERT INTO todos (title) VALUES ('install JDK');
INSERT INTO todos (title) VALUES ('install sbt');
INSERT INTO todos (title) VALUES ('install IntelliJ IDEA');
INSERT INTO todos (title) VALUES ('study Scala');
INSERT INTO todos (title) VALUES ('study PlayFramework');
```

---
layout:true
## データベースに ScalikeJDBC を使う

---

---

### 準備ができましたので、ここからが本番です

---
### すること

- `ToDo` オブジェクトに `SQLSyntaxSupport` を継承させる

```
object ToDo extends SQLSyntaxSupport[ToDo] {
```

- `tableName`、`defaultAlias` を指定する

```
override def tableName = "todos"
def defaultAlias = syntax("t")
val t = defaultAlias
```

---
layout:true
## 既存の実装を書き換える

---
### `def getAll`、`def create` の書き換え

---
### Exercise

- `def getToBeDone`、`def findById`、`def updateTitle`、`def finish` を実装してみましょう
- 既存の `val db: mutable.Map` を消す
- 余裕があれば、ToDoの削除も実装してみる（画面も含め）
    - `def remove(id: Int)`