## 参照の宣言

````c++
int a = 0;
int &b = a;
````

## 参照渡しの利点

### 関数の結果を複数返したい場合

```c++
#include <bits/stdc++.h>
using namespace std;

// a,b,cの最大値、最小値をそれぞれminimumの参照先、maximumの参照先に代入する
void min_and_max(int a, int b, int c, int &minimum, int &maximum) {
    minimum = min(a, min(b, c));  // 最小値をminimumの参照先に代入
    maximum = max(a, max(b, c));  // 最大値をmaximumの参照先に代入
}

int main() {
    int minimum, maximum;
    min_and_max(3, 1, 5, minimum, maximum);  // minimum, maximumを参照渡し
    cout << "minimum: " <<  minimum << endl;  // 最小値
    cout << "maximum: " <<  maximum << endl;  // 最大値
}

```

min_and_maxから複数の結果 (minimumとmaximum) が返ってきている
<br>
<br>

### 無駄なコピーを減らす

````c++
#include <bits/stdc++.h>
using namespace std;

// 配列の先頭100要素の値の合計を計算する (参照渡し)
int sum100(vector<int> &a) {
    int result = 0;
    for (int i = 0; i < 100; i++) {
        result += a.at(i);
    }
    return result;
}

int main() {
    vector<int> vec(10000000, 1);  // すべての要素が1の配列

    // sum100 を500回呼び出す
    for (int i = 0; i < 500; i++) {
        cout << sum100(vec) << endl;  // 参照渡しなので配列のコピーは生じない
    }
}

````

実行結果

````
100
100
100
100
... (500回実行される)
````

実行時間
15 ms
<br>
参照渡しをしなかった場合、1000万要素の配列のコピーが500回生じ、実行時間が数百倍になる
<br>
<br>

### 範囲for文での参照

````c++
vector<int> a = {1, 3, 2, 5};
for (int x : a) {
  x = x * 2;
}
// aは{1, 3, 2, 5}のまま
````

````c++
vector<int> a = {1, 3, 2, 5};
for (int &x : a) {
    x = x * 2;
}
// aは{2, 6, 4, 10}となる
````

配列の要素を書き換える処理を簡潔に書ける
<br>
<br>

## 注意点

__参照先の指定して初期化__ する必要がある

````c++
int a = 0;
int &b; // 初期化されていない参照
````

エラー出力

````c++
./Main.cpp: In function ‘int main()’:
./Main.cpp:6:8: error: ‘b’ declared as reference but not initialized
   int &b;
        ^
````

__vectorの要素への参照を生成した後は元のvectorの要素数が変わるような操作を行わない__ ようにしなければならない
<br>

また参照を用いても、 __スコープの制約を越えて変数を使用することはできない__