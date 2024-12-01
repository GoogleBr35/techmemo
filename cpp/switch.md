### エラーの原因？
各caseは `{` `}` で囲んであげるとエラーを吐かない場合がある。
```c++
switch(x) {
    case a: {
        ...
        break;
    } case b: {
        ...
        break;
    } default: {
        ...
    }
}
```