# 🏠 HOME AUTOMATION USING IoT

## 🚀 Project Title:
**Home Automation to Control Light and Fan Using IoT Platforms (Blynk)**

---

## 📋 Intern Details

- **👨‍💼 Name:** Shaik Javed Ahmed  
- **🎓 Intern ID:** CT04DF594  
- **🏢 Company:** CodTech IT Solutions  
- **🌐 Domain:** Internet of Things  
- **📅 Internship Duration:** 4 Weeks  
- **🧑‍🏫 Mentor:** Neela Santhosh  

---

## 📌 Project Overview

This project demonstrates a simple home automation prototype that allows users to control **light and fan** appliances remotely using a **smartphone via the Blynk IoT platform**. It integrates a **NodeMCU ESP8266** microcontroller and **relay modules** to handle real devices.

---

## 🔧 Components Required

| Component       | Quantity |
|----------------|----------|
| NodeMCU ESP8266| 1        |
| 2-Channel Relay| 1        |
| Light Bulb (or LED)| 1    |
| Fan (or DC Motor)| 1      |
| Smartphone with Blynk App | 1 |
| Jumper Wires    | As required |
| Wi-Fi Connection| 1        |

---

## 📱 Blynk Setup Instructions

1. Install **Blynk IoT App** from Play Store/App Store.
2. Create a **new project** and select **ESP8266** as the device.
3. Add two buttons:
   - **Button 1** → Virtual Pin **V0** for Light  
   - **Button 2** → Virtual Pin **V1** for Fan
4. Set the button mode to **switch**.
5. Copy the **Auth Token** from the app (or email).

---

## ⚙️ Circuit Diagram

![Circuit Diagram](circuit_diagram.png)

*(Use the circuit image generated earlier)*

---

## 🧠 Working Principle

- The **NodeMCU ESP8266** connects to Wi-Fi and the Blynk cloud.
- Blynk mobile app buttons send signals to virtual pins (V0, V1).
- NodeMCU reads the virtual pin values and activates the **relay module**, turning ON/OFF light and fan accordingly.

---

## 💻 Arduino Code (`home_automation.ino`)

```cpp
#define BLYNK_TEMPLATE_ID "YourTemplateID"
#define BLYNK_TEMPLATE_NAME "HomeAutomation"
#define BLYNK_AUTH_TOKEN "YourAuthToken"

#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>

char auth[] = "YourAuthToken";         // Blynk Auth Token
char ssid[] = "YourWiFiName";          // WiFi SSID
char pass[] = "YourWiFiPassword";      // WiFi Password

#define LIGHT D1
#define FAN D2

void setup() {
  pinMode(LIGHT, OUTPUT);
  pinMode(FAN, OUTPUT);
  Blynk.begin(auth, ssid, pass);
}

BLYNK_WRITE(V0) {
  int pinValue = param.asInt();
  digitalWrite(LIGHT, pinValue);
}

BLYNK_WRITE(V1) {
  int pinValue = param.asInt();
  digitalWrite(FAN, pinValue);
}

void loop() {
  Blynk.run();
}

