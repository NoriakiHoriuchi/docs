name: inverse
layout: true
class: center, middle, inverse
---
# Create CRUD Application

PlayFramework Tutorial 01

Noriaki Horiuchi, 2017

---
layout:false
## Agenda

- MVC × CRUD

---
layout: true
## Read

---
layout: true
## Create

---
layout: true
## Update

---
### はじめに：実装を修正
- `Seq[ToDo]` ではなく `Map[Int, ToDo]` へ
    - それに伴いコンパイルエラーを取り除いてください

---
### Scala文法の確認：タプル

```
val tuple2: (Int, Int) = (1, 2)

val tuple3: Tuple3[Int, Int, String] = (1, 2, "String")
```
- 括弧でまとめた値
    - 型はなんでもよい
    - Tuple22まである

---
### Scala文法の確認：タプル
```
val (key, value) = 2 -> ToDo(1, "todo", false)



val map: Map[Int, ToDo] = Map(1 -> ToDo(1, "todo", false))

val list: Seq[(Int, ToDo)] = map.toList
```

- タプルを分解して変数に代入できる
- `Map.toList` すると タプル2のリストが得られる

---
layout: true
## Delete



---
layout: true
## Views

---
layout: true
## References
