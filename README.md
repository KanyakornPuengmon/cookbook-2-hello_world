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


## สรุปผลการทดลอง
