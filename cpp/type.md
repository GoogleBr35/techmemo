## 型エイリアス
型エイリアス `using 新しい型名 = 型名` を用いると型に別の名前をつけることができる。 pairやtupleなど型名が長くなってしまう場合に型エイリアスを使うと便利。
> `using namespace std;` にも `using` というキーワードが出てくるが、この `using` と型エイリアスの `using` は違う意味なので注意
<br>


## 各型の範囲
<table>
    <thead>
        <tr>
            <th style="text-align: center;"> int </th> <th style="text-align: center;"> int64_t </th>
        </tr>
    </thead>
    <tr>
        <td style="text-align: center;"> -2147483648 </td> <td style="text-align: center;"> -9223372036854775808 </td>
    </tr>
    <tr>
        <td style="text-align: center;"> 2147483647 </td> <td style="text-align: center;"> 9223372036854775807 </td>
    </tr>
</table>

また、符号付正数型や符号無し整数型、小数型の使用メモリ一覧を示す。
<table>
    <thead>
        <tr>
            <th> 型 </th> <th> メモリ量 (bit) </th>
        </tr>
    </thead>
    <tr>
        <td> signed char </td> <td> 8 </td>
    </tr>
    <tr>
        <td> short </td> <td> 16  </td>
    </tr>
    <tr>
        <td> int </td> <td> 32 </td>
    </tr>
    <tr>
        <td> long long </td> <td> 64 </td>
    </tr>
    <tr>
        <td> int8_t </td> <td> 8 </td>
    </tr>
    <tr>
        <td> int16_t </td> <td> 16 </td>
    </tr>
    <tr>
        <td> int32_t </td> <td> 32 </td>
    </tr>
    <tr>
        <td> int64_t </td> <td> 64 </td>
    </tr>
    <tr>
        <td> unsigned char </td> <td> 8 </td>
    </tr>
    <tr>
        <td> unsigned short </td> <td> 16 </td>
    </tr>
    <tr>
        <td> unsigned int </td> <td> 32 </td>
    </tr>
    <tr>
        <td> unsigned long long </td> <td> 64 </td>
    </tr>
    <tr>
        <td> uint8_t </td> <td> 8 </td>
    </tr>
    <tr>
        <td> uint16_t </td> <td> 16 </td>
    </tr>
    <tr>
        <td> uint32_t </td> <td> 32 </td>
    </tr>
    <tr>
        <td> uint64_t </td> <td> 64 </td>
    </tr>
    <tr>
        <td> float </td> <td> 32 </td>
    </tr>
    <tr>
        <td> double </td> <td> 64 </td>
    </tr>
</table>


### 型の指定
プログラム中に直接 `10LL` のように `LL` を付け足して書くと、 `int64_t` として扱う。

## 出力
除算演算子 `/` は、int型の場合小数点以下切り捨てのため、割り算は後にやった方がよい
<br>

double型などは、普通に出力すると適当に四捨五入される。
<br>

 `cout << fixed << setprecision(桁数)` と書くことで、小数点以下の桁数を指定可能。
<br>

### 情報落ち
double型では約16桁までの数字の並びを保持できるので、それを越える小数を正確に扱えない。
差が極端に大きい2つの数を足すと、桁が消える場合がある。
```c++
double x = 1000000000;
double y = 0.000000001;

// 1000000000.000000001 を表現するには19桁分必要 → 扱えない
double z = x + y;  // yの分が消えてしまう

cout << fixed << setprecision(16);
cout << "x: " << x << endl;
cout << "y: " << y << endl;
cout << "z: " << z << endl;
```
実行結果
```
x: 1000000000.0000000000000000
y: 0.0000000010000000
z: 1000000000.0000000000000000
```
小さい数から順に足すことで、情報落ちの影響を減らせる。

### 桁落ち
差が極端に小さい2つの数を引くと、桁が消える場合がある。
<table>
    <thead>
        <tr>
            <th></th> <th style="text-align: center;"> 実際の値 </th> <th style="text-align: center;"> コンピュータ上での値 </th>
        </tr>
    </thead>
    <tr>
        <td> x </td> <td> 0.1234567890123... </td> <td> 0.123456 </td>
    </tr>
    <tr>
        <td> y </td> <td> 0.12334567889012... </td> <td> 0.123345 </td>
    </tr>
    <tr>
        <td> x - y </td> <td> 0.000111111111... </td> <td> 0.000111 </td>
    </tr>
</table>

引き算を行う際にはなるべく差が大きくなるように計算順序を工夫したり、そもそも引き算をなるべく行わないように工夫する必要がある。

### printf関数でのフォーマット指定子
<table>
    <thead>
        <tr>
            <th> 型 </th> <th> フォーマット指定子 </th>
        </tr>
    </thead>
    <tr>
        <td> int </td> <td> %d </td>
    </tr>
    <tr>
        <td> int64_t </td> <td> %ld (%lld)  </td>
    </tr>
    <tr>
        <td> double </td> <td> %lf </td>
    </tr>
    <tr>
        <td> char </td> <td> %c </td>
    </tr>
</table>

> 32ビットシステム上でint64_tをprintfで出力する場合、フォーマット指定子は `%lld` とする必要がある。

## 型の変換
 `(型)変数` でキャストが可能。
<br>

double型→int型は小数点以下切り捨てとなる。
<br>

int型→string型のような数値型以外への変換は基本的にはできない。
### 文字列との変換
 `文字列変数 = to_string(数値変数)` で数値を文字列に変換する。
<br>

 `数値変数 = stoi(文字列変数)` で逆の操作。
<br>

文字列からの変換の対応表を示す。
<table>
    <thead>
        <tr>
            <th> 型 </th> <th> 関数 </th>
        </tr>
    </thead>
    <tr>
        <td> int </td> <td> stoi </td>
    </tr>
    <tr>
        <td> int64_t </td> <td> stoll  </td>
    </tr>
    <tr>
        <td> double </td> <td> stod </td>
    </tr>
</table>

### 暗黙的な数値型同士の変換
<table>
    <thead>
        <tr>
            <th style="text-align: center;"> 型の組 </th> <th style="text-align: center;"> 計算結果の型 </th>
        </tr>
    </thead>
    <tr>
        <td> int, double </td> <td> double </td>
    </tr>
    <tr>
        <td> int, int64_t </td> <td> int64_t </td>
    </tr>
    <tr>
        <td> double, int64_t </td> <td> double </td>
    </tr>
</table>