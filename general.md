<details><summary>計算量</summary>

# 1秒で解けるfor文のループ数
1 秒間で処理できる for 文ループの回数は、<br>
 `10^8 = 100,000,000` <br>
回程度

## 工夫してループの入れ子構造を減らそう
```math
a + b + c = X, \\
a \times d1 + b \times d2 + c \times d3 = Y
```
が成り立っているとき、
```c++
for(a:N) 
    for(b:N) 
        for(c:N) {
            if(total == X && combination == Y)
        }
```
としがちだが、実は以下のように2重ループで済む。
```math
a = a', b = b' のとき
c = X - a' - b'\\
```
と一意に定まるので
```c++
for(a:N)
    for(b:N-a)
        c = N - a - b;
        if(total == X && combination == Y)
```

</details>