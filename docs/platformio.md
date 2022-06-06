# Windows PlatformIO導入完全攻略wiki
## これは何
WindowsでPlatformIO導入時にトラブルが頻発しているので、可能な限りの解決法をまとめました。
~~なんでこんな記事が必要なんだ~~

## 「※やり直し」とは
1. PlatformioをVSCodeからアンインストール
1. `~/.platformio` を完全削除(shift+delete)
1. Pathに上記ディレクトリが(あれば)削除
1. PC再起動

## 手順
- インストール前にPython 3を**手動**で入れる
    - Wingetなら `winget install python.python.3`
    - 公式から落としてくるときは `add path to …` にチェックを忘れずに入れる

- その後ローカルアカウントのサインインに必ず切り替える
    - MSアカウントだとインストールできませんでした
    - サインアウトだけすればよい
    - 参考: [これ](https://win11lab.info/win11-local-account-signin/)とか[これ](https://pc-karuma.net/windows10-switch-local-account-from-microsoft-account/)とか

- Platformioをインストールする
    - インストール中に「pythonがない」みたいなダイアログが出たら**その時点で失敗**なので※やり直し

- 新規プロジェクト作成を試みる
    - ここですんなりいけば成功、うまくいかなければ次へ

- プロジェクト作成中にエラー `PIO Core call error` が出る または `Loading…`が無限に終わらない場合
    - 新規プロジェクト作成は諦め、ビルドが通るか確認する
    - [空のプロジェクト](https://github.com/long-paddy-field/test_pio)を`clone`して`code .`
    - ビルドしてみる、ここで通れば成功

- `Rebuilding Intellisense Index…`が終わらない またはビルドボタンを押したときに `pio run command not found`になる
    - VSCodeを落とし、Wi-Fiを切ってからVSCodeを立ち上げ、`Rebuilding…`が終わるのを見てからWi-Fiを入れる

- ビルド中に`toolchain`のダウンロードが進まなくなる
    - `keiomobile2`のプライマリDNSサーバーで名前解決に失敗してるっぽい？(推測)
    - テザリング接続にする

- ビルドが通れば、プロジェクトの新規作成を試みる
    - これで万が一プロジェクトが作れなくても、ビルド成功したプロジェクトを複製すればよい

- ビルドは通るがプロジェクトは作れない場合
    - `pio cli`でプロジェクトを作ってみる
    - `~/.platformio/penv/Scripts/`を`PATH`に追加
    - 適当なディレクトリに移動
    - `pio project init`
    - `code .`
    - `platformio.ini`を書き換える
    - `pio run`

- `pio cli`をアップデートしてみる
    - `./pio upgrade`

- ビルドも通らないし、プロジェクトも作れない場合
    - VSCodeをアンインストールし、ユーザーインストーラーではなく全体インストーラーでインストールしなおす
    - pioも ※やり直し する
    - 最悪、新規でローカルアカウントをセットアップして全部 ※やり直し

- それでもダメ
    - 諦める
