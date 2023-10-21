# Airlevel
> This Airlevel project is part of Computer Programming Project, KMITL Semester 10/2022 2st Year
 ## บทคัดย่อ 📝
> เนื่องจากพบว่าในปัจจุบันมีค่าฝุ่นที่เพิ่มมากขึ้นซึ่งเป็นสาเหตุหนึ่งของโรคที่เกี่ยวข้องกับทางเดินหายใจ โดยมีคนไทยเป็นโรคนี้จำนวนมากติด Top 5 ของโรคที่คนไทยเป็นมากที่สุด
>    
> ผู้จัดทำเห็นถึงปัญหาจึงจัดทำโครงงานชิ้นงาน Air quality notification ที่ใช้ C เป็น Microcontroller โดยเป็นการวัดค่าคุณภาพอากาศของพื้นที่ที่เซ็นเซอร์ตรวจวัดค่าฝุ่นตั้งอยู่  
>
> โดยเรานำความรู้ และทักษะการต่อวงจรจากวิชา Physical Computing มาปรับใช้กับการพัฒนา Microcontroller ตัวนี้ และเพื่อความสะดวกต่อการรับรู้ข้อมูลคุณภาพอากาศ เราจึงทำการแสดงผลของข้อมูลผ่าน notification ของ Application LINE
## วัตถุประสงค์ 
> * เพื่อป้องกันและเฝ้าระวังค่า PM 2.5 และหาทางป้องกันเพื่อไม่ให้กระทบต่อสุขภาพในแต่ละวัน
> * เพื่อนำความรู้ภาษา C มาประยุกต์ใช้ให้เกิดประโยชน์
> * เพื่อเสริมสร้างแหล่งข้อมูลข่าวสารที่สดวกสบายเกี่ยวกับ PM 2.5
> * เพื่ออำนวยความสดวกให้บุคคลทั่วไปสามารถรับข้อมูลได้ง่ายยิ่งขึ้น
## ข้อดี 💚
> * สามารถวัดอุณหภูมิเพื่อใช้ในห้องสำหรับเก็บเซิร์ฟเวอร์หรือเหมืองคริปโต
> * สามารถวัดปริมาณความชื้นเพื่อประกอบการทำกิจการได้ เช่น ถ้าเรารู้ว่าถ้าชื้นเกินก็ยังไม่ควรตากผ้า
> * ใช้งานง่าย เข้าถึงทุกคน และ สะดวกสะบาย
## อุปกรณ์ 🛠
> 1. Breadboard  
> <img src="https://github.com/MadaMun/language_C/assets/94043213/4f984cb9-8093-4ce5-9acf-8c4d924d9c1b" width="200" height="200" /></br> 
> 2. Nodemcu esp8266  
> <img src="https://github.com/MadaMun/language_C/assets/94043213/7a771aa4-5dcf-404d-b279-35bdd114d90d" width="200" height="200" /></br> 
> 3. sharp gp2y1010au0f dust sensor  
> <img src="https://github.com/MadaMun/language_C/assets/94043213/27dc01a0-2a05-4140-9624-31254541cdd0" width="200" height="200" /></br> 
> 4. สายไฟจั้มเปอร์  
> <img src="https://github.com/MadaMun/language_C/assets/94043213/9d675d9f-e22b-484d-ae68-75eed5378bcc" width="200" height="200" /></br> 


## โปสเตอร์
> ![poster (download)](https://media.discordapp.net/attachments/865671142626033694/974339698401116220/poster_compro.jpg?width=496&height=702)
## ชิ้นงาน
> >  ![microcontroller (download)](https://media.discordapp.net/attachments/865671142626033694/974340163226456105/279963943_378952927534906_8536625025542008159_n.jpg?width=526&height=701)
## Code การเชื่อมต่อตัว Microcontroller กับ LINE
```C
void setup()
{
  Serial.begin(9600);
  dht.setup(2); // data pin 2
  
  WiFi.begin(ssid, pass); 
  delay(1000);
  Serial.print("Connecting to ");
  Serial.print(ssid);
  Serial.print("\nPleas wait"); 
  
  while (WiFi.status() != WL_CONNECTED) 
  {
    Serial.print(".");
    delay(300);
  }
  
  Serial.print("\nWiFi connected\nIP : ");
  Serial.println(WiFi.localIP());
  LINE.setToken(LINE_TOKEN);  // กำหนด Line Token
  LINE.notify("เชื่อมต่อกับ WeatherToday สำเร็จเเล้ว");

  ts = ts1 = millis();
}
```
## Code การส่งข้อความวัดค่าอุณหภูมิและความชื้นจาก Microcontroller ไปที่ LINE
```C
void loop(){
  delay(dht.getMinimumSamplingPeriod());
  float humidity = dht.getHumidity(); // ดึงค่าความชื้น
  float temperature = dht.getTemperature(); // ดึงค่าอุณหภูมิ
  ts = millis();
  //DHT.read11(dht_apin);
 if ((ts - ts1 >= 10000) && (WiFi.status() == WL_CONNECTED))
 { 
  LINE.notify("Temperature : " + String(temperature) + " °C" +"\n" + "Humidity : " + String(humidity)) + " %";
  return;
 } 
```
## ตัวอย่างการส่งข้อความผ่านไลน์
> >  ![Line (download)](https://media.discordapp.net/attachments/865671142626033694/974340163775905892/279510677_733612044304531_965625920282107422_n.png?width=324&height=701)
## วิดีโอนำเสนอชิ้นงาน
> * [Youtube](https://www.youtube.com/watch?v=nYhOadwQpEU)
---
# Members <img src="https://www.iwlconsulting.com/wp-content/uploads/2020/09/teamwork-icon-200x200-1.gif"  width="50">

| Student ID | ชื่อ - นามสกุล |
| :--------  | :-------- |
|   64070121 |   นางสาวนิโลบล ตรีสุคนธรัตน์ |
|   64070142 |   	นายพงศกร นพรัตยาภรณ์   |
|   64070155 |   	นางสาวพิชญา พัฒน์เจริญ  |
|   64070168   |   นางสาวภัณฑิรา ปิ่นกิ่งทอง |
