# 🏠 Home Automation Using IoT (Blynk)

This project allows you to control light and fan using your smartphone via the Blynk IoT platform.

## 💡 Components Used
- NodeMCU ESP8266
- 2-Channel Relay Module (or LEDs for demo)
- Smartphone with Blynk app
- Internet (WiFi)

## 📱 Blynk Setup
- Create new project → ESP8266
- Add 2 buttons:
  - Light: Virtual Pin V0
  - Fan: Virtual Pin V1
- Copy Auth Token from email

## ⚙️ Connections
| Device | NodeMCU Pin |
|--------|--------------|
| Light  | D1 (GPIO5)   |
| Fan    | D2 (GPIO4)   |

## 💻 Code

```cpp
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

char auth[] = "YourAuthToken";
char ssid[] = "YourWiFiName";
char pass[] = "YourWiFiPassword";

#define LIGHT D1
#define FAN D2

void setup() {
  pinMode(LIGHT, OUTPUT);
  pinMode(FAN, OUTPUT);
  Blynk.begin(auth, ssid, pass);
}

BLYNK_WRITE(V0) {
  digitalWrite(LIGHT, param.asInt());
}

BLYNK_WRITE(V1) {
  digitalWrite(FAN, param.asInt());
}

void loop() {
  Blynk.run();
}
