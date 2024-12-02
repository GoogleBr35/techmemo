# B
<details><summary>bitset</summary>

## 宣言・初期化
```c++
bitset<ビット数> 変数名;
bitset<ビット数> 変数名("ビット列");
bitset<ビット数> 変数名(整数);
```

> ビット列は定数限定
> 整数をビット列としてみなしてbitsetに変換することができる

## ビット演算
<table>
    <thead>
        <tr>
            <th>演算</th><th>演算子</th><th>使い方</th>
        </tr>
    </thead>
    <tr>
        <td>AND</td><td>&</td><td>bs1 & bs2</td>
    </tr>
    <tr>
        <td>OR</td><td>|</td><td>bs1 | bs2</td>
    </tr>
    <tr>
        <td>XOR</td><td>^</td><td>bs1 ^ bs2</td>
    </tr>
    <tr>
        <td>NOT</td><td>~</td><td>bs1 ~ bs2</td>
    </tr>
    <tr>
        <td>左シフト演算</td><td><<</td><td>bs1 << シフトするビット数</td>
    </tr>
    <tr>
        <td>右シフト演算</td><td>>></td><td>bs1 >> シフトするビット数</td>
    </tr>
</table>

演算子の後ろに `=` をつけると複合代入演算子になるよ

> ### 注意点
> 優先順位が低い演算子が多いので、必ず( )で囲む！


## 操作
<table>
    <thead>
        <tr>
            <th>操作</th><th>書き方</th><th>備考</th>
        </tr>
    </thead>
    <tr>
        <td>全てのビットを1にする</td><td>bs.set()</td><td></td>
    </tr>
    <tr>
        <td>あるビットを1にする</td><td>bs.set(location)</td><td>ビットの位置を0始まりのインデックスで指定</td>
    </tr>
    <tr>
        <td>あるビットの値変更</td><td>bs.set(location,value)</td><td>ビットの位置を0始まりのインデックスで指定</td>
    </tr>
    <tr>
        <td>全てのビットを0にする</td><td>bs.reset()</td><td></td>
    </tr>
    <tr>
        <td>全てのビットを反転する</td><td>bs.flip()</td><td></td>
    </tr>
    <tr>
        <td>全てのビットが1か調べる</td><td>bs.all()</td><td>返り値: bool</td>
    </tr>
    <tr>
        <td>あるビットが１か調べる</td><td>bs.test(location)</td><td>ビットの位置を0始まりのインデックスで指定<br>返り値: bool</td>
    </tr>
    <tr>
        <td>いずれかのビットが１か調べる</td><td>bs.anyt()</td><td>返り値: bool</td>
    </tr>
    <tr>
        <td>出力</td><td>bs</td><td></td>
    </tr>
    <tr>
        <td>文字列化</td><td>bs.to_string()</td><td></td>
    </tr>
    <tr>
        <td>整数化</td><td>bs.to_ullong()</td><td>mapのKeyとして使う場合や四則演算を行う場合に<br>ビット数が64ビットを超えている場合は、整数に変換できずに実行時エラー</td>
    </tr>
</table>

> ビットの位置は右から `0, 1, 2` ！


## 2進数リテラル
`0b` に続けて01のビット列を書くと二進表記で整数が書ける
```c++
0b1001 // 9
```


## ビット全探索
2のk乗の値を得るために、1 << kという書き方をする
```c++
for(int tmp; tmp < (1 << 3); tmp++)
```

### ビット全探索のひな型
```c++
for(int tmp = 0; tmp < (1 << ビット数); tmp++) {
    bitset<ビット数> s(tmp);
    // sに対する処理
}
```
bitsetの長さの指定に変数は使えないことに注意<br>
また計算量にも注意 (2^N回以上のループ)


## 計算量
### 整数をビット列として用いる場合
全てO(1)

### bitsetを用いる場合
ビット数をNとしてO(N)だが、<br>
まとめて処理するように実装されていることが多いため、 <br>
64ビット以内であれば基本的にO(1)になる
</details>





# D
<details><summary>deque</summary>
最初に追加したものを取り出す」というキューの操作と 「最後に追加した要素を取り出す」というスタックの操作を同時に行えるデータ構造

## 宣言
 `deque<型> 変数名;`
<br>

## 操作
値の追加
```c++
変数.push_back(値);  // 末尾への値の追加
変数.push_front(値); // 先頭への値の追加
```
値のアクセス
```c++
変数.front() // 先頭の値へのアクセス
変数.back()  // 末尾の値へのアクセス
変数.at(i)   // i番目へのアクセス
```
<br>

</details>





# L
<details><summary>lower_bound / upper_bound</summary>

昇順にソートされた配列において、「x以上の最小の要素」を求める場合にはSTLの `lower_bound` を使うことができる。<br>
同様に、「xを超える最小の要素」を求めるときには `upper_bound` を使うことができる。
<br>

## 使い方
```c++
*lower_bound(配列.begin(), 配列.end(), 値)  // 「値」以上の最小の値
*upper_bound(配列.begin(), 配列.end(), 値)  // 「値」を超えるの最小の値
```
> 先頭に*を付ける必要がある。
<br>

</details>





# M
<details><summary>max</summary>
a, bのうち大きい方の値を返す
<br>

</details>



<details><summary>map</summary>

「特定の値に、ある値が紐付いている」ようなデータを扱うことができる
## 宣言
 `map<keyの型, Valueの型> 変数名;` 

## 操作
<table>
    <thead>
        <tr>
            <th>操作</th> <th>記法</th> <th>備考</th>
        </tr>
    </thead>
    <tr>
        <td>値の追加</td> <td>変数[key] = value;</td> <td> </td>
    </tr>
    <tr>
        <td>値の削除</td> <td>変数.erase(key);</td> <td> </td>
    </tr>
    <tr>
        <td>値のアクセス</td> <td>変数.at(key);<br>変数[key];</td> <td>.at(key) : keyに対応するvalueが存在しない場合はエラーになる<br>[key] : keyに対応するvalueが存在しない場合はValueの型の初期値が追加される</td>
    </tr>
    <tr>
        <td>所属判定</td> <td>変数.count(key);</td> <td> </td>
    </tr>
    <tr>
        <td>要素数の取得</td> <td>変数.size();</td> <td> </td>
    </tr>
</table>

### ループに関するサンプルプログラム
```c++
// Keyの値が小さい順にループ
for (pair<Keyの型, Valueの型> p : 変数名) {
  Keyの型 key = p.first;
  Valueの型 value = p.second;
  // key, valueを使う
}
```
autoを用いて簡潔にできる
```c++
// Keyの値が小さい順にループ
for (auto p : 変数名) {
  auto key = p.first;
  auto value = p.second;
  // key, valueを使う
}
```
<br>

</details>



<details><summary>min</summary>
a, bのうち小さい方の値を返す
<br>

</details>





# P
<details><summary>priority_queue</summary>
「それまでに追加した要素のうち、最も大きいものを取り出す」という処理を行うことができる

## 宣言
 `priority_queue<型> 変数名;` 

## 操作
<table>
    <thead>
        <tr>
            <th>操作</th> <th>記法</th> <th>備考</th>
        </tr>
    </thead>
    <tr>
        <td>要素の追加</td> <td>変数.push(値);</td><td></td>
    </tr>
    <tr>
        <td>最大要素の取得</td> <td>変数.top();</td><td></td>
    </tr>
    <tr>
        <td>最大要素の削除</td> <td>変数.pop();</td><td></td>
    </tr>
    <tr>
        <td>要素数の取得</td> <td>変数.size();</td><td></td>
    </tr>
    <tr>
        <td>queueが空か調べる</td> <td>変数.empty();</td> <td>queueが空ならtrue</td>
    </tr>
</table>

## 使用例
```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  priority_queue<int> pq;
  pq.push(10);
  pq.push(3);
  pq.push(6);
  pq.push(1);

  // 空でない間繰り返す
  while (!pq.empty()) {
    cout << pq.top() << endl;  // 最大の値を出力
    pq.pop();  // 最大の値を削除
  }
}
```
実行結果
```
10
6
3
1
```

## 値が小さい順に取り出されるpriority_queueの宣言
 `priority_queue<型, vector<型>, greater<型>> 変数名;` 

### 使用例
```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  // 小さい順に取り出される優先度付きキュー
  priority_queue<int, vector<int>, greater<int>> pq;
  pq.push(10);
  pq.push(3);
  pq.push(6);
  pq.push(1);

  // 空でない間繰り返す
  while (!pq.empty()) {
    cout << pq.top() << endl;  // 最小の値を出力
    pq.pop();  // 最小の値を削除
  }
}
```
実行結果
```
1
3
6
10
```
<br>

</details>





# Q
<details><summary>queue</summary>
「値を1つずつ追加していき、追加した順で値を取り出す」ような処理を行うことができる

## 宣言
 `queue<型> 変数名;` 

## 操作
<table>
    <thead>
        <tr>
            <th>操作</th> <th>記法</th> <th>備考</th>
        </tr>
    </thead>
    <tr>
        <td>要素の追加</td> <td>変数.push(値);</td><td></td>
    </tr>
    <tr>
        <td>先頭要素へのアクセス</td> <td>変数.front();</td><td>空のqueueに対しての動作は未定義で、実行時エラーになるとは限らない<br> `#define _GLIBCXX_DEBUG` をプログラムの1行目に追加してエラーにできる</td>
    </tr>
    <tr>
        <td>先頭要素の削除</td> <td>変数.pop();</td><td></td>
    </tr>
    <tr>
        <td>要素数の取得</td> <td>変数.size();</td><td></td>
    </tr>
    <tr>
        <td>queueが空か調べる</td> <td>変数.empty();</td> <td>queueが空ならtrue</td>
    </tr>
</table>

## 使用例
```c++
#include <bits/stdc++.h>
using namespace std;

int main() {
  queue<int> q;
  q.push(10);
  q.push(3);
  q.push(6);
  q.push(1);

  // 空でない間繰り返す
  while (!q.empty()) {
    cout << q.front() << endl;  // 先頭の値を出力
    q.pop();  // 先頭の値を削除
  }
}
```
実行結果
```
10
3
6
1
```
<br>

</details>





# R
<details><summary>reverse</summary>
配列変数vecの要素の並びを逆にする
<br>

</details>





# S
<details><summary>set</summary>
重複の無いデータのまとまりを扱うためのデータ型

## 宣言
 `set<型> 変数名;` 
<br>

## 操作
<table>
    <thead>
        <tr>
            <th>操作</th> <th>記法</th> <th>備考</th> <th>計算量</th>
        </tr>
    </thead>
    <tr>
        <td>要素の追加</td> <td>変数.insert(値);</td><td></td><td>logN</td>
    </tr>
    <tr>
        <td>要素の削除</td> <td>変数.erase(値);</td><td></td><td>logN</td>
    </tr>
    <tr>
        <td>所属判定 (bool)</td> <td>変数.count(値);</td><td></td><td>logN</td>
    </tr>
    <tr>
        <td>最小値の取得</td> <td>*begin(変数);</td><td>空のsetにこの操作をしてはいけない</td><td>1</td>
    </tr>
    <tr>
        <td>最大値の取得</td> <td>*rbegin(変数);</td><td>空のsetにこの操作をしてはいけない</td><td>1</td>
    </tr>
</table>

</details>



<details><summary>sort</summary>
vecをソートする（要素を小さい順に並び替える）<br>
大きい順に並べ替えるには、<br>
 `sort(vec.begin(), vec.end(), greater<int>())` <br>
にする
<br>

</details>



<details><summary>stack</summary>
「新しく追加したものほど先に取り出される」ような処理を行うデータ構造

## 宣言
 `stack<型> 変数名;` 

## アクセス
 `変数名.top();` 
<br>

</details>



<details><summary>swap</summary>
a, bの値を交換する
<br>

</details>





# U
<details><summary>unordered_map</summary>

基本的な機能はmapと同じだが、アクセスや検索を高速に行うことができるデータ構造<br>
> 制約
> pairやtupleなどのハッシュ関数が定義されていない型をKeyとして用いることができない
> ループで取り出すときに、どのような順番で取り出されるかが分からない
<br>

</details>



<details><summary>unordered_set</summary>

制約がある代わりに高速なset
> 制約
> pairやtupleなどのハッシュ関数が定義されていない型をKeyとして用いることができない
> ループで取り出すときに、どのような順番で取り出されるかが分からない
> 最大値や最小値を取り出すことができない
<br>

</details>