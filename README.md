# Arduino-serial-communication
Arduino serial communication between Leonardo and Uno
#include <SoftwareSerial.h>
SoftwareSerial mySerial(7, 6);  // 7번을 RX, 6번을 TX 처럼 사용할 수 있게 핀지정


void setup() {
  // put your setup code here, to run once:
  Serial1.begin(9600);  // 아두이노와 RFID리더기 하드웨어 Serial
  Serial.begin(9600);  // 아두이노와 컴퓨터간의 Serial
  mySerial.begin(9600); // leonardo와 uno간의 serial
}

void loop() {
  // put your main code here, to run repeatedly:
  static String sentence; // 저장된 문장
  byte data;

  while (Serial1.available()) {
    data = Serial1.read();
    mySerial.write(data);
    sentence += char(data);

    // 문장의 끝을 구두점으로 판단하고 줄 바꿈 추가
    if (data == '') {
      Serial.write('\n');
      sentence = ""; // 문장 초기화
    }
    if (Serial.available()) {
    data = Serial.read();
    mySerial.write(Serial.read());
  }
  }
  delay(10);
}
