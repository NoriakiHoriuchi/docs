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
## すること
- テーブルのマイグレーション（期日カラムの追加）
- モデルの修正（変数を追加）
    - コントローラも修正
    - フォームにはまだ期日欄を設置しない
- 期日を設定できるようにビュー、フォームを改修
- カスタムバリデーションを作成
