# Proximity-Alert-System-using-ESP32
# 🔊 Proximity Alert System using ESP32

This project uses an **ultrasonic sensor (HC-SR04)** and a **buzzer**, connected to an **ESP32**, to create a simple **proximity alert system**. When an object comes within 10 cm of the sensor, the buzzer sounds an alert.

## 🚀 Features

- Detects objects within a specified range (10 cm).
- Activates a buzzer alert when the object is too close.
- Uses ESP32 for fast, low-power operation.
- Serial Monitor displays real-time distance data.

## 🛠️ Components Used

| Component            | Quantity |
|----------------------|----------|
| ESP32 Dev Board      | 1        |
| Ultrasonic Sensor HC-SR04 | 1        |
| Buzzer (Active or Passive) | 1        |
| Jumper Wires         | As needed |
| Breadboard           | 1        |

## 🔌 Circuit Diagram

### Ultrasonic Sensor (HC-SR04) to ESP32:
- **VCC** → 3.3V
- **GND** → GND
- **Trig** → GPIO 12
- **Echo** → GPIO 13

### Buzzer to ESP32:
- **Positive (long leg)** → GPIO 15
- **Negative (short leg)** → GND

> ⚠️ If your buzzer requires more current, use a transistor or a relay module.

## 📟 Code

```cpp
#define TRIG_PIN 12    // Trigger pin of the ultrasonic sensor
#define ECHO_PIN 13    // Echo pin of the ultrasonic sensor
#define BUZZER_PIN 15  // Buzzer pin

void setup() {
  Serial.begin(115200);
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  digitalWrite(BUZZER_PIN, LOW);
}

void loop() {
  // Send trigger pulse
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  // Measure echo time
  long duration = pulseIn(ECHO_PIN, HIGH);
  long distance = (duration / 2) / 29.1;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance < 10) {
    digitalWrite(BUZZER_PIN, HIGH); // Turn buzzer ON
  } else {
    digitalWrite(BUZZER_PIN, LOW);  // Turn buzzer OFF
  }

  delay(500);
}
