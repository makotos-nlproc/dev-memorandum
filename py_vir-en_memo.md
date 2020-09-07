# 1　virtualenvwrapper
virtualenvのラッパーのvirtualenvwraperを使いたい
→virtualenvwrapperの初期設定でcourceコマンドを使う
(sourceコマンドはLinuxやMacにおいて、ファイルに書かれたコマンドを現在のシェルに反映させるコマンド。主にしゃえるの設定ファイルを反映させる際に使う。)
→windowsで使用できない
→#2に書いた手順でやるとsourceコマンドのくだりは必要なさそう？

思えばvirtualenvwrapperに固執する理由はなく、社内Wikiで見かけたという動機（去年の5月ごろに書かれたものらしい）
（ちなみにこれ：[virtualenvによる仮想環境構築とWebアプリの勉強メモ]()


# 2　virtualenvwrapperを（無理やり）使ってみる
（無理やり）：sourceコマンドのくだりを無視して取り合えずvirtualenvwrapper-winだけして動くようなので。

- pythonのインストール
- pip install virtualenvwrapper-win
- mkvirtualenv env_name
→これでenv_nameの仮想環境が作成され有効化（activate）された状態になる
→(env_name)が目印
- deactivateで無効化
- workon env_nameで有効化
- workonで環境リストの表示

- mkvirtualenv --no-site-package env_nameでまっさらな状態の環境が作れる
- cdvirtualenvで仮想環境のディレクトリに移動


pip freezeインストール済みのパッケージ一覧を確認できる
（pip listはより詳しい。違いはググりましょう。）
→環境を「フリーズ」（固定）するためにfreeze > requirements.txtである環境のパッケージリストとそのバージョンを記録したテキストファイルが作成できる
→pip install -r requirements.txtでその環境を再現できる（上で記録したテキストを読み込んでる）

参照
- [仮想環境](https://python-guideja.readthedocs.io/ja/latest/dev/virtualenvs.html)
→詳しい。途中からvirtualenvwrapper-winについても記述がある。
- [virtualenvでpython環境を管理する](https://qiita.com/caad1229/items/325ca5c8ad198b0ebce7)
→Mac, Ubuntu環境かつざっくりだが、virtualenvwrapper-winでインストールさえしておけば使い方は同じようだ。環境を離れてみるのを試したりするのでわかりやすい。
- [virtualenvwrapper 3.5](https://virtualenvwrapper-docs-ja.readthedocs.io/en/latest/)
→公式のドキュメント。やはりsourceコマンドのくだりが何を逢っているかは機会があれば調べるor 聞くことにする。


仮想環境を削除するには、そのフォルダを削除する



# ３　その他の仮想環境を使ってみる
