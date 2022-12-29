# README

## 環境構築
```
$ bundle install
$ bin/rails db:setup
$ yarn install
$ bin/rails s
```

## 事業をエンジニアリングしよう提案編の回答は以下に記述してください
# 選択した事業側の課題
サービス登録者数の内、男性60%に対して、女性は40%。一方で、サービス内のもくもく会に参加した人の比率は、男性90%：女性10%と大きな差が出ています。
もっと女性が使いやすいようなサービス設計にする必要があるのではないか？

# 提案内容
ユーザー情報に性別と年齢を加える
もくもく会の参加者の性別を見えるように設定 & 女性限定、募集年齢に制限をしたもくもく会ができるようにする
もくもく会の画像アップロード機能を加える

→ 現状もくもく会は参加者の身元がわかりづらく、同性の方はいるのか？や同世代の方はいるのか？などの参加する前に不安を感じると考えられる。
  参加するハードルを下げるため、同性や同年代と選択的に繋がれる仕組みを作る。
  もくもく会のイメージを膨らませるようにイメージ写真を付けられるようにする。過去開催した時の写真などを上げられるようにする。

# 実装方針
DBのuserテーブルに性別と年齢を加える。初期値は不明にして公開したくない人も考慮する。
もくもく会の主催者、参加者の性別ごとに名前の色を変える。直接書くのはどうかなと思うため、女性は赤、男性は青、不明は黒のようにしてUIで表記。
もくもく会の作成時に女性限定募集をできるようにする（作成できるのも女性のみ）。
もくもく会の作成時に募集年齢を指定できるようにする（作成者が年齢制限外であれば作成できないようにする）。
もくもく会の画像アップロード機能を加える。表示位置は、"event-default-image.png"が表示されている部分。画像がアップロードされなかった場合のデフォルトは現状の画像。

## 事業をエンジニアリングしよう実装編
# 実装方針
[x]  ユーザー登録時に手入力やチェックボックス入力ではなく、セレクト形式で性別登録できる。
[x]  イベント作成画面にOnly womanのチェックボックスにチェックを入れるだけで女性限定イベントを作成できる。
[x]  ユーザーが女性以外の場合、イベント作成時にOnly womanは表示されず、女性限定イベントが作成できない。
[x]  女性限定イベントには女性のみが参加できる。
[x]  女性以外の場合、女性限定イベントの詳細ページを開いた際に「このもくもく会に参加する」が表示されない。
[x]  女性限定イベントは一覧・詳細画面にて「女性限定」が表記される。

# 注意点
[x]  イベントが女性限定であるかを判定するカラムは"only_woman"とする
[x]  ユーザーの性別登録のカラムは"gender"とする
[x]  ユーザー登録時の性別のセレクト部分はenumを使って「その他・男性・女性」が表示される（その際に特に操作が無かれば"その他"が選択される）

# Gemfile
Testグループに以下のgemを追加
- gem 'capybara', '~> 3.23'
- gem 'selenium-webdriver'
- gem "webdrivers" 