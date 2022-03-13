# プロジェクトを作ろう/DigitalOutでLチカしよう
[前回の記事](./intro.md)で環境構築が終わったので、さっそくプロジェクトを作ってプログラミングをしてみましょう。今回はマイコンとしてNucleo F303K8を使用します。

## プロジェクトの作り方
1. 画面左側のツールバーのPlatformIOのアイコンを押す。
2. `PIO Home`下の`Open`を押す。
3. `New Project`を押す。
<div style="text-align: center;">
<image src = "./img/Prj_intro1.png" alt = "Prj_intro" title = "Prj_intro" width = "400" height = "200"/>
</div>

4. `Name`に適当なプロジェクト名（**必ず英数字**）を入力する。
5. `Board`に使用するマイコンボードを入力する。"F303"と打ち込むと、"ST Nucleo F303K8"とサジェストが出るのでそれを選ぶ。
6. `Framework`には"mbed"を入力する。Arduinoで作りたくなったら"Arduino"と入力すればよい（今回はmbedを解説する）
<div style="text-align: center;">
<image src = "./img/Prj_intro2.png" alt = "Prj_intro" title = "Prj_intro" width = "400" height = "200"/>
</div>

7. `Location`を設定する。デフォルトは**非推奨**[^1]。デスクトップに適当なフォルダを自作してそこにプロジェクトを作りましょう。
<div style="text-align: center;">
<image src = "./img/Prj_intro3.png" alt = "Prj_intro" title = "Prj_intro" width = "400" height = "200"/>
</div>

8. 全部の設定が終わったら、`Finish`を押してプロジェクトを作りましょう。そこそこ時間がかかります。
9. 完了すると下の画像のような画面が表示されます。
<div style="text-align: center;">
<image src = "./img/Prj_intro4.png" alt = "Prj_intro" title = "Prj_intro" width = "400" height = "200"/>
</div>

## DigitalOutでLチカさせよう
一番初めのプログラムとして、マイコン上に搭載されているLEDを光らせてみましょう。
``` Lesson1_DigitalOut.cpp

```

[^1]: PlatformIOは**日本語を含むアドレスにアクセスできない**ので、"C:\Users\username\Onedrive\ドキュメント"みたいな場所にファイルを作るとうまく実行できない場合があります。