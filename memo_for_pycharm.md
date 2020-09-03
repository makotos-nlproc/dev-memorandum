# pycharmに関するメモ

# 新規プロジェクト＋新規仮想環境を作る
- File > NEW PROJECTで新しいプロジェクトを作成
- パスの場所とデフォルトでuntitledになっている部分を任意の名前に変更
- `Project Interpreter: New Virtualenv environment`より仮想環境を設定
- 新規仮想環境作成の場合New、Locationは今回作ったプロジェクト内でOK、Baseも特にいじらない
- Make available to allにチェックを入れておくと別のプロジェクトからその仮想環境を利用可能になる
- 既存の仮想環境を使用する場合はExisting
- 作成完了

# gitの設定をする
- 上部`VCS`から`バージョン管理統合を使用可能にする`から、Gitを選択（おそらく`git init`をしたのと同じ）
- リモートリポジトリを設定する（プッシュ先）
  - githubやその他gitリモートリポジトリホスティングサービス上でリポジトリを新規作成
  - このurlをコピーしてpycharm上右クリック＞Git＞Repository＞Remotesにコピペ