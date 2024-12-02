# 自動補完機能があまり動いていなかったので設定する

 `#incl` とかを書いても補完されないので、`c_cpp_propertiees.json` のincludePathを編集する

1.  `/.vscode/c_cpp_properties.json` を開く
2.  初期状態
    ```
    {
        "configurations": [
            {
                "name": "Linux",
                "includePath": [
                    "${workspaceFolder}/**"
                ],
                "defines": [],
                "compilerPath": "/usr/bin/gcc",
                "cStandard": "c17",
                "cppStandard": "gnu++17",
                "intelliSenseMode": "linux-gcc-x64"
            }
        ],
        "version": 4
    }
    ```
3. 以下のように設定
    ```
        {
        "configurations": [
            {
                "name": "Linux",
                "includePath": [
                    "${workspaceFolder}/**",
                    "/usr/include/x86_64-linux-gnu"
                ],
                "defines": [
                    "_DEBUG",
                    "UNICODE",
                    "_UNICODE"
                ],
                "compilerPath": "/usr/bin/gcc",
                "cStandard": "c17",
                "cppStandard": "gnu++17",
                "intelliSenseMode": "linux-gcc-x64"
            }
        ],
        "version": 4
    }
    ```
    includePath には、include したいファイルがあるフォルダを適宜追加