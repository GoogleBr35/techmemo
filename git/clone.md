# リポジトリのクローン
1. クローンしたリポジトリを入れたいディレクトリの1つ上に移動
2. GitHubでリポジトリのURLをコピー
3. ターミナルで `git clone url` と入力

今いるディレクトリの中にクローン元のリポジトリがそのまま作られる<br>
例
```
/projects$ git clone url_of_ETC
/projects$ ls
ETC
-> ETCの中に `.git` が含まれており、クローンが完了
```