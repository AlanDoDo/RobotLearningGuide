LED 灯珠长引脚为正极,短引脚为负极。

```Python
//头文件
#include <Arduino.h>

//定义LED灯引脚为常量，因为程序跑起来就不需要更改IO值
#define PIN_LED 18

void setup() {
  //初始化引脚为输出
  pinMode(PIN_LED, OUTPUT);
}

void loop() {
    //设置为高电平（3.3V），1s后设置为低电平（0V），再1s后重复
    digitalWrite(PIN_LED, HIGH);
    delay(1000);
    digitalWrite(PIN_LED, LOW);
    delay(1000);
}

//学习编程最重要的是动手动手再动手，一定要跟着写代码，哪怕你已经看懂了
```