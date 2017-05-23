name: inverse
number: 03
layout: true
class: center, middle, inverse
---
# Form and Validation

PlayFramework Tutorial {{ number }}

Noriaki Horiuchi, 2017

---
layout: false
## Agenda

### [Form and Validation](https://www.playframework.com/documentation/2.5.x/ScalaForms)
### [Custom Validation](https://www.playframework.com/documentation/2.5.x/ScalaCustomValidations)

---
layout: true
## Form And Validation

---
### Lifecycle
![lifecycle](form-lifecycle.png)

---
### すること

- ToDo を作成（Create）、タイトルを変更（Update）する
- `title` の要件
    - 空でない（1文字以上）
    - 5文字以内

---
layout: true
## Custom Validation

---
### ToDo に期日を設定する

- 文字列で入力する
- 正しい形式でなければエラー
    - java.time API (Java 8 より追加：JSR310)

---
### すること
- テーブルのマイグレーション（期日カラムの追加）
- モデルの修正（変数を追加）
    - コントローラも修正
    - フォームにはまだ期日欄を設置しない
- 期日を設定できるようにビュー、フォームを改修
- カスタムバリデーションを作成

---
layout: false
## Exercise

- タイトル変更機能にもバリデーションを適用する

---
layout: true
## Past Exercise

---
### 第1回

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

---
###  第2回

- `def getToBeDone`、`def findById`、`def updateTitle`、`def finish` を実装してみましょう
- 既存の `val db: mutable.Map` を消す
- 余裕があれば、ToDoの削除も実装してみる（画面も含め）
    - `def remove(id: Int)`
