### 構造体
STLのpair/tupleを拡張したようなもの。
(pair/tupleは構造体を用いて実装されている)

#### 定義
関数の外側、内側どちらにも書ける。
```c++
struct 構造体名 {
  型1 メンバ変数名1
  型2 メンバ変数名2
  型3 メンバ変数名3
  ...(必要な分だけ書く)
};  // ← セミコロンが必要
```
構造体型の値を __オブジェクト__ という
<br>
<br>

#### アクセス
 `オブジェクト.メンバ変数` 
<br>
<br>

### メンバ関数
オブジェクトに関連した処理を行う関数を定義することができる。<br>
使用例
```c++
#include <bits/stdc++.h>
using namespace std;

struct MyPair {
  int x;
  string y;
  // メンバ関数
  void print() {
    // 直接x, yにアクセスできる
    cout << "x = " << x << endl;
    cout << "y = " << y << endl;
  }
};

int main() {
  MyPair p = { 12345, "Hello" };
  p.print();  // オブジェクト`p`の`print`を呼び出す

  MyPair q = { 67890, "APG4b" };
  q.print();  // オブジェクト`q`の`print`を呼び出す
}
```

#### 定義
```c++
struct 構造体名 {
  返り値の型 メンバ関数名(引数の型1 引数名1, 引数の型2 引数名2, ...) {
    // 関数の内容
    //   (ここではメンバ変数に直接アクセスすることができる)
  }
};
```

#### アクセス
 `オブジェクト.メンバ関数(引数1, 引数2, ...)`
<br>
<br>

### コンストラクタ
オブジェクトが作られるときに行う独自の初期化処理
<br>
複数定義することができ、与える引数の型や引数の個数によって自動的に呼び分けることができる。

#### 定義
```c++
struct 構造体名 {
  // コンストラクタ
  構造体名(引数1の型 引数1の名前, 引数2の型 引数2の名前, ...) {
    // コンストラクタの内容
  }
};
```

コンストラクタが引数を取る場合、次のようにオブジェクトの宣言時にコンストラクタの引数に対応する値を渡す必要がある。
<br>

`構造体名 オブジェクト名(引数1, 引数2, 引数3, ...);`
<br>
<br>

### コピーコンストラクタ
関数の引数としてオブジェクトを渡す場合などの条件を満たした場合には、 __コピーコンストラクタ__ という特殊なコンストラクタが呼ばれる。
<br>

コピーコンストラクタを定義しなかった場合には、 「全てのメンバ変数をそのままコピーして新しいオブジェクトを作る」 という動作をするコピーコンストラクタが __自動的__ に作られるので、 ただコピーしたいだけならコピーコンストラクタを自分で書く必要はない。

#### 条件
* 関数の引数としてオブジェクトを渡した場合
* オブジェクトを宣言する際にMyStruct new_obj = old_obj;で初期化する場合
* オブジェクトを宣言する際にMyStruct new_obj(old_obj);の形で初期化する場合
* など

#### 定義
```c++
struct 構造体名 {
  // コピーコンストラクタ
  構造体名(const 構造体名 &old) {
    // コンストラクタの内容
    // (oldの内容を使って初期化などを行う)
  }
};
```
使用例
```c++
#include <bits/stdc++.h>
using namespace std;

struct MyPair {
  int x;
  string y;
  // コンストラクタ
  MyPair() {
    cout << "normal constructor called" << endl;
  }
  // コピーコンストラクタ
  MyPair(const MyPair &old) {
    cout << "copy constructor called" << endl;
    x = old.x + 1;
    y = old.y + " new";
  }
};

int main() {
  MyPair p;  // ここでコンストラクタが呼ばれる
  p.x = 12345;
  p.y = "hello";
  cout << "p.x = " << p.x << endl;
  cout << "p.y = " << p.y << endl;

  MyPair q(p);  // コピーコンストラクタが呼ばれる
  cout << "q.x = " << q.x << endl;
  cout << "q.y = " << q.y << endl;

  MyPair r = q;  // コピーコンストラクタが呼ばれる
  cout << "r.x = " << r.x << endl;
  cout << "r.y = " << r.y << endl;
}
```
実行結果
```
normal constructor called
p.x = 12345
p.y = hello
copy constructor called
q.x = 12346
q.y = hello new
copy constructor called
r.x = 12347
r.y = hello new new
```
<br>

### 演算子オーバーロード
新たに定義した構造体型のオブジェクトに対してC++の演算子を使えるようにすることができる。
> 引数の個数は1つまで

#### 使用例
演算子オーバーロードをメンバ関数として定義
<br>

+演算子のオーバーロード
```c++
    ...
    // 別のMyPair型のオブジェクトをとって、x, yにそれぞれ+したものを返す
    // +演算子をオーバーロード
    MyPair operator+(const MyPair &other) {
        MyPair ret;
        ret.x = x + other.x;  // ここではint型の+演算子が呼ばれる
        ret.y = y + other.y;  // ここではstring型の+演算子が呼ばれる
        return ret;
    }
    ...

    ...
    MyPair c = a + b;
    ...
```

代入演算子のオーバーロード
```c++
    ...
    // 代入演算子をオーバーロード
    void operator=(const MyPair &other) {
        cout << "= operator called" << endl;
        x = other.x;
        y = other.y;
    }
    ...
```

#### 構造体の外側で定義する場合
自分が定義していない構造体(例えばSTLのpairなど)に対しても演算子をオーバーロードすることができる。

使用例 (pairの<演算子をオーバーロードして `.second` を優先して比較する) 
```c++
#include <bits/stdc++.h>
using namespace std;

// .second → .first の順に比較
bool operator<(pair<int, int> l, pair<int, int> r) {
  if (l.second != r.second) {
    return l.second < r.second;
  } else {
    return l.first < r.first;
  }
}
// <演算子 を用いて定義
bool operator> (pair<int, int> l, pair<int, int> r) { return r < l; }
bool operator<=(pair<int, int> l, pair<int, int> r) { return !(r < l); }
bool operator>=(pair<int, int> l, pair<int, int> r) { return !(l < r); }

int main() {
  pair<int, int> a = {1, 5};
  pair<int, int> b = {3, 2};
  cout << (a < b) << endl;  // 0
  cout << (a > b) << endl;  // 1
}
```

### メンバ初期化子リスト
例えばメンバ変数が参照型である場合のように、コンストラクタ内で初期化することができない場合には、 メンバ初期化子リストで初期化する必要がある。

コンストラクタに `:` を続けて書く。

```c++
struct 構造体名 {
  型1 メンバ変数1;
  型2 メンバ変数2;
  ...(必要な分だけ書く)

  構造体名() : メンバ変数名1(初期化内容), メンバ変数名2(初期化内容), ...(必要な分だけ書く)
  {
  }
};
```