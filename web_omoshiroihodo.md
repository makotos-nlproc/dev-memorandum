
# chap1

virtualboxのインストール
vagrantから利用するのでcustom setupのcreate a shortcut on the desktopのチェックは外す。 インストール後起動もしない。
vagrantのインストール

コマンドプロンプトで
mkdir %USERPROFILE%\vagrant\ubuntu\64_16
cd %USERPROFILE%\vagrant\ubuntu\64_16

Linux仮想環境をインストールするためフォルダを作って移動しただけ。

ubuntuをダウンロード
vagrant box add ubuntu/xenial64 https://vagrantcloud.com/ubuntu/boxes/xenial64/versions/20170929.0.0/providers/virtualbox.box

設定ファイルを作成
vagrantinit ubuntu/xenial64

winのパッケージマネージャchocolateyをインストール
管理者権限で起動したコマンドプロンプトで
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"

PowerShellをアップデート
choco install -y powershell

Linuxの起動
vagrant up

これで起動したubuntuにSSHで接続する
-> SSHクライアントRLoginをインストール

接続するために必要な情報を確認する
vagrant ssh-config

UserとPortを確認してRLoginを起動、新規より
エントリー：vagrant
プロトコル：ssh
Server Adress: localhost
Socket Port: 接続先のPort
User Name: 接続先のUser
SSH Identity Keyは%USERPROFILE%\vagrant\ubuntu\64_16.vagrant\machines\default\virtualbox\private_key
デフォルト文字セット: UTF-8

接続情報の設定が保存されるので次回以降はこれを使う

ubuntuを日本語化する
sudo locale-gen ja_JP.UTF-8
echo export LANG=ja_JP.UTF-8 >> ~/.profile
source ~/.profile

コンソールを閉じる
exit

仮想マシンを終了する
cd %USERPROFILE%vagrant\ubuntu64_16
vagrant halt

## sec03 コマンドによるファイル操作

pwd
ls
ls -a :ドットで始まるファイルもすべて表示
cd
mkdir
rm
rm -r directory_name: ディレクトリの削除
rmdir directory_name: 同
cp
cp -r dirname1 dirname2: 中身も含めて再帰的にコピー
mv dir1 dir2: 1の名前を2へ変更
find
find dir -name filename: dir以下からfilenameをd探す

command man: コマンドのマニュアルを表示

共有フォルダを利用する
cd %USERPROFILE%vagrant\ubuntu64_16
mkdir workspace

エディタで%USERPROFILE%vagrant\ubuntu64_16\Vagrantfileを開く
L47にconfig.vm.synced_folder "./workspace", "/home/vagrant/workspace"
winの場合その下に
config.vm.provider :virtualbox do |vb| vb.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnablesSymlinksCreate//home/vagrant/workspace", "1"]

またL55~61の以下三行#を無くして有効化
config.vm.provider "virtualbox" do |vb|
vm.memory = "1024"
end

これを上書き、設定を反映させるために再起動する
fsutil behavior set SymlinkEValuation L2L:1 R2R:1 L2R:1 R2L:1
cd %USERPROFILE%vagrant\ubuntu64_16
vagrant reload --provision

## sec04 標準出力
標準出力をファイルに書きだすこと->リダイレクト
command > txtfile
>>: ファイルに追記して出力
2>: 標準エラーを出力
2>&1: 標準出力とエラーの両方を出力

Concatenate
ファイルの中身を見る
cat dir以下からfilenameをd探す

パイプ
grepコマンド

## sec05 vi
vim filename
~は何もない行を示す
esc -> :q で閉じる
:q!で破棄
:w 書き込み

### コマンドモードとインサートモード
コマンドモード：カーソル移動、ファイル操作、他モードへ、切り取り貼り付け、繰り返し処理、検索置換など
インサートモード
編集したい部分でIかA
insert or append


チュートリアル
mkdir ~/workspace/vim-study
cd ~/workspace/vim-study
vimtutor


## Chap3 シェル
OSのカーネルを包み込みOSと対話する機能
mkdir workspcae/my-first-shell
cd workspace/my-first-shell
touch my-first.sh

my-first.shをエディタで開く
#!/bin/bash
ls
date
windowsの場合はVSCodeの右下CRLFをLFに設定

#!の行をジバン

ファイルの権限を与えるためubuntuのコンソールで
chmod a+x my-first.sh

./my-first.shで実行

read varで入力待ち

### sec02 通信とネットワーク
