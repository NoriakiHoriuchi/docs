name: inverse
number: 04
layout: true
class: center, middle, inverse
---
# I18n and DI

PlayFramework Tutorial {{ number }}

Noriaki Horiuchi, 2017

---
layout: false
## Agenda

### [I18n (Internationalization)](https://www.playframework.com/documentation/2.4.x/ScalaI18N)
### [DI (Dependency Injection)](https://www.playframework.com/documentation/2.4.x/ScalaDependencyInjection)

---
layout: true
## I18n

---
###  Internationalization
- 今回は日本語にだけ対応
- 日本語のメッセージをまとめたファイルを作る
- 必要に応じてメッセージを取得して表示

---
### Dependency Injection
- 「依存性の注入」
- 疎結合にしてテスト性・メンテナンス性を維持するためのしくみ
- PlayFramework は標準で Google の Guice を使用する

---

### すること

- application.conf の修正
- messages.ja の作成
- コントローラに MessagesApi を Inject する
- テンプレートに Messages を Inject する

???

BuiltinModule.scala の紹介
実際に注入する際は Modules を定義する
