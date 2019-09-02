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

### 関数の呼び出し

- 関数名の後に引数のリストを括弧で囲んで呼び出す
- 関数はネストできる
  - 入れ子になった関数は、**外側の関数で宣言された変数にアクセスできる**

### 複合値

- タプルを使用して関数から複数の値を返す

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
  test(tuple.a)
  ```

  





