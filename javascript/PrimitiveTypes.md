# Primitive Types

<details><summary>const</summary>

## constの変数は値を変えれない訳ではない
### 再代入できない例
```JavaScript
    const num = 7;
    num = 100; // error
```

### 値を変えれる場合
```JavaScript
    const array = [1, 2, 3];
    array = [4, 5, 6]; // 再代入なのでエラー
    array[1] = 5; // 参照型において中身の変更はできる
```

### なぜ？
> const 宣言は格納された値に読み取り専用の参照を作りますが、JavaScriptの定数(const)は再代入できないだけで必ずしも変更できないわけではない。<br>
> 定数が制限するのはアドレス変更、つまり再代入。
> 参照型ではアドレス変更をせずに値を変更できるため、定数でも値の変更ができる。<br>
> 参照型*(Array, Objectなど)*では、値を格納している参照値を変更せず格納された値を変更できる。

[参考](https://qiita.com/NoobieGull/items/11d8c2bdcd82a01e8146)

</details>