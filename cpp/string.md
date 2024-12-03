## 宣言
 `string S`
<br>
<br>

## 入力
 `cin >> S;` 
<br>
<br>

## アクセス
 `S.at(i)` 
> 範囲外アクセスに注意


## 関連する関数
### std::basic_string::substr
#### substr(n)
n番目以降の文字列を取り出す

#### substr(n, m)
n番目以降からm文字だけ取り出す
```c++
S.substr(i, d.size()) == d
```
Sのi+1番目からd.size()番目までを取り出すことができる<br>
index+1なので注意