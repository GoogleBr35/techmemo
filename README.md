# 困ったときの為のTips

## マークダウン方式(md)について

[参考記事](https://qiita.com/Qiita/items/c686397e4a0f4f11683d#links---%E3%83%AA%E3%83%B3%E3%82%AF "Markdown記法 チートシート")<br>
__※一部の記法はGitHubに対応していないので注意__
<details><summary>コード</summary>

### コードブロック

「c」のコードをファイル名「sample.c」で表示したいときは __バッククオート(__  `` ` ``  __)__ または __チルダ(__ `~` __)__ を使い、以下のようにする。

````
```c:sample.c
#include <stdio.h>touch
int main() {
    printf(Hello, world!\n);
    return 0;
}
```
````

### インライン表示

コードをインライン表示したいときは `` `printf(Hello, world!);` `` のようにする。

### Diff

Diffを用いる場合は、各シンタックスに新たに `diff_*` という名前をつけ、行の先頭に `-, +` を追加する。

```diff_c++
#include <stdio.h>
int main() {
- printf("hello, world!");
+ printf("Hello, world!");
    return 0;
}
```

</details>

<details><summary>テキストの装飾</summary>

### 強調・強勢

 `_` か `*` で囲むとHTMLのemタグになる。GitHubでは *italic type* 。<br>
 `__` か `**` で囲むとHTMLのstrongタグになる。GitHubでは __太字__ 。

### 打消し線

打消し線を使うには、`~~` で囲む。 ~~ 打消し ~~
:::note warn
GitHubでは打消し線が反映されない可能性あり。
:::

### 折りたたみ

HTMLの詳細折りたたみ要素を使える。 `details` タグで囲む。要約として表示したい文章は `summary` タグで記載。<br>
 `open` 属性をつけると折りたたみを広げた状態にできる。
:::note warn
HTMLタグの下には空行が必要。
:::
<details open><summary>サンプル</summary>

これはサンプルの中身です。
</details>

### 改行

改行するには、HTMLタグの `<br>` を用いるか、空行を一行つくる。

### Note

目を引く形で補足説明をしたい場合、 `:::note * :::` で囲む。<br>
 `*` は `info` , `warn` , `alert` の3種類。また、`:::note *` と `:::` は別の行にする必要がある。
</details>

<details><summary>リスト</summary>

### 順序無しリスト
文頭に `*` を置く。

### 数字付きリスト
文頭に `1. ` のように `数字とドット` を置く。
<br>

ドットの次には半角スペースが必要。
</details>

<details><summary>引用</summary>

文頭に `>` を置く。
<br>
複数行にまたがる場合、改行のたびにこの記号を置く必要がある。
<br>
引用の上下には空行がないと正しく表示されない。
<br>
例

> これは引用の例です。
</details>

<details><summary>リンク</summary>

タイトル (リンク上にマウスホバーすることで表示される) 付きのリンク

````md
[リンクテキスト](URL "タイトル")
"タイトル"はオプション
````

結果
<br>

[リンクテキスト](http://qiita.com "タイトル")

</details>

<details><summary>画像埋め込み</summary>
タイトル有の画像を埋め込む
<br>

```md
![代替テキスト](画像のURL "画像タイトル")
```
![代替テキスト](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse3.mm.bing.net%2Fth%3Fid%3DOIP.1TvSemgKVDJn8obvK6lNSAHaHa%26pid%3DApi&f=1&ipt=c0f4418824d18ca7d5dcd61d96b9deb8c159c9ae189153c83400bc9d04cc3ef2&ipo=images "画像タイトル")

</details>

<details><summary>テーブル</summary>

#### 視覚的な記述

```md
| Left align | Right align | Center align |
|:-----------|------------:|:------------:|
| This       | This        | This         |
| column     | column      | column       |
| will       | will        | will         |
| be         | be          | be           |
| left       | right       | center       |
| aligned    | aligned     | aligned      |
```

結果

| Left align | Right align | Center align |
|:-----------|------------:|:------------:|
| This       | This        | This         |
| column     | column      | column       |
| will       | will        | will         |
| be         | be          | be           |
| left       | right       | center       |
| aligned    | aligned     | aligned      |

テーブル内で `|` を使いたい場合は `\|` と入力
<br>

#### HTMLによる記述

```HTML
<table>
    <caption>HTMLの要素</caption>
    <thead>
        <tr>
            <th>名前</th> <th>説明</th>
        </tr>
    </thead>
    <tr>
        <td> table </td> <td>テーブル</td>
    </tr>
    <tr>
        <td> caption </td> <td>テーブルのキャプション</td>
    </tr>
</table>
```

結果
<table>
    <caption>HTMLの要素</caption>
    <thead>
        <tr>
            <th>名前</th> <th>説明</th>
        </tr>
    </thead>
    <tr>
        <td> table </td> <td>テーブル</td>
    </tr>
    <tr>
        <td> caption </td> <td>テーブルのキャプション</td>
    </tr>
</table>

</details>

<details><summary>数式の挿入</summary>

コードブロックに `math` と言語指定して、TeX記法を用いて記述できる
````
```math
\left( \sum_{k=1}^n a_k b_k \right)^{\!\!2} \leq
\left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)
```
````
結果
```math
\left( \sum_{k=1}^n a_k b_k \right)^{\!\!2} \leq
\left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)
```
 `$` で挟むとインライン表示
```
x^2 + y^2 = 1 をインライン表示すると $x^2 + y^2 = 1$ になります。
```
結果
x^2 + y^2 = 1 をインライン表示すると $x^2 + y^2 = 1$ になります。

</details>