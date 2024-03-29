# Swift 学習メモ(Swift5.1)

## 単一処理

### 定義

- 変数は`var` 

- 定数は`let`

  - 型指定する場合：変数の後ろをコロンで区切る
  
    ```
    let doubleVal:Double = 1
    ```
  
  - 型指定しない場合：初期化時に値から型が決められる
  
    ```
    let doubleVal = 1.0
    ```

### 文字列

- 文字列は ”” で囲む

- 連結：**+演算子**

  - ```
    var name = "hoge" + " " + "hoge"
    ```

- 文字列を追加：**+=演算子**

  - ```
    name += "hoge"
    ```

- 文字列内に値を入れる

  - （）内に値を書き、 \を前に書く

  - ```
    let apples = 3
    let appleSummary = "I have \(apples) apples."
    ```

- 複数行

  - ```
    let name = """
    hoge.
    hogehoge.
    """
    ```

### 配列

- 配列は[]を使って定義

- 要素追加は`append`で追加する

  - ```
    var array = ["hoge","hoge"]
    array.append("hoge2")
    ```

- 空配列、ディクショナリ：初期化子構文を用いる

  - ```
    let emptyArray = [String]()
    let emptyDictionary = [String: Float]()
    ```

## 制御フロー　

- Time:1.5h

### ループ

- for文
  
- for-inで記述する
  
    - インデックスの範囲を指定するには`..< `を用いる
    
    ```
    var total = 0
    for i in 0..<4 {
        total += i
    }
    print(total)
    ```
  
    
  
- switch文

  - case内のコードを実行した後にSwitch文から抜ける
    - **breakしなくて良い**

- While,repeat-while文

  - repeat-while
    - Do-whileと同じ原理
    - 一回はループが実行される

### オプショナル値

- 値があるかもしれないし、ないかもしれないことを表す
- オプショナル値型であることを表すために、型名に**?**を付ける
- 値を持つオプショナル値は**!**を付けることで値を取り出せる

```
var optionalString: String? = "Hello"
print(optionalString!)
```

- 値がないことを表すのは**nil**
- if文でオプショナル値に値があるか知ることができる

```
print(optionalString == nil)	
```

  - オプショナル値の判定処理

      - **if let tmpVar = OptionalVar** 構文

          - オプショナル値のありなし判定と同時に値を変数に束縛できる
          - オプショナル値がnilの場合は{}内がスキップされる

      - ```
        var optionalName: String? = "John Appleseed"
        var greeting = "Hello!"
        if let name = optionalName {
            greeting = "Hello, \(name)"
        }
        ```

    - `??`演算子

      - `オプショナル値 ?? デフォルト値`のように記述する
      - オプショナル値がnilの場合にデフォルトの値が代入される

      ```
      let nickName: String? = nil
      let fullName: String = "John Appleseed"
      let informalGreeting = "Hi \(nickName ?? fullName)"
      ```

    #### オプショナル型と非オプショナル型の違い
    
    - オプショナル型の変数はnilの代入が可能であるが、非オプショナル型の変数はnilを代入できない
    - オプショナル型の変数の宣言には、データ型の最後に"?"か"!"をつける
    
    #### オプショナル型の扱い
    
    - オプショナル型を非オプショナル型と同様に扱うには「アンラップ」という処理が必要
    - アンラップをしない場合、オプショナル型の値にはOptional()というラッピングがされる
    
    #### アンラップの方法
    
    - オプショナル型の宣言時に"!"を使うと、自動でアンラップされるようになる
    - アンラップには「強制的アンラップ」、「オプショナルバインディング」、「オプショナルチェイニング」の3つの方法がある。
    - 「強制的アンラップ」はオプショナル型の変数に最後に"!"をつけて強制的にアンラップする方法
    - 「オプショナルバインディング」は条件式を使って、オプショナル型がnilでないときだけアンラップして処理をおこなう方法
    - 「オプショナルチェイニング」はオプショナル型の変数に最後に"?"をつけて、オプショナル型がnilでないときだけ続けてプロパティを取得したり、メソッドを呼び出す方法で取得できる値はすべてオプショナル型になる

## 関数とクロージャー

### 関数

- 関数名の後に引数のリストを括弧で囲んで呼び出す
- 関数の戻り値は、`->`の後に指定
- 関数はネストできる
  - 入れ子になった関数は、**外側の関数で宣言された変数にアクセスできる**

#### 特徴

- 戻り値として関数を返すことが可能

```
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7) // 結果：8
```

- 引数として関数を取ることが可能

- 引数
  - 可変長引数
    - 引数の型名の後に`Int...のように定義
  - In-Out引数
    - 関数に渡した引数を、関数内で変更したい場合に、引数定義の先頭に記述

#### 複合値

- 関数の戻り値にタプルを使用して、関数から複数の値を返すことができる

- タプル

  - 順序付けされた値の集合体
  - 値の追加、削除、繰り返し処理はできない

- ラベル付き

  - 名前または番号で参照できる

  ```
  func test(a: String, b: Int) -> (Int, String) {
      return (b, a)
  }
   
  let tuple = ("aaa", 1)
  test(tuple.a)　// 結果：aaa
  ```

### クロージャー

#### 説明

- 自分を囲むスコープ内の変数を参照する関数
- C言語：関数ポインターのようなもの

#### 定義

```
 { (引数名:引数の型) -> 戻り値の型 in
    処理
 }
```

#### 使い方

```
let closure = { (num1: Int, num2: Int) -> Int in return num1 + num2 }
closure(1, 2) // 結果：3
```

- クロージャーを簡潔に書くための方法

  - 処理が単文の場合は戻り値の型が省略可能

  ```
  let closure = { (num1: Int, num2: Int) in  num1 + num2 }
  closure(1, 2) // 結果：3
  ```

  - 型がわかっている場合は省略可能

  ```
  let closure: (Int, Int) -> Int
  let closure = { (num1, num2) in  num1 + num2 }
  closure(1, 2) // 結果：3
  ```

  - 引数名を省略可能（名前ではなく番号を指定する）
    - `$`をつけると引数の代わりとなる

  ```
  let closure: (Int, Int) -> Int
  let closure = { $0 + $1 }
  closure(1, 2) // 結果：3
  ```

  

#### 参考資料

- [Swiftの関数](https://qiita.com/HaNoHito/items/43db7bffb7412daadfa8)
- [【Swift】クロージャ（基本編）](https://qiita.com/funafuna/items/9be7653cf8d002bac4ec)

## オブジェクトとクラス

### クラス

#### 特徴

- **クラスはコード中で常に参照渡し**される

```
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

#### インスタンス

- 作成
  
  - クラス名の後に`()`をつけて関数のように宣言する
  
- ```
  var shape = Shape()
  ```

- 属性

  - `.`（ドット）をつけてアクセスする

  ```
  shape.numberOfSides = 7
  ```

- イニシャライザ

  - メソッド名の前に`func`は不要

  ```
      init(name: String) {
          self.name = name
      }
  ```

- デイニシャライザ

  - obj-c：`dealloc`
  - Swift：`deinit`

#### サブクラス

- クラス名の後に`:`で区切ってスーパークラス名を置く

```
class サブクラス名: スーパークラス名{
 hogehoge
}
```

- オーバーライド
  - スーパークラスの実装をオーバーライドしたサブクラスのメソッドは、`override`と書く

```
override func メソッド名()
```

- setter/getter
  - プロパティに持たせることが可能
  - setterの中で、新しい値には暗黙の名前**newValue**がある
    - setの後の括弧中に明示的に名前を与えることも出来る

```
init(hoge: Int) {
   self.hoge = hoge
}

var hogehoge: Int{
  get {
        return hoge
    }
    set {
        hoge = newValue + 3
    }
}
```

  - プロパティ監視
      - willset
          - 変数の`値の変更直前`に実行される
    - didset
      - 変数の`値の変更直後`に実行される
    - 値が変更されが場合に処理を行いたい時に使用する
      - 特定のメソッドを呼ぶ
      - イベントを通知する
      - など...

## 列挙と構造体

### 列挙

#### 定義

- 列挙は`enum`を使用する

#### 特徴

- 標準型

- ```
  enum Signal: Int {
   case blue
   case yellow
   case red
  }
  let blueValue = Signal.blue
  //enum型がわかっていれば省略可能
  let blueValue: Signal = .blue
  ```

- 値型

  - 各要素に指定した値を割り当てられる

  - `enum enum名: 値型名`

    - 整数値
    - 浮動小数点数値
    - 文字列

  - `rawValue`：要素に割り当てられた値を取得できる

    ```
    enum Signal: Int {
     case blue,yellow,red
    }
    let blueValue: Signal = .blue
    blueValue.rawValue // 0
    ```

- 関連型

  - caseに複数の値を持たせることが可能

- メソッドを定義

- ```
  enum Signal: Int {
   case blue,yellow,red
   
   func meaning: String {
          switch self {
          case .blue:
              return "進め"
          case .yellow:
              return "注意"
          case .red:
              return "止まれ"
          }
      }
  }
  let blueValue: Signal = .blue
  print(blueValue.meaning()) // 進め
  ```

### 構造体

#### 定義

- `struct`を使用する

#### 特徴

- **構造体はコード中で常にコピー渡しされる**
- **クラス**との違い
  - 継承できない
  - deinitializerがない
  - 実行時の型キャストがない

#### enumのネスト

- 関係性を階層構造で表すことができる

```
struct Trump {
	enum pattern{
    case spades, hearts, diamonds, clubs 
  }
  enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king
  }
  
  let patternType: pattern
  let rankType: Rank   
}

let card = Trump(patternType: .spade, rankType: .jack)
print("This card is \(card.patternType) of \(card.rankType)")
```





#### 参考資料

- [Swiftのenumについてまとめてみる](https://qiita.com/cyan-drop/items/4db9d61f0794643eb996)



## プロトコルと拡張機能

### protocol

#### 特徴

多言語ではインターフェースと呼ばれる。

継承先のクラスで実装すべき、メソッドなどを定義する。

#### 宣言

```
protocol hogeProtocol
{
	var Fuga:String {get set}
    
  func  FugaFuga() -> Void 
}
```

#### 呼び出し方法

```
 class Test : hogeProtocol
{
    var fuga:String!
    
    var Fuga: String{
        get{
            return self.fuga
        }
        set{
            self.fuga = newValue
        }
    }   
    // 実装しないとエラー
    func  FugaFuga() -> Void{
        print(self.Fuga)
    }
}

var hoge:hogeProtocol = Test()
hoge.Fuga = "ほげ"
hoge.FugaFuga() //ほげほげ
```

### Extention

#### 特徴

クラス・データ型・構造体などの機能を拡張する。

データ型にプロジェクト内でよく使う処理の追加やライブラリの拡張・プロトコル実装などに利用する。

#### 宣言

- データ型の拡張

```
例：
extension Int
{
    var Rate: Float
    {
        return (Float)(self) / 100.0
    }
}
print(80.Rate) // 0.8
```

- クラスの拡張
  - データ型同様に行えるが、`self`で取得できるものはない。また、クラス街の扱いであるので`private`はアクセスできない。

  - プロトコル実装などをクラス外書きたい場合

    - クラスとプロトコル実装のエクステンションを同一ファイル内に書く場合は`fileprivate`というアクセス指定子でアクセス可能となる。

    ```
    extention 元のクラス: プロトコル
    ```

```
// StrProperty.swift

protocol HogeStrProperty {
    var HogeStr:String{ get }
}
```

```
// class.swift
class HogeHoge {
    fileprivate let hogeStr = "HogeHoge"
}

extension HogeHoge:HogeStrProperty {
    public var HogeStr:String {
        get {
            return self.hogeStr
        }
    }
}
```

