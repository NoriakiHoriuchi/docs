name: inverse
number: 01
layout: true
class: center, middle, inverse
---
# Create CRUD Application

PlayFramework Tutorial {{ number }}

Noriaki Horiuchi, 2017

---
layout:false
## Agenda

- ToDo Application
    - Show all ToDos
    - Show a ToDo
    - create a new ToDo

---
layout: true
## Show All ToDos

---
### Model

- ToDo クラスの作成
    - 保持するデータ
        - ID：整数
        - タイトル：文字列
        - 完了/未完了：真偽値

```
case class ToDo(id: Int, title: String, isDone: Boolean)
```

---
### Model

- ToDo オブジェクトの作成
    - ToDo クラスと対になる、シングルトンなオブジェクト
        - 個別のインスタンスに紐付かないあれこれを定義
    - Map を "DB" として使用します
    - ToDoクラスを操作するメソッドを作成
        - メソッド：`def`
        - getAll, getToBeDone, findById, create, updateTitle, finish
    - 本体部分は `???` と置いて、仮実装としておきます

```
object ToDo {
  val db: mutable.Map[Int, ToDo] = mutable.Map()
  ...
  ...
}
```

---
### Disable Filters

コントローラの実装に入る前にすることがあります

- 全てのリクエストに適用したい処理を定義するのが「フィルタ」
- 主にセキュリティ関連の機能
- ハンズオンには不要なので一旦全て解除します

---
### Controller

- コントローラ HomeController の編集
- テンプレート views/index.scala.html の編集
- ルーティング定義ファイル conf/routes の編集

---
### Model (再)

- ToDo.findAll の処理を実装します

```
  def getAll: Seq[ToDo] = db.values.toList
```

---
### 動作確認

プロジェクトルートで以下のコマンドを実行

```
$ sbt

[play-scala-seed] ~run
```

http://localhost:9000/ にアクセス

---
layout: false
## Show a ToDo

すること

- HomeController に `def show` を追加
- conf/routes を修正
- `ToDo.findById` を実装
- views/show.scala.html テンプレートファイルを新規作成
- views/index.scala.html に個別のToDo画面へのリンクを追加

---
## Create a new ToDo

すること

- HomeController に `def create` を追加
- conf/routes を修正
- `ToDo.create` を実装
- views/index.scala.html に新規作成フォームを追加

---
## Exercise

一覧画面で試してみましょう

- 現在は ToDo の順番が保証されません
    - ToDo を昇順に並べる
    - ToDo を降順に並べる
- 現在は完了かどうかにかかわらず表示しています
    - 未完了の ToDo のみ表示しましょう
        - db から選択的に取得する方法
        - テンプレート内で表示を切り替える方法

個別の画面で試してみましょう

- ToDo のタイトルを変更する
- ToDo を完了する
- ToDo を削除する
