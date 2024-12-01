## pair

### 宣言・初期化
```c++
pair<型１, 型2> 変数名(値1, 値2);
// または
make_pair(値1, 値2);
```

### アクセス
```c++
変数名.first; // 1つ目の値
変数名.second; // 2つ目の値
```

> 配列にpair型を格納した際に
> ```c++
>   for(int i = 0; i < N; i++) {
>       cout << a.at(i).first << a.at(i).second << endl; 
>   } 
> ```
> のようにアクセスするとエラーが出るので注意。

### 分解
```c++
p = make_pair("*", 1);

型1 変数1;
型2 変数2;
tie(変数1, 変数2) = p;
```
変数1, 変数2にそれぞれpairの1番目、2番目の値が代入される

```c++
cout << 変数1 << endl;
cout << 変数2 << endl;
```
実行結果
```
*
1
```
<br>

## tuple

pairの一般化「複数個の値の組」を表す型

### 宣言

```c++
tuple<型1, 型2, 型3, ...> 変数名(値1, 値2, 値3, ...);
// または
make_tuple(値1, 値2, 値3, ...);
```

### アクセス

```c++
get<k>(tuple型変数); // k番目にアクセス
```
kは0から始まる

また、変数でなく定数である必要がある

### 分解

```c++
data = make_tuple(2, "WORLD", true)

型1 変数1;
型2 変数2;
型3 変数3;
︙
tie(変数1, 変数2, 変数3, ...) = data;
cout << 変数1 << " " << 変数2 << " " << 変数3 << endl;
```
実行結果
```
2 WORLD 1
```
<br>

## pair同士/tuple同士の比較
1番目の値が最優先で比較され、等しい場合は2番目の値で比較する。…<br>
のように1番目の値から順に比較される。
<br>

 `==` は全ての値が等しい場合<br>
 `!=` は1つ以上の異なる値が存在する場合<br>
 にtrueとなる。

```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  vector<tuple<int, int, int>> a;
  a.push_back(make_tuple(3, 1, 1));
  a.push_back(make_tuple(1, 2, 100));
  a.push_back(make_tuple(3, 5, 1));
  a.push_back(make_tuple(1, 2, 3));
  sort(a.begin(), a.end());

  for (tuple<int, int, int> t : a) {
    int x, y, z;
    tie(x, y, z) = t;
    cout << x << " " << y << " " << z << endl;
  }
}
```
実行結果
```
1 2 3
1 2 100
3 1 1
3 5 1
```
<br>

## ignore
pairやtupleを分解する際、いらない要素を捨てたい場合は `ignore` をtieの引数に渡す。

```c++
    pair<int, int> p(3, 5);
    int right;
    tie(ignore, right) = p;
    cout << right << endl;

    tuple<int, string bool> tpl(2, "hello", false);
    int x;
    string s;
    tie(x, s, ignore) = tpl;
    cout << x << " " << s << endl;
```
実行結果
```
5
2 hello
```
<br>

## auto
初期化を伴って変数を宣言する場合や範囲for文において、型の部分にautoと書くことによって型を省略することができる。