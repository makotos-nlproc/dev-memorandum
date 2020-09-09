# 雑記メモ

# winサービスにフォルダ作成のスクリプトを登録する
- python　コードを書く
- winサービスに登録して常駐化（適切な表現化不明？）
- その登録した機能を使用したい最はそのAPIを叩く
- HeinsenからそのAPIを叩けるようにすれば、OK?

# git わすれるので定期的に以下を読む
- [git pro](https://git-scm.com/book/en/v2)

# ファイルをいちいち保存しないでweb app上からクライアント側へ送り出したかった
- 自分がpythonでエクセル操作をする際はサードパーティ製のpandasで読み込み、データフレームというオブジェクトで操作、書き出しくらいだった
- pandasはセルの大きさ等、xlsxに対する細かい処理が弱い
- 定型のエクセルがあり、それを読み込んで記入→新規ファイルとしたい場合なのでopenpyxlを使用することにした
- 最初は一時的にxlsxのファイルをheinesen上に作り、ダウンロードまでさせたら消す処理を書こうとした
- が、一般的なweb appではいちいちファイル保存はしなさそう（冷静に考えればそう）
- なので、オブジェクトのまま何とかできないか考える方針へ
- pythonにtempfileモジュールがあり、こちらも考えるがLocal/Application/Temp的な感じでテンポファイルを作るのでサーバー上での動きが想像できず断念
- [bottleでCSVファイルをダウンロードさせるときにつまづいたところ](https://create-fecundity.com/programming/bottle-csv-download-stumbled/)
- の記事を見つけ、これがpandasのdfオブジェクトをcsvに変換したオブジェクトをHTTPResponceのボディとしていたので、これをopenpyxlのWookbookオブジェクトできないか調べた
- すると、プログラム上でファイルっぽいオブジェクトをfile likeオブジェクトやストリーム？として扱うのがweb開発の共通の考え方があるようなので、それを手掛かりに調べると
- [saving-openpyxl-file-via-text-and-filestream](https://stackoverflow.com/questions/8469665/saving-openpyxl-file-via-text-and-filestream)
- [django-openpyxl-saving-workbook-as-attachment](https://stackoverflow.com/questions/16016039/django-openpyxl-saving-workbook-as-attachment)
- がみつかった
- ストリーム処理（一時的に出力内容を貯める？はc++のcoutとかでうっすら聞いたような記憶があるのでそのうち、、、）→key web開発　ストリームなど
- 

# bat
- windows上のコマンドをファイルにまとめておける
- ダブルクリックで実行できるのでめんどくさい環境準備がいらない
- 以下のようなバッチ
  - ファイルの一括リネーム
  - 特定のフォルダ・ファイルを削除する
  - 特定のフォルダ単位でZip化、名前をもとのフォルダ名にする
  - など  

# vimとGvim
- https://vim-jp.org/vim-users-jp/2010/06/05/Hack-152.html
- GUIのvimとかと思っておけば良さそう？
- Gvimの方が便利そうだけど制約も多そうな印象

- https://knowledge.sakura.ad.jp/23018/
- ターミナルとして使うのからなれるのは良さそう

# [名前解決](https://ja.wikipedia.org/wiki/%E5%90%8D%E5%89%8D%E8%A7%A3%E6%B1%BA#%E3%83%8D%E3%83%83%E3%83%88%E3%83%AF%E3%83%BC%E3%82%AF%E3%81%AB%E3%81%8A%E3%81%91%E3%82%8B%E5%90%8D%E5%89%8D%E8%A7%A3%E6%B1%BA)

# FastAPIが使えそう

# windowsサービス
- services（サービス）＝＝常駐プログラムの管理ツール
- 常駐プログラム：windowsマシンが稼働中にバックグラウンドで動きつづけるプログラム
  - e.g. セキュリティのプログラムとか
  - 

# pycharmでPJ作成・環境整備後、gitの設定をする

- pycharm上部VCSから`バージョン管理統合を使用可能にする`を選ぶ
- Gitを選択する
- リモートリポジトリに登録する
- gitbucketやgithub上で空のリポジトリを作成する（pycharm上から作る方法もあるようなのでそのうち調べる
  -  gitbucketではログインした状態で、右上の`+`マークを押す
  -  new repository
  -  repo nameを決める（pycharm上のpj名とそろえるのが良い
  -  create an empty repoにチェックが入った状態で`create repository`
  -  ここでurlをコピー
- pycharmに戻って、右クリック＞Git＞Repository＞Remotes
- 上記のurlを登録する

これで設定ができたのでコミットしてプッシュ

# 読んだもの

- [品質リスクを考慮した機械翻訳の訳文配信.pdf](/attachment/5dfaedda33dcac0042ecf994)
  - 従来の機械翻訳はn個の訳文を生成、基準に従いランク付け、1位を訳文として採用
  - 2位以下に翻訳の品質が良い場合もある
  - そこで「品質リスク」（＝翻訳品質の不確実性）を用いて、2位以下も再検討する（あるいは提示する）
  - 

# pythonでテスト駆動開発

- [Python 3 標準の unittest でテストを書く際のディレクトリ構成](https://qiita.com/hoto17296/items/fa0166728177e676cd36)
  - > Python では実行されたファイルのディレクトリがトップレベルの階層として扱われるため、それより上の階層に遡ってパッケージのファイルを import することができず、エラーになってしまう。
  - パスをちゃんと通すか、テストに限って言えばコマンドを使える

# 前処理
- [【Python】画像から文字起こししてテキストに変換する方法（tesseract-OCR、pyocr）](https://punhundon-lifeshift.com/tesseract_ocr)
  - >tesseract-OCRはオープンソースです。誰でも使うことができます。さらに、tesseract-OCRは画像のアップロードが不要です。一旦、ソフトウェアをインストールすれば、あとは自分のPC内で処理を完結できます。

# Javaが気になる
- [Javaいまでは古臭いと見なされることが多い気がするけど](https://twitter.com/fushiroyama/status/1189350182942584832)
- [コンピュータシステムの理論と実装 ―モダンなコンピュータの作り方](https://www.oreilly.co.jp/books/9784873117126/)

# APIを切る、叩く関連

APIのテスト
- [REST API のテストにcurlとか使ってる？便利なのあるよ](https://qiita.com/yokurin/items/8f5bc0b41f6dd3d13fed)
- [Chrome を REST Client にする拡張機能 Restlet Client - REST API Testing](https://loumo.jp/wp/archive/20180125120021/)
- [JSON/REST APIの簡易テスト方法](https://qiita.com/tomotagwork/items/f723e07d9f11e7475a23)
- [全ての開発者に知って欲しい5つの業務効率化ツール](https://qiita.com/baby-degu/items/2c194fb05049d3b1a7f9?utm_source=Qiita%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=41b48e0dbb-Qiita_newsletter_385_10_30_2019&utm_medium=email&utm_term=0_e44feaa081-41b48e0dbb-35122377)
  - APIのテストにInsomniaが使えそう。
- [BottleでWeb APIを作成する](https://kapibara-sos.net/archives/25)
- [bottleでJSONを返す](http://shuzo-kino.hateblo.jp/entry/2016/09/27/234605)
- [リクエストのJSONデータを受け取る - Bottle](https://tmg0525.hatenadiary.jp/entry/2017/08/20/131859)
- [Python+BottleでToDoアプリを作ってみた](https://qiita.com/shogo0525/items/cb4939c0a91f549d8b77)

# ログイン管理
- [4歳娘「パパ、セッションとCookieってなあに？」](https://qiita.com/Yametaro/items/9b65a21940e001554719?utm_source=Qiita%E3%83%8B%E3%83%A5%E3%83%BC%E3%82%B9&utm_campaign=41b48e0dbb-Qiita_newsletter_385_10_30_2019&utm_medium=email&utm_term=0_e44feaa081-41b48e0dbb-35122377)

# 型
- [すごいHaskell、ハスケル子と学ぼう！ - Qiita](https://qiita.com/Yametaro/items/d12ec13de82d221702de)

# pythonのデコレータ
- [Pythonのデコレータを理解するための12Step](https://qiita.com/_rdtr/items/d3bc1a8d4b7eb375c368)

# Pycharmでコーディングする
## 仮想環境構築
- File > NEW PROJECTで新しいプロジェクトを作る
- 紐付いたディレトリを作ってくれるので、パスの場所とデフォルトでuntitledになっている部分をリネームする
- \>Project Interpreter: New Virtualenv environmentで仮想環境を設定する
- 新しく作る場合Newの方、LocationはプロジェクトでOK、Baseも特にいじらない、Make available to allにチェックを入れておくと別のプロジェクトからその仮想環境を利用できる
- 既に作ってある仮想環境を選ぶ場合はExistingの方
- 作成完了

- 上記でjupyter環境を作るとカーネルエラーになってつらい、**<span style="color: red; ">助けて、、、 </span>**

# パッケージ管理
- プロジェクトの設定からインストール、アンインストールできる
- 下部のターミナルで仮想環境が動いていることを念のため確認（プロジェクト名）が先頭に出る
- `pip list`でパッケージ一覧確認、インストール・アンインストールも同様。

# Bottleをやる
- pipで入れる方法もある
- 同階層に生のbottle.pyを置くのが楽
- 上記のプロジェクト内で問題ない

- [Bottleでファイルを分割する方法](https://doitu.info/blog/5ac362762e280f0095116f10)
- [Webアプリのセッション管理とデータ保存を学ぶ#1（社内勉強会)](https://techracho.bpsinc.jp/hachi8833/2018_09_19/61260)
- [Python3 Bottleフレームワーク入門（その５）- Cookie And Session](https://www.netmarvs.com/archives/869)
- [デコレータを用いた bottle.py のアクセスコントロール](http://www.shido.info/py/bottle_session.html)

# virtualenvwrapper
virtualenvのラッパーのvirtualenvwraperを使いたい
→virtualenvwrapperの初期設定でcourceコマンドを使う
(sourceコマンドはLinuxやMacにおいて、ファイルに書かれたコマンドを現在のシェルに反映させるコマンド。主にしゃえるの設定ファイルを反映させる際に使う。)
→windowsで使用できない
→#2に書いた手順でやるとsourceコマンドのくだりは必要なさそう？

思えばvirtualenvwrapperに固執する理由はなく、社内Wikiで見かけたという動機（去年の5月ごろに書かれたものらしい）

# virtualenvwrapperを（無理やり）使ってみる
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


仮想環境を削除するには、そのフォルダを削除するでOK

