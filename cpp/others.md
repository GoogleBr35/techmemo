## bool型と関数の戻り値
```c++
bool f(bool a) {
    if(a) return true; // a = true
    else return false; // a = false
}

int main(void) {
    bool a;
    while(true) {
        if(f(a)) break; // a = trueのときにはループを抜けたい
    }
}
```
このコードは、無限ループに陥り停止しない可能性がある。
以下のように、bool型変数の値を更新し、その変数を返すと終了する。
```c++
bool f(bool a) {
    bool flag = false;
    if(a) flag = true;
    return flag; // a == trueでtrue、a == falseでfalse
}

int main(void) {
    bool a;
    while(true) {
        if(f(a)) break; // a = trueのときにはループを抜ける
    }
}
```
最初からreturn文を書くのは関数の最後だけと決めておけば防げるだろう。
<br>

## 各桁に対する操作
10進法なら、
```
N % 10 -> 1の位
N /= 10
N % 10 -> 10の位
...
```
というように `%` , `/` を用いて操作するとよい。
<br>

使用例 (10進法から2進法への書き換え)
```c++
#include <bits/stdc++.h>
using namespace std;

int main(void) {
    int N = 1234; // 変換前

    stack<int> bits;
    while(N >= 1) {
        bits.push(N % 2);
        N /= 2;
    }
    while(bits.size() > 0) {
        cout << bits.top();
        bits.pop();
    }
    cout << endl;
    return 0;
}
```
発展的話題として、2 進法や 3 進法や 16 進法など、10 進法以外の n 進法への書き換えなども、ほぼ同じ処理で実現できる。