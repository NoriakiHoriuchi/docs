name: inverse
number: 03
layout: true
class: center, middle, inverse
---
# Form, Validation, I18n and DI

PlayFramework Tutorial {{ number }}

Noriaki Horiuchi, 2017

---
## Agenda

- Form
    - Validation
- I18n (Internationalization)
    - DI (Dependency Injection)

---
## Form And Validation

- ToDo を作成（Create）、変更（Update）する
- `title` の要件
    - 空でない（1文字以上）
    - 50文字以内

---
## Lifecycle
![lifecycle](form-lifecycle.png)

---
layout: true
## Custom Validation

---
### ToDo に期日を設定する

- 文字列で入力する
- 正しい形式でなければエラー
    - java.time API

---
## すること
- テーブルのマイグレーション（期日カラムの追加）
- モデルの修正（変数を追加）
    - コントローラ、ビュー等も修正
    - フォームの期日欄はとりあえずNone
- 期日を設定できるようにフォームを改修
- カスタムバリデーションを作成

---
layout: true
## I18n

---
###  Internationalization
今回は日本語にだけ対応
日本語のメッセージを集めたファイルを作る
必要に応じてそれを取得する

- application.conf の修正
- messages.ja の作成

---
### Dependency Injection
- 「依存性の注入」
- 疎結合にしてテスト性・メンテナンス性を維持するためのしくみ
- PlayFramework は標準で Google の Guice を使用する

コントローラに MessagesApi を Inject するなどする

---
## References

https://www.playframework.com/documentation/2.5.x/ScalaForms

https://www.playframework.com/documentation/2.5.x/ScalaCustomValidations
