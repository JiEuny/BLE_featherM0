# BLE_featherM0
bluefruit le (BLE) module + adafruit feather M0
created by JiEun Lee 
email : love9ly@gmail.com

1. 라이브러리 다운로드 및 추가
https://learn.adafruit.com/introducing-the-adafruit-bluefruit-le-uart-friend/software

2. ble가 잘 작동하는지 확인하기 위해 예제의 atcommand 샘플을 우선 테스트

3. 회로도를 따라 feather 보드와 ble 모듈을 구성한다.
            feather m0    ble
              rx          tx
              tx          rx
              usb         vin
              gnd         gnd
              gnd         cts
  
*특히 CTS핀은 반드시 GND로 물려야 하며, 모드 스위치는 CMD 모드에 둬야함

4. UART 통신을 위해서 코드 수정 필요
  - spi 통신 코드를 주석처리하고 uart 통신 코드의 주석을 풀어 Serial1을 디파인 해 주어야 함
  
----------------------------------------------------------------------------------------------------

#define BLUEFRUIT_HWSERIAL_NAME      Serial1
/* ...or hardware serial, which does not need the RTS/CTS pins. Uncomment this line */
Adafruit_BluefruitLE_UART ble(BLUEFRUIT_HWSERIAL_NAME, BLUEFRUIT_UART_MODE_PIN);

/* ...hardware SPI, using SCK/MOSI/MISO hardware SPI pins and then user selected CS/IRQ/RST */
//Adafruit_BluefruitLE_SPI ble(BLUEFRUIT_SPI_CS, BLUEFRUIT_SPI_IRQ, BLUEFRUIT_SPI_RST);

----------------------------------------------------------------------------------------------------

5. 시리얼 모니터를 통해 ble의 정보를 읽어오고 AT 명령어가 정상적으로 동작하는 것을 확인한 후, 다음 과정으로 넘어감

6. 예제 코드 중 bleuart_datamode 샘플을 불러와서 4번의 과정을 반복하거나, bleuart_datamode_20181121 파일을 다운받아 업로드
  *이 떄도 모드 스위치는 CMD 모드에 둬야함
  
7. 시리얼 모니터를 통해 ble가 정상적으로 factory reset을 완료하면, bluefruit 어플리케이션을 다운받아 블루투스 연결

8. 블루투스 연결에 성공하면 어플리케이션의 UART 모드로 들어간 후, ble 모듈의 모드 스위치를 UART 모드로 변경

9. 정상적으로 데이터를 주고받는 과정 확인

*feather 보드에 코드를 업로드 할 때는 반드시 모드 스위치를 CMD 모드로 두어야 하며,
  데이터를 주고받을 시에만, UART 모드로 두어야 함
