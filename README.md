# แนวทางการทำงาน Hello World Example

## การเลือก Example IDF

![image](https://github.com/user-attachments/assets/71ccc1dd-9895-476a-a121-52626292d12b)

1. เลือก ESP-IDF

2. เลือก show example

3. เลือก hello_world

![สกรีนช็อต 2024-10-29 225559](https://github.com/user-attachments/assets/59f78a45-4eec-46da-8118-34861d4b4db2)

5. คลิกเลือก Create project using example hello_world

6. เมื่อสร้างแล้วจะได้ไฟล์ทั้งหมดดังนี้

![สกรีนช็อต 2024-10-29 225615](https://github.com/user-attachments/assets/6ecfce95-cc31-4852-bf60-3d1d8eb820dc)

## Build and Flash

7. เลือก com port

8. เลือก Build Flash and Monitor

## ผลลัพท์

- Serial Moniter แสดงดังนี้
  
จะแสดงข้อความ Hello World และ restart ทุกๆ 1 วินาที

![image](https://github.com/user-attachments/assets/1867c04e-70ba-4a99-99dc-6a39e89996a5)

https://drive.google.com/file/d/1eDD9pm7NwLE3vpSs0VemYqX635si4KWS/view


## การแก้ไข

9. เลือกไฟล์ main.c เพื่อแก้ไข
   
- สามารถเปลี่ยนข้อความที่แสดงผลได้ตามต้องการจากบรรทัดที่ 18

![สกรีนช็อต 2024-10-29 232504](https://github.com/user-attachments/assets/958d6e6e-e63d-44d1-8fb0-d7b115c8d13c)

### ตัวอย่าง

```
printf("Welcome to my ESP32 program!\n");
```

- สามารถเปลี่ยนความเร็วในการแสดงผลได้ในบรรทัดที่ 47
  
![สกรีนช็อต 2024-10-29 232516](https://github.com/user-attachments/assets/8c82667a-fdb4-4ad6-b251-71dafa256094)

### ตัวอย่าง

```
for (int i = 10; i >= 0; i--) {
    printf("Restarting in %d seconds...\n", i);
    vTaskDelay(500 / portTICK_PERIOD_MS); // เปลี่ยน 1000 เป็น 500
}

```
## ผลลัพท์หลังจากแก้ไข

- แสดงข้อความบน Serial Moniter Welcome to my ESP32 program! และ restart ทุกๆ 0.5 วินาที

  ![image](https://github.com/user-attachments/assets/ba2199c3-90c9-4570-a962-7e95facf69b2)

https://drive.google.com/file/d/1_N9FbyJzZUgmrFnPGaOdk6oHDQRatUSq/view



## ตัวอย่างโค้ดที่แก้ไข

```

#include <stdio.h>
#include <inttypes.h>
#include "sdkconfig.h"
#include "freertos/FreeRTOS.h"
#include "freertos/task.h"
#include "esp_chip_info.h"
#include "esp_flash.h"
#include "esp_system.h"

void app_main(void)
{
    printf("Welcome to my ESP32 program!\n");

    / Print chip information /
    esp_chip_info_t chip_info;
    uint32_t flash_size;
    esp_chip_info(&chip_info);
    printf("This is %s chip with %d CPU core(s), %s%s%s%s, ",
           CONFIG_IDF_TARGET,
           chip_info.cores,
           (chip_info.features & CHIP_FEATURE_WIFI_BGN) ? "WiFi/" : "",
           (chip_info.features & CHIP_FEATURE_BT) ? "BT" : "",
           (chip_info.features & CHIP_FEATURE_BLE) ? "BLE" : "",
           (chip_info.features & CHIP_FEATURE_IEEE802154) ? ", 802.15.4 (Zigbee/Thread)" : "");

    unsigned major_rev = chip_info.revision / 100;
    unsigned minor_rev = chip_info.revision % 100;
    printf("silicon revision v%d.%d, ", major_rev, minor_rev);
    if(esp_flash_get_size(NULL, &flash_size) != ESP_OK) {
        printf("Get flash size failed");
        return;
    }

    printf("%" PRIu32 "MB %s flash\n", flash_size / (uint32_t)(1024 1024),
           (chip_info.features & CHIP_FEATURE_EMB_FLASH) ? "embedded" : "external");

    printf("Minimum free heap size: %" PRIu32 " bytes\n", esp_get_minimum_free_heap_size());

   for (int i = 10; i >= 0; i--) {
    printf("Restarting in %d seconds...\n", i);
    vTaskDelay(500 / portTICK_PERIOD_MS); // เปลี่ยน 1000 เป็น 500
}

    printf("Restarting now.\n");
    fflush(stdout);
    esp_restart();
}
﻿
```

## สรุปผลการทดลอง
- การทดลอง Hello World Example บน ESP32 เป็นขั้นพื้นฐานที่ช่วยให้เราเข้าใจการเชื่อมต่อและการเขียนโค้ดเบื้องต้นบนบอร์ด ESP32 ได้ดี เมื่ออัปโหลดโค้ดสำเร็จ และเปิด Serial Monitor จะเห็นข้อความ "Hello, World!" ถูกพิมพ์ออกมาตามที่ตั้งไว้ในโปรแกรม ซึ่งแสดงว่าการเชื่อมต่อและการอัปโหลดโค้ดทำงานได้อย่างถูกต้อง ถ้ามีความต้องการจะเปลี่ยนแปลงข้อความหรือแก้ไขระยะเวลาในการ restart ก็สามารถที่จะปรับเปลี่ยนได้ตามความต้องการดังตัวอย่างที่ให้มา
