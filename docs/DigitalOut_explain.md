←　[第０話](./intro.md)　｜　第２話　→

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

## DigitalOutでLEDを点灯させよう
　一番初めのプログラムとして、マイコン上に搭載されているLEDを光らせてみましょう。
以下のようなプログラムを作成します。
``` cpp
#include <mbed.h>

DigitalOut myled(LED1);

int main() {
  // put your setup code here, to run once:
  myled.write(1);
  wait_us(1000000);
  myled.write(0);
  while(1) {
    // put your main code here, to run repeatedly:
  
  }
}
```
出来上がったら、ビルドして書き込みましょう。
下の画像のようにUSB経由でPCにつなぎます。
<div style="text-align: center;">
<image src = "./img/DO_img1.jpg" alt = "Prj_intro" title = "Prj_intro" width = "100" height = "150"/>
</div>
ビルドボタンと書き込みボタンは下画像の位置にあります。
<div style="text-align: center;">
<image src = "./img/kakikomi.png" alt = "Prj_intro" title = "Prj_intro" width = "400" height = "270"/>
</div>

プログラムが正常に実行されると、下の画像のように緑色のLEDが1 秒間点灯するはずです。
<div style="text-align: center;">
<image src = "./img/DO_img2.jpg" alt = "Prj_intro" title = "Prj_intro" width = "100" height = "150"/>
</div>

## 解説：DigitalOut
先ほどのコードを一行ずつ解説していきます。※main関数とかは省略します。
### include文
``` cpp
#include <mbed.h>
```
mbedのライブラリを使えるようにincludeしています。
**ライブラリとは、便利なプログラムの集まりのようなもの**です。mbed.hをincludeすることで、マイコンプログラミングに必要となるクラスを使えるようになります。

### DigitalOut のインスタンス化
``` cpp
DigitalOut myled(LED1);
```
**DigitalOutクラスのインスタンス**を作成しています。この説明でピンと来ない人はクラスの復習をしましょう。
DigitalOutは、Arm社（mbedを作った会社）が提供しているmbedライブラリの中のクラスの一つで、名前の通り**デジタル出力を司る**クラスです。要するに、**ピンから電圧をかけるか、かけないかを管理するクラス**だと思ってください。これによってLEDを点滅させたり、ブザーを鳴らしたりできます。

```
DigitalOut　インスタンスの名前（ピンの名前）
```
の形式でインスタンスを作成します。ピンの名前は、[マイコンのピン配置の図](https://os.mbed.com/platforms/ST-Nucleo-F303K8/)を参考にしてください。`PX_N`(`PA_6`等)と書いてある水色の四角に囲まれたものがピンの名前です[^3]。

### 出力
``` cpp
myled.write(1);
```
このコードで先ほど指定したピンへ電圧をかけます。マイコン内部でピンと3.3 Vの線が接続され、電気が流れる仕組みです。逆に
``` cpp
myled.write(0);
```
でピンとGNDが接続され、電圧をかけない状態にすることもできます。

ちなみに、
``` cpp
myled = 1;
```
``` cpp
myled = 0;
```
と書いても正常に動作します。なぜOKなのかは発展的な内容なのでこの記事では扱いません。気になる人は「オペレーター指定子」で検索してください。

### 待機
``` cpp
wait_us(1000000);
```
この行で処理を一定時間経つまで次の処理への移行を待つことができます。`wait_us`のusはマイクロ秒の意味です。このコードによって、LEDが点灯した後、その下のLED消灯のコードの処理に移るのを1秒間遅らせることができます。<br/>
ちなみに、ナノ秒単位で指定できる`wait_ns(ナノ秒)`もあります。**ミリ秒単位で指定できる関数はmbedOS6以降消滅したので存在しません**。欲しくなったら自作してください。

## 練習問題
先ほどのプログラムを改造して、マイコン上のLEDが1 秒周期で点滅するプログラムを作成してください。

<details><summary>プログラミング例</summary><div>

``` cpp
#include <mbed.h>

DigitalOut myled(LED1);

int main() {
  // put your setup code here, to run once:
  while(1) {
    // put your main code here, to run repeatedly:
    myled.write(1);
    wait_us(500000);
    myled.write(0);
    wait_us(500000);    
  }
}
```
点滅のような繰り返しのある処理は、**ループ処理**を使えばいいのでしたね。今回は無限に点滅させたいので、`while`分を使うと手っ取り早いです。点滅周期が1 秒なので、0.5 秒毎に点灯と消灯を交互に繰り返せばよいでしょう。
</div></details>

以上、DigitalOutについて要点だけ説明しました。さらに詳しく知りたい人は[こちら](https://os.mbed.com/docs/mbed-os/v6.15/apis/digitalout.html)からリファレンスマニュアル[^2]を読んでください。

[^1]: PlatformIOは**日本語を含むアドレスにアクセスできない**ので、"C:\Users\username\Onedrive\ドキュメント"みたいな場所にファイルを作るとうまく実行できない場合があります。
[^2]: リファレンスマニュアル（または「リファレンス」）とは、そのクラスの情報を纏めたもので、要するに辞書のようなものです。mbedには英語版（公式）と日本語版（非公式）があります。
[^3]: マイコンボード上のLEDには、"LED1"等がピン名の代わりに割り振られているので、今回の例ではそれを用いています。

←　[第０話](./intro.md)　｜　第２話　→