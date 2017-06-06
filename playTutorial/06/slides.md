name: inverse
number: 06
layout: true
class: center, middle, inverse
---
# Asynchronous Processing

PlayFramework Tutorial {{ number }}

Noriaki Horiuchi, 2017

---
layout: false
## Agenda

ネットワークやデータベースに対して非同期的にIOをします

- Future
- ネットワーク・アクセス
    - メールの送信
- データベース・アクセス
    - 読み込み
    - 書き込み

---
## Asynchronous Processing

非同期的に処理したい

```
Thread.sleep(1000)
```

- ブロッキングな処理
    - 処理自体は軽いが時間がかかる
        - ネットワークやDBへのアクセス
        - CPUパワーが余る
    - 重い処理
        - 画像・動画処理など
        - CPUパワーを全部使いたい

---
## Future

- Future を使う
    - 並列に実行
    - CPUの有効活用

```
import scala.concurrent.ExecutionContext.Implicits.global

Future {
  Thread.sleep(1000)
}
```

???

まずは何も無しでやる
次にデフォルトのExecutionContextで。ただし3秒かかる、デフォルトの盲点

ExecutionContextはタスクを実行するスレッドプールのようなもの。
これらは、非同期処理を実行する方法を指定するため、Future には不可欠。

最後に専用ExecutionContextを用意して実行、12並列、1秒台で終了

※ 重い処理もFutureで。並列数をコア数に限定すると効率的



---
## Mail

- Play メールプラグインの追加
- application.conf の修正
- ToDo新規作成時のメール通知

---
## Database

- HomeController 内のDBアクセスを非同期化
    - todos
    - findById
    - create

---
## Exercise

- メールの送信
    - 作成時に、ToDoの内容を送信
    - DBからメールアドレスを全件取得して送信
    - 送信対象メールアドレスをフォームから登録
