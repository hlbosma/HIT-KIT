## 🔍 What the Code Does

* 🌐 Connects to WiFi and an MQTT broker to send and receive messages.
* ✋ Detects capacitive touch input on pin D13.
* 🔘 Reads a physical button state on pin D7.
* 📤 Sends MQTT messages when touch or button states change.
* 📥 Listens for incoming MQTT messages and prints them.

## 🚀 How to Use This Code

1. Connect your microcontroller to WiFi and configure your MQTT broker details in the `settings` file.
2. Connect the capacitive touch sensor to pin D13.
3. Connect the button to pin D7.
4. Run the script.
5. Touch or press the button to send MQTT messages.
6. Incoming MQTT messages on `"XR-message/trigger3"` will be printed.

## 🎮 Connecting to Unreal Engine

You can use MQTT messages from this script as **inputs in your Unreal Engine project**! This allows you to create interactive XR experiences controlled by physical sensors.

### The 3 Main Elements in Unreal Engine:

1. **Blueprint that spawns markers**

   * Contains a list linking specific marker IDs to specific blueprints you want to spawn.

2. **MQTT Connector**

   * Connects Unreal Engine to the MQTT broker and reads incoming messages.

3. **Spawned Blueprint**

   * Receives MQTT messages and spawns different objects depending on the message content.

## ⚙️ Main Parts of the Code

### 📨 MQTT Setup

* `Create_MQTT(client_id, handle_message)`: Creates an MQTT client to connect to the broker.
* `handle_message(client, topic, msg)`: Called when a new MQTT message arrives; stores the message for processing.

### 📡 MQTT Topics

* **Subscribed topic:** `"XR-message/trigger3"` — receives messages from other devices.
* **Published topics:**

  * `"TUI-message/trigger1"` — publishes touch input changes.
  * `"TUI-message/trigger2"` — publishes button input changes.

### 🛠️ Inputs

* `touchio.TouchIn(board.D13)`: Capacitive touch sensor on pin D13.
* `digitalio.DigitalInOut(board.D7)`: Button input on pin D7, configured with pull-down resistor.

### 🔄 Main Loop

* Continuously processes MQTT messages.
* Detects changes in touch and button states.
* Publishes MQTT messages reflecting those changes.
* Prints status updates with emojis for easy reading.
* Prints received MQTT messages from the subscribed topic.

### ⚠️ Error Handling

* If MQTT errors occur, the script tries to reconnect automatically and keeps running.
