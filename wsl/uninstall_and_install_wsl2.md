# wsl2をアンインストールしてまたインストールした 11/30/24

## wslが入っているか確認する
1.  `Windows PowerShell` を管理者として実行
2. `wsl -l -v` と入力し、Linuxの状態を確認
    1. (pro8) Ubuntuが入っていることを確認できた `Ubuntu Stopped`
    * `wsl --shutdown` と入力し、一応Linuxを停止
    * `wsl --unregister ubuntu` と入力し、Ubuntuの登録解除
    * 最後に一応、設定のアプリから `Ubuntu` がアンインストールされていることを確認
    
    2. (desktop) ディストリビューションがインストールされています
    * 以下の３機能を一度無効化
    * _仮想マシンプラットフォーム_
    * _Linux用Windowsサブシステム_
    * _Windowsハイパーバイザープラットフォーム_
    * `dism.exe /online /disable-feature /featurename:VirtualMachinePlatform /norestart`
    * `dism.exe /online /disable-feature /featurename:Microsoft-Windows-Subsystem-Linux /norestart`
    * `dism.exe /online /disable-feature /featurename:HypervisorPlatform /norestart`
    * 再起動
    * `Restart-Computer -Force` 
    * 上記の3機能を有効化
    * `dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`
    * `dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`
    * `dism.exe /online /enable-feature /featurename:HypervisorPlatform /all /norestart`
    * 再起動
    * `Restart-Computer -Force`

## wslのインストール
1. `wsl --install`
2. 再起動

## Ubuntuのインストール
1. `wsl --install -d Ubuntu`
2. 再起動

## Ubuntuの初期設定
1. 必要な場合はusrnameとpasswdを設定
2. Ubuntuのパッケージリストの更新
    > sudo apt-get update
3. パッケージのインストール
    > sudo apt-get install パッケージ名<br>
    > sudo apt-get install build-essential gdb python-is-python3<br>
    > 何か聞かれたら `y` 
4. インストールの確認
    > whereis ファイル名