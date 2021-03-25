#**การทดลองที่ 7 เรื่อง การเขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP) เขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์**

##**วัตถุประสงค์(อธิบายเป็นข้อๆ)**
1. เพื่อที่จะสามารถใช้ไมโครคอนโทรเลอร์ตัวนั้นได้ในสิ่งที่เราต้องการ
2. เพื่อที่จะสามารถ run program ลงไปโครคอนโทรเลอร์ได้สำเร็จ

##**อุปกรณ์ที่ใช้ (รายการอุปกรณ์)**
1. ไมโครคอนโทรเลอร์
2. USB

##**ศึกษาข้อมูลเบื้องต้น (แหล่งข้อมูลเพื่อการศึกษา)**

#โปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP) [YouTube](https://www.youtube.com/watch?v=T26DVHePlTs)

#เขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์   [YouTube](https://www.youtube.com/watch?v=VX-QNQcO-b4)

##**วิธีการทำการทดลอง (ทำเป็นขั้นตอนพร้อมภาพประกอบ)**
1. ต่อ USB เข้า อแดปเตอร์ และค่อยนำไมโครคอนโทรเลอร์มาเสียบต่อ [![Image](https://imgbb.com/)](https://ibb.co/qWCHFqG)
2. พิมพ์ platformio.ini src และพิมพ์ vi src/main.cpp ซึ่งเป็นโปรแกรม 06 ไว้ทดสอบไมโครคอนโทรเลอร์ โดยที่ต้องสร้าง wifi AP ขึ้นเอง ซึ่งเขียนด้วยภาษา C/C++ โดยที่เราต้องกำหนดชื่อ wifi ของเรา ในที่นี้ชื่อ ssid = WIFI-FREE-MEE-YOU-JING และจะไม่มี password เนื่องจากเป็น wifi ที่ให้ใช้ free และถ้าจะปล่อย wifi ให้ใช้ ต้องกำหนด IPAddress ทั้ง local_ip , gateway subnet  มี 2 ส่วน ส่วนแรก คือส่วน setup() ซึ่งจะ run ครั้งเดียว (บรรทัดที่ 15-35) จะทำการ set server ไว้ 1ตัว และrunคำสั่ง APโดยกำหนด ssid และ password ลงไป และrunบอกว่า IPAddess ที่ตั้งไว้เป็นเท่าไหร่ และส่วนที่สอง คือส่วน loop() ซึ่งจะวนloopเรื่อยๆ ตลอดไป 
3. จากนั้นเขียนโปรแกรมต่อไป คือโปรแกรม 05_Wifi-Web-Server out put portไว้ทดสอบไมโครคอนโทรเลอร์ โดยที่ต้องต่อกับwifiก่อน ชื่อ ssid = WIFI-FREE-MEE-YOU-JING ลงไป ซึ่งเขียนด้วยภาษา C/C++ มี 2 ส่วน ส่วนแรก คือส่วน setup() ซึ่งจะ run ครั้งเดียว (บรรทัดที่ 15-22) จะทำการ set Wifi ที่เลือกไว้ หลังจากนั้นก็จะset up web server ถ้ามีการเชื่อมโยงก็จะแสดงผลง่ายๆ โดยนำ cnt++ มาบวก1ไปเรื่อยๆ และส่วนที่สอง คือส่วน loop() ก็จะ run วนloop ตลอดไป
4. พิมพ์ pio run -t upload เพื่อที่จะ upload โปรแกรมลงไมโครคอนโทรเลอร์ ในขณะที่ run ก็กดปุ่มดำเพื่อบอกให้มัน load โหลดช้าเร็วขึ้นกับความเร็วของมัน และกดปุ่มแดงให้มัน reset 
5. เมื่อโหลดเสร็จแล้ว เราจะต้องใช้โทรศัพท์มือถือ หรือคอมพิวเตอร์ในการเช็คผลลัพธ์ ในที่นี้ใช้โทรศัพท์มือถือ โดยที่ต้องพิมพ์ pio device monitor และ ver started ก่อน เพื่อดูผลลัพธ์ที่แสดงบนหน้าจอ monitor ไมโครคอนโทรเลอร์จะแสดงการค้นหา wifi บนโทรศัพท์มือถือ แล้วทำการเขื่อมต่อwifi 
6. จากนั้นเข้าไปเซ็คที่ web browser กดปุ่ม reset และ  พิมพ์ pio device monitor เพื่อดูผลลัพธ์ที่แสดงบนหน้าจอ monitor ไมโครคอนโทรเลอร์จะแสดงการค้นหา wifi แล้วเขื่อมต่อwifi จากนั้นจะบอก IPAddress เราทำการ copy แล้วใช้ browser จะแสดงผล่า hello 1 hello 2 hello 3 ไปเรื่อยๆ แสดงว่าสามารถใช้ไมโครคอนโทรเลอร์ตัวนี้เข้า web server ได้ทั่วไป 

##**platformio.ini**
```
platform = espressif8266
board = esp01_1m
framework = arduino
board_build.flash_mode = dout

upload_port = /dev/cu.usbserial-1420
;upload_port = COM3

monitor_port = /dev/cu.usbserial-1420
;monitor_port = COM3
monitor_speed = 115200
```
##**CODE เขียนโปรแกรมสร้างไวไฟแอคเซสพอยต์ (Wifi AP)**
```
#include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>

const char* ssid = "WIFI-FREE-MEE-YOU-JING";

IPAddress local_ip(198, 186, 1, 1);
IPAddress gateway(198, 186, 1, 1);
IPAddress subnet(234, 234, 234, 0);

ESP8266WebServer server(80);

int cnt = 0;

void setup(void){
	Serial.begin(115200);

	WiFi.softAP(ssid);
	WiFi.softAPConfig(local_ip, gateway, subnet);
	delay(200);

	server.onNotFound([]() {
		server.send(404, "text/plain", "Path Not Found");
	});

	server.on("/", []() {
		cnt++;
		String msg = "Connected cnt: ";
		msg += cnt;
		server.send(200, "text/plain", msg);
	});

	server.begin();
	Serial.println("HTTP server started");
}

void loop(void){
  server.handleClient();
}

```
##**CODE เขียนโปรแกรมเชื่อมต่อไวไฟและเว็บเซอร์เวอร์**
```
#include <ESP8266WiFi.h>
//#include <WiFiClient.h>
#include <ESP8266WebServer.h>

const char* ssid = "HI_BMFWIFI_2.4G";

ESP8266WebServer server(80);

int cnt = 0;

void setup(void){
	Serial.begin(115200);

	WiFi.mode(WIFI_STA);
	WiFi.begin(ssid);
	while (WiFi.status() != WL_CONNECTED) {
		delay(200);
		Serial.print(".");
	}
	Serial.print("\n\nIP address: ");
	Serial.println(WiFi.localIP());

	server.onNotFound([]() {
		server.send(404, "text/plain", "Path Not Found");
	});

	/// http://192.0.0.1/ = Hello cnt: ???
	server.on("/", []() {
		cnt++;
		String msg = "Hello cnt: ";
		msg += cnt;
		server.send(200, "text/plain", msg);
	});
	/// http://198.0.0.1/on = Hello cnt: ???
	server.on("/on", []() {
		cnt++;
		String msg = "Switch on ";
		msg += cnt;
		server.send(200, "text/plain", msg);
	});
	/// http://198.0.0.1/off = Switch off: ???
	server.on("/off", []() {
		cnt++;
		String msg = "Connected cnt: ";
		msg += cnt;
		server.send(200, "text/plain", msg);
	});

	server.begin();
	Serial.println("HTTP server started");
}

void loop(void){
  server.handleClient();
}
```
##**การบันทึกผลการทดลอง (พร้อมตัวอย่าง)**
####### ต้องใช้โทรศัพท์มือถือ หรือคอมพิวเตอร์ในการเช็คผลลัพธ์ ในที่นี้ใช้โทรศัพท์มือถือ โดยที่ต้องพิมพ์ pio device monitor และ ver started ก่อน เพื่อดูผลลัพธ์ที่แสดงบนหน้าจอ monitor ไมโครคอนโทรเลอร์จะแสดงการค้นหา wifi บนโทรศัพท์มือถือ แล้วทำการเขื่อมต่อwifi  ผลลัพธ์ที่แสดงบนหน้าจอ monitor ไมโครคอนโทรเลอร์จะแสดงการค้นหา wifi แล้วเชื่อมต่อwifi จากนั้นจะบอก IPAddress เราทำการ copy แล้วใช้ browser จะแสดงผลว่า hello 1 hello 2 hello 3 ไปเรื่อยๆ แสดงว่าสามารถใช้ไมโครคอนโทรเลอร์ตัวนี้เข้า web server ได้ทั่วไป 

##**อภิปรายผลการทดลอง (พร้อมตัวอย่าง)**
####### ในการทดสอบไมโครคอนโทรเลอร์ตัวนี้ เราไม่ต้องใช้ wifi AP ของที่อื่น เราสามารถสร้างโปรแกรมขึ้นมาเองได้

##**คำถามหลังการทดลอง (พร้อมตัวอย่างคำตอบ)**
####### ต้องใช้คำสั่งอะไรให้แสดงผลบนหน้าจอ
####### ANS พิมพ์ pio device monitor และ ver started ก่อน เพื่อดูผลลัพธ์ที่แสดงบนหน้าจอ monitor ไมโครคอนโทรเลอร์
