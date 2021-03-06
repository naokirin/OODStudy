# 不思議のダンジョン2 風来のシレン

アイテム周りに関連した簡易的な仕様を元に設計してみる

![Shiren](http://blog-imgs-27.fc2.com/d/o/u/doughtful/shiren02.gif)

## プレイヤー

* プレイヤーはゲーム中に1人しかいない

### ステータス

* 名前
* HP
* 基本攻撃力
* 剣のつよさ (装備している武器によって決まる)
* 盾のつよさ (装備している盾によって決まる)


### 攻撃する

* プレイヤーはモンスターにのみ攻撃できる

#### モンスターに攻撃する

* そのモンスターにダメージを与える
 * ダメージをいくら与えるかは、ダメージ計算を参照
* 装備していると効果のある武器の効果
 * ゴースト系に2倍のダメージ
 * 1ツ目系に2倍のダメージ
 * ドレイン系に2倍のダメージ
 * ドラゴン系に2倍のダメージ

### 攻撃される

* ダメージを受ける
 * ダメージをいくら受けるかは、ダメージ計算を参照
* 装備していると効果のある盾の効果
 * ゴースト系からのダメージを半減
 * 1ツ目系からのダメージを半減
 * ドレイン系からのダメージを半減
 * ドラゴン系からのダメージを半減


## 敵

* 敵はゲーム中に複数登場する

### ステータス

* 名前
* HP
* 攻撃力
* 防御力
* 属性


### 攻撃する

* 敵はプレイヤー、敵の両方に攻撃できる

#### プレイヤーに攻撃する

* プレイヤーにダメージを与える
 * ダメージをいくら与えるかは、ダメージ計算を参照

#### 敵に攻撃する

* その敵にダメージを与える
 * ダメージをいくら与えるかは、ダメージ計算を参照


### 攻撃される

* ダメージを受ける
 * ダメージをいくら受けるかは、ダメージ計算を参照

### 属性の種類

* ゴースト
* 1ツ目
* ドレイン
* ドラゴン
* なし


## アイテム

* プレイヤーはアイテムを20個まで所持できる
* プレイヤーはアイテムは拾うことができる
* アイテムを拾ったとき、所持しているアイテムが20個未満ならそのアイテムを所持する
* 所持しているアイテムの順序は拾った順になる
* アイテムは捨てることができる
* プレイヤーは武器、盾を各種1つずつ装備することができる

### 武器

* 名前を持つ
* 0以上の整数値の攻撃力を持つ
* -99から99までの整数値の修正値を持つ
* プレイヤーは所持しているアイテムのうち、1つの武器を装備できる
* 武器を装備したプレイヤーの剣のつよさは、装備した武器のつよさになる
* 武器のつよさは攻撃力に修正値を足したものとなる
* 武器のつよさが0未満となった時は、武器のつよさは0とする
* 武器のつよさが255以上となった時は、武器のつよさは255とする

### 盾

* 名前を持つ
* 0以上の整数値の防御力を持つ
* -99から99までの整数値の修正値を持つ
* プレイヤーは所持しているアイテムのうち、1つの盾を装備できる
* 武器を装備したプレイヤーの盾のつよさは、装備した盾のつよさになる
* 盾のつよさは攻撃力に修正値を足したものとなる
* 盾のつよさが0未満となった時は、盾のつよさは0とする
* 盾のつよさが255以上となった時は、盾のつよさは255とする


## アイテムの効果

### 武器の効果

* ゴースト系に2倍のダメージ
* 1ツ目系に2倍のダメージ
* ドレイン系に2倍のダメージ
* ドラゴン系に2倍のダメージ

### 盾の効果

* ゴースト系からのダメージを半減
* 1ツ目系からのダメージを半減
* ドレイン系からのダメージを半減
* ドラゴン系からのダメージを半減


## アイテム合成

* 同じ種類(武器、盾)のアイテム同士は合成することができる
* 合成すると合成するアイテムは消える
* 合成すると基本になるアイテムの修正値に、合成するアイテムの修正値が加えられ、基本になるアイテムに、合成するアイテムの効果が追加される
* 合成時に同じ効果が重複する場合、その重複する効果は追加されない

## ダメージ計算

* 特に明記していない場合は、計算後に少数点以下を四捨五入した値となる
* 攻撃を受けたプレイヤーや敵は、ダメージの数値分、HPが減る
* HPは0以下にはならない
* m^nはmのn乗の意味で用いている

### プレイヤー

* 攻撃力
 * [基本攻撃力] + (([基本攻撃力] * [剣の強さ] / 16) の小数点以下を四捨五入した値)
 * ただし、255を超えた場合は255となる
* ダメージ
 * [攻撃力] * (15/16)^[敵の防御力]

### 敵

* ダメージ (プレイヤーが受ける場合)
 * [攻撃力] * (15/16)^[プレイヤーの盾の強さ]
* ダメージ (プレイヤー以外)
 * [攻撃力] * (15/16)^[敵の防御力]


## ターンについて

* ターンについての処理はなくてよい

## あえて捨てている機能

基本的に、アイテム、合成に関与しないものや、仕様の簡易化のために削っている

* ターンごとの処理
* 死亡判定
* レベル関連の機能
* プレイヤーのちから
* 空腹
* ダメージの乱数
* 命中率に関する機能
* 敵の特殊能力、特性
* 腕輪、矢、杖、草、種、食料、巻物、壺、肉、ギタン
* 未識別のアイテム
* 投げる、置く
* 罠
* 状態異常
