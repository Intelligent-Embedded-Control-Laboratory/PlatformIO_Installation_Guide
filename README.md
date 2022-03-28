# PlatformIO_Installation_Guide

## 一、下載安裝VSC
### Step 1. 下載 Visual Studio Code (VSC)
下載網址 https://code.visualstudio.com/

![1](https://user-images.githubusercontent.com/96014379/160340055-64dd95fc-2cb9-49b0-a621-4199330ad9a6.png)

記得其他內的選項全部都要打勾

![2](https://user-images.githubusercontent.com/96014379/160340739-af78be16-45ce-4656-8c2e-e1d5a4fa2a9e.png)

安裝畫面

![3](https://user-images.githubusercontent.com/96014379/160340811-0e8113e9-64ff-462f-afeb-91c64376a010.png)

### Step 2. 第一次啟動時，可能會推薦安裝中文語言包；或進入延伸模組，搜尋 chinese 手動安裝繁體中文語言包。

![4](https://user-images.githubusercontent.com/96014379/160340955-fd8c5dcd-820a-465f-90aa-98ecab96b494.png)

## 二、加入 PlatformIO
### Step 1. 進入延伸模組，搜尋 "PlatformIO" 手動安裝

![5](https://user-images.githubusercontent.com/96014379/160341108-7b136a10-14b9-43d8-bbfb-15b7084cb85e.png)

### Step 2. 安裝完後重新啟動 VSC，左側會出現 PlatformIO 的圖示。

![6](https://user-images.githubusercontent.com/96014379/160341179-1de648c4-535b-4add-a23d-a5e7193f39b3.png)

## 三、安裝Platform
開發版除了預設的板子(nano,uno)可以直接上傳程式，其他都要先安裝Platform (類似開發版環境)

  * Teensy->裝Teensy
  * ESP32->裝Espressif32
  * ESP8266->裝Espressif 8266

詳細安裝步驟參考下文

以ESP32為例:
### Step 1. 進入platformIO >> PIO HOME >> Open >> Platform

![7](https://user-images.githubusercontent.com/96014379/160341362-f076551b-f678-47d2-b053-ede283665a90.png)

### Step 2. 選擇Embedded，搜尋”espressif”，進入Espressif32。

![8](https://user-images.githubusercontent.com/96014379/160341431-cc72c25c-9be8-40d6-b209-bb20e12809cc.png)

### Step 3. 安裝，需耗時 5~10 分鐘。
![9](https://user-images.githubusercontent.com/96014379/160341472-4ce4dc50-dcaf-415f-9304-6b997b499d44.png)

### Step 4. 安裝完成。

![10](https://user-images.githubusercontent.com/96014379/160341596-02d0bebb-8ec1-4f81-a1ff-bb59e9872141.png)

### Step 5. 同樣方法搜尋 "teensy"，安裝teensy開發環境，Platform >> Installed可以看到安裝的環境 。ESP8266同理。
![11](https://user-images.githubusercontent.com/96014379/160341685-aa665738-46d3-4ede-99f7-e46bd9e2ede8.png)

## 四、開新專案
裝好要燒入板子的Platform，就可以開新專案準備燒入程式

### Step 1. 進入platformIO >> PIO HOME >> Projects，"Creat New Project"

![12](https://user-images.githubusercontent.com/96014379/160341810-91317fa0-633b-41fe-865b-d63782089a1c.png)

### Step 2. 建立專案名稱，及選擇MCU，esp32選擇”NodeMCU-32S”，可直接輸入；儲存位置預設為: (D:\Users\IEC5892M\Documents\PlatformIO\Projects)底下。

![13](https://user-images.githubusercontent.com/96014379/160341889-5cd682db-e25e-47c4-924d-52cacfe5eb5c.png)

補充:
Teensy:Board選對應的4.0選40，3.2選31
ESP32 : Board選NodeMCU-32S
ESP8266:Board 選Espressif Generic ESP8266 ESP-001 1M

取消預設可指定儲存位置。
![14](https://user-images.githubusercontent.com/96014379/160341955-bc70542d-e640-4c5c-bc5e-db120bd9f0ca.png)

### Step 3. 按下 finish 建構專案，重新啟動VSC後建專案可能會花比較多時間 3~10 min都有可能。

## 五、編輯介面說明
1. 編譯器主題設置
於介面右下角：

![51](https://user-images.githubusercontent.com/96014379/160400082-c8574b53-297b-443d-8168-41aa828c553e.png)

中間就會跳出數種選擇

![52](https://user-images.githubusercontent.com/96014379/160400118-064dbec8-8860-497b-9f9e-405cfb066bfd.png)

2. 主程式在 src 資料夾之下，會將演算法寫在 main.cpp

![521](https://user-images.githubusercontent.com/96014379/160402733-034fa4c8-4665-426e-8f90-89ef2afed3f9.png)

以下提供點 LED 燈的範例程式碼

```c=1
#include <Arduino.h>
void setup() 
{
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() 
{
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);
}
```

3. ini檔 (上傳的設定) 參考程式碼
```
; PlatformIO Project Configuration File
;
;   Build options: build flags, source filter
;   Upload options: custom upload port, speed and extra flags
;   Library options: dependencies, extra library storages
;   Advanced options: extra scripting
;
; Please visit documentation for the other options and examples
; https://docs.platformio.org/page/projectconf.html

[platformio]
; default_envs = teensy31      ;Teensy3.2&3.6
; default_envs = teensy40    ;Teensy4.0
default_envs = nodemcu-32s ;ESP32

; 開發環境共同的部分
[env] 
framework = arduino
monitor_speed = 115200 ; 設定序列埠擷取資料的 baud rate(VScode內建的UART顯示baud rate)
lib_extra_dirs = ; 設定本地 library 的絕對路徑 (每台電腦不一樣)
    ; G:\我的雲端硬碟\My Experiment\My_Libs
lib_deps = ;參考後面加入函式庫
    ; martinl1/BMP280_DEV@^1.0.18
    ; bolderflight/Bolder Flight Systems MPU9250@^1.0.2

;以下為各開發板的設定port會根據插入的板子不同而改變
[env:teensy40]
platform = teensy
board = teensy40
upload_port = COM30;上傳的port，參考後面上傳口檢查

[env:teensy31]
platform = teensy
board = teensy31 
upload_port = COM6

[env:nodemcu-32s]
platform = espressif32
board = nodemcu-32s
upload_port = COM4
```

4. 設定程式碼上傳的序列埠
* 確認插入單晶片的傳輸port可以藉由點選外星人->Devices->Refresh->看有哪個COM X是你插上去才有的就是這晶片的port

![53](https://user-images.githubusercontent.com/96014379/160401302-fc9ecf26-5f26-4e8e-b87e-ced20ef74f4a.png)

* 更改ini檔中對應開發板中的upload_port，這裡以ESP32示範，COM4，所以ini檔最下面是COM4，且[platformio]底下留default_envs = nodemcu-32s ;ESP32，另外兩個是註解的狀況(前面提供的程式碼)，按下Ctrl+Alt+U就可以快速上傳，上傳成功終端機會通知，然後你的ESP32上板載LED就會亮一秒暗一秒(藍燈)。
![54](https://user-images.githubusercontent.com/96014379/160401436-c74744e9-800f-40fe-ab30-96495731b456.png)

* 同樣的，這份範例程式碼是Teensy也可以用的，改插上Teensy3.2，此時要更改開發版只要再ini檔前改成tensy31，另兩個註解掉，如下所示。
```c
[platformio]
default_envs = teensy31      ;Teensy3.2&3.6
; default_envs = teensy40    ;Teensy4.0
; default_envs = nodemcu-32s ;ESP32
```

* 然後也要確認後面對應的teensy31中upload_port是正確的(同樣確認方式)
```c
[env:teensy31]
platform = teensy
board = teensy31 
upload_port = COM5
```

* 上傳成功後板載上的小橘燈會開始閃爍
* 快捷鍵補充:
  * 上傳:Ctrl+Alt+U
  * Build(編譯但不上傳): Ctrl+Alt+B
  * 開啟序列埠終端機: Ctrl+Alt+S
  * 離開序列埠終端機:Ctrl+C

5. 加入函式庫
有3種加法
(1) 加在include或lib路徑之下，再於主程式#include " "或<>

![55](https://user-images.githubusercontent.com/96014379/160403160-2bc91a4d-645f-4034-9ecf-3c2129369dfb.png)

如有紅線(移動檔案路徑會重抓會需要一段時間，但一段時間也未消失)則移至紅線處，會顯示偵測到錯誤，選快速修復->新增至…..(lib位址)，即可引入成功

![56](https://user-images.githubusercontent.com/96014379/160402971-32c5fb36-4ae4-4ec0-a87b-69cb80714488.png)

(2) 引入本地函式庫
前面ini檔中lib_extra_dirs =後面輸入函式庫資料夾位址，則整個資料夾內的函式庫都會引入，當然主程式也要#include " "

(3) 藉由 PlatformIO IDE 來搜尋函式庫
platformIO在介面中選Libraries，並搜尋需要的涵式庫

![57](https://user-images.githubusercontent.com/96014379/160403259-91f0c819-e7f9-4679-81b0-74a9c25fa4dc.png)

點選想要的涵式庫，選擇installation，可以直接選取Add to Project，或是將它提供的網址加入ini檔中的lib_deps =即可，加入ini檔好處是此份程式到其他台電腦，會自行下載安裝好(特別說明@^後數字是版本號，不同版本會有些許更動要看作者說明)

![58](https://user-images.githubusercontent.com/96014379/160403402-0bfa88d0-9388-4595-841a-c71fdb09c63a.png)

範例ini檔中取消註解後如下

```
lib_deps = ;參考後面加入函式庫
    martinl1/BMP280_DEV@^1.0.18
    bolderflight/Bolder Flight Systems MPU9250@^1.0.2
```

上傳或Build會自動下載，記得main檔要都include才不會報錯

```
#include <MPU9250.h>
#include <BMP280_DEV.h>
```

它們會存在.pio中開發版的函式庫中，裡面就有examples可以參考如何使用這個 lib

![59-2](https://user-images.githubusercontent.com/96014379/160405321-08899007-d283-4e56-96ea-19883620443f.png)

## 六、VS Code 模組推薦
參考用，裝了能提高你的工作效率

1. Code Spell Checker

功能：檢查拼字有無錯誤

![61](https://user-images.githubusercontent.com/96014379/160343432-2ca307e0-c172-40fd-b22f-0b71775303df.png)

2. TabOut

功能：如果喜歡用tab跳離括號的人可以使用

![62](https://user-images.githubusercontent.com/96014379/160343483-4468d980-0bcc-4df3-90c1-130c0fef5e9b.png)

3. Material Icon Theme

功能：檔案總管各種檔案有各自圖示

![63](https://user-images.githubusercontent.com/96014379/160343623-af788803-87ad-4583-a94c-062d0e36538f.png)

4. Doxygen Documentation Generator

功能：輔助程式註解

![64](https://user-images.githubusercontent.com/96014379/160343860-285ea54e-8a5c-4754-81af-9fb3970ba898.png)

5. Power Mode

功能：打字可以有特效(但要改json檔，要用自己學 by 志嘉)

![65](https://user-images.githubusercontent.com/96014379/160343983-e46cd910-f768-4291-ad14-985d31ee8d93.png)

6. background

功能：可以有賽高的工作環境 by 志嘉
參考json程式碼 (我就幫到這了)
```
// background
    "background.enabled": true,
    "background.useDefault": false,
    "background.customImages": [
        "file:////D:/VSbackground/test.png"
        //圖片地址
        ],
    "background.style": {
    
        "content": "''",
        "pointer-events": "none",
        "position": "absolute",
        "z-index": "99999",
        "width": "100%",
        "height": "100%",
        // "background-position": "center",
        "background-repeat": "no-repeat",
        "background-size": "40%,40%",
        "opacity": 0.15
    },
```

程式執行效果：
![67](https://user-images.githubusercontent.com/96014379/160403990-1cdd823f-ae4f-41f5-b612-664a3242eb9a.png)

