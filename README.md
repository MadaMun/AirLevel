<img src="https://github.com/MadaMun/AirLevel/assets/94043213/af91afbb-a329-4d53-97ef-05f6169e0fa6" width=1100 height="200" /></br>
# AirLevel
> This AirLevel project is part of Computer Programming Project, KMITL Semester 10/2022 2st Year
 ## บทคัดย่อ 📝
> เนื่องจากพบว่าในปัจจุบันมีค่าฝุ่นที่เพิ่มมากขึ้นซึ่งเป็นสาเหตุหนึ่งของโรคที่เกี่ยวข้องกับทางเดินหายใจ โดยมีคนไทยเป็นโรคนี้จำนวนมากติด Top 5 ของโรคที่คนไทยเป็นมากที่สุด
>    
> ผู้จัดทำเห็นถึงปัญหาจึงจัดทำโครงงานชิ้นงาน Air quality notification ที่ใช้ C เป็น Microcontroller โดยเป็นการวัดค่าคุณภาพอากาศของพื้นที่ที่เซ็นเซอร์ตรวจวัดค่าฝุ่นตั้งอยู่  
>
> โดยเรานำความรู้ และทักษะการต่อวงจรจากวิชา Physical Computing มาปรับใช้กับการพัฒนา Microcontroller ตัวนี้ และเพื่อความสะดวกต่อการรับรู้ข้อมูลคุณภาพอากาศ เราจึงทำการแสดงผลของข้อมูลผ่าน notification ของ Application LINE
## วัตถุประสงค์ :triangular_flag_on_post:
> * เพื่อป้องกันและเฝ้าระวังค่า PM 2.5 และหาทางป้องกันเพื่อไม่ให้กระทบต่อสุขภาพในแต่ละวัน
> * เพื่อนำความรู้ภาษา C มาประยุกต์ใช้ให้เกิดประโยชน์
> * เพื่อเสริมสร้างแหล่งข้อมูลข่าวสารที่สะดวกสบายเกี่ยวกับ PM 2.5
> * เพื่ออำนวยความสะดวกให้บุคคลทั่วไปสามารถรับข้อมูลได้ง่ายยิ่งขึ้น
## หลักการทำงาน 🔥
> เริ่มต้นจากสร้างการเชื่อมต่อกับwifi ด้วย SSID(ชื่อเครือข่าย) และ Password จากนั้น สร้างการเชื่อมต่อกับ Line ด้วย Access Token ที่ generate ขึ้น จากส่วนที่ประกาศไว้ ผ่านโค้ดในส่วน setup()
> 
> จากนั้น Sensor จะส่งแสงเลเซอร์ไปกระทบกับตัวรับและให้อากาศผ่านในช่อง หากการรับแสงมีน้อยแสดงว่าฝุ่นละอองเยอะ หากมีการรับแสงได้มากแสดงว่าฝุ่นละอองน้อย จะทำให้ได้ค่าฝุ่นออกมา 
> 
> สุดท้ายจะทำการส่งค่าที่ได้ด้วยคำสั่ง Notify จากไลบารี่ TridentTD_Linenotify ทำให้แสดงออกมาเป็นผลลัพธ์ผ่านทาง Groupchat Line ที่มาจากการดึงบัญชี Line notify ที่เชื่อมต่อผ่าน Token เรียบร้อยแล้วเข้าไปในกลุ่ม
## ผลคาดว่าที่จะได้รับ 💫
> * สามารถเข้าถึงข้อมูลคุณภาพอากาศภายในบริเวณได้อย่างสะดวก รวดเร็ว และมีความน่าเชื่อถือ
> * ได้นำความรู้ที่เรียนจากวิชา Physical Computing มาปรับใช้และต่อยอดกับชีวิตประจำวัน
## อุปกรณ์ 🛠
> 1. Breadboard  
> <img src="https://github.com/MadaMun/language_C/assets/94043213/4f984cb9-8093-4ce5-9acf-8c4d924d9c1b" width="200" height="200" /></br> 
> 2. Node mcu esp8266 v2  
> <img src="https://github.com/MadaMun/AirLevel/assets/94043213/85384ed9-9a2d-4fab-b4a5-e57b78865af7" width="200" height="200" /></br> 
> 3. sharp gp2y1010au0f dust sensor  
> <img src="https://github.com/MadaMun/language_C/assets/94043213/27dc01a0-2a05-4140-9624-31254541cdd0" width="200" height="200" /></br> 
> 4. สายไฟจั้มเปอร์  
> <img src="https://github.com/MadaMun/language_C/assets/94043213/9d675d9f-e22b-484d-ae68-75eed5378bcc" width="200" height="200" /></br> 


## โปสเตอร์ ✨
> ![poster (download)](https://media.discordapp.net/attachments/865671142626033694/974339698401116220/poster_compro.jpg?width=496&height=702)
## ชิ้นงาน 📦️
> >  ![microcontroller (download)](https://media.discordapp.net/attachments/865671142626033694/974340163226456105/279963943_378952927534906_8536625025542008159_n.jpg?width=526&height=701)
## Code การเชื่อมต่อตัว Microcontroller กับ LINE 🧑‍💻
```C
void setup() 
{
  initHardware();
  Serial.begin(115200); // Initialize the serial communication
  digitalWrite(LED_PIN, HIGH);
  Serial.println(LINE.getVersion());

  WiFi.begin(SSID, PASSWORD);
  Serial.printf("WiFi connecting to %s\n",  SSID);
  while (WiFi.status() != WL_CONNECTED) {
    Serial.print(".");
    delay(400);
  }
  Serial.printf("\nWiFi connected\nIP : ");
  Serial.println(WiFi.localIP());

  // กำหนด Line Token
  LINE.setToken(LINE_TOKEN);
}
```
## Code การส่งข้อความคุณภาพของอากาศจาก Microcontroller ไปที่ LINE 🧑‍💻
```C
void loop() 
{
  // Read analog data from the dust sensor
  int dustConcentration = analogRead(ANALOG_PIN);

  // Read digital data from another sensor, if needed
  int digitalValue = digitalRead(DIGITAL_PIN);

  // Print the data to the serial monitor
  Serial.print("Dust Concentration (analog): ");
  Serial.println(dustConcentration);
  LINE.notify("");
  LINE.notify("Dust Concentration "+String(dustConcentration)+" ug/m^3");
  if(dustConcentration>50){
    LINE.notify("Air Condition is not quite good, be careful.");
  }

  // Print the digital value, if applicable


  delay(60000); // Adjust the delay to control the data printing frequency
}

void initHardware()
{
  pinMode(DIGITAL_PIN, INPUT_PULLUP);
  pinMode(LED_PIN, OUTPUT);
  digitalWrite(LED_PIN, LOW);
  // No need to set ANALOG_PIN as input, that's all it can be.
}
```
## ตัวอย่างการส่งข้อความผ่านไลน์ 💬
> > <img src="https://github.com/MadaMun/AirLevel/assets/94043213/6154e331-1d09-4cc3-8ac2-b3bf26ce99cc" width="400" height="600" /></br>


## วิดีโอนำเสนอชิ้นงาน <img src="https://github.com/MadaMun/language_C/assets/94043213/7491e0c9-fac8-49c1-893c-e50b9d82b7f8" width="30" height="20" />

[Youtube](https://www.youtube.com/watch?v=nYhOadwQpEU)

---
# Members <img src="https://www.iwlconsulting.com/wp-content/uploads/2020/09/teamwork-icon-200x200-1.gif"  width="50">

| Student ID | ชื่อ - นามสกุล |
| :--------  | :-------- |
|   65070121 |   นางสาวนิโลบล ตรีสุคนธรัตน์ |
|   65070142 |   	นายพงศกร นพรัตยาภรณ์   |
|   65070155 |   	นางสาวพิชญา พัฒน์เจริญ  |
|   65070168   |   นางสาวภัณฑิรา ปิ่นกิ่งทอง |
