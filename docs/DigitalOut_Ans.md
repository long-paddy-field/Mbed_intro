# 解答例
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
