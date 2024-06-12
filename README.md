# Custom Wake word "Hey Alfred" for home assistant. This is a work in progress!!

## TIf you want to build you own you wake work instead of "Hey Alfred" you can follow these instructions [These instructions](https://www.home-assistant.io/voice_control/create_wake_word/) and use the generated file the the instructions below 

## Install

To install The Hey Alfred wake word, you must have a [Wyoming Satellite](https://github.com/rhasspy/wyoming-satellite) up and running.

You can choose where to initially download the files. I put them in the root directory, but we will be moving and renaming the files later.

1. SSH into your Pi
2. Run the following in your root or were you would like to have thes file stored in on your directory
   ```
   git clone https://github.com/The-Blackstone/HeyAlfredWakeWord
   ```

3. Enter new directrory
   ```
   cd ~/HeyAlfredWakeWord
   ```
4. Pick Sensitivity 1 beeing less sentive and 3 beeing most sensitiv and run the following command
   ```
   cp hey_alfred_sensitivity_{Insert 1-3}.tflite ~/wyoming-openwakeword/wyoming_openwakeword/models/hey_alfred_v0.1.tflite
   ```
5. Open the Wyoming services to choose the new wake command
   ```
   sudo systemctl edit --force --full wyoming-satellite.service
   ```
6. Eddit the file and change
   ```
   [Unit]
   ...
   Requires=wyoming-openwakeword.service
   
   [Service]
   ...
   ExecStart=/home/pi/wyoming-satellite/script/run ... --wake-uri 'tcp://127.0.0.1:10400' --wake-word-name 'ok_nabu'
   ...
   
   [Install]
   ...
   ```
   To
   ```
   [Unit]
   ...
   Requires=wyoming-openwakeword.service
   
   [Service]
   ...
   ExecStart=/home/pi/wyoming-satellite/script/run ... --wake-uri 'tcp://127.0.0.1:10400' --wake-word-name 'hey_alfred'
   ...
   
   [Install]
   ...
   ```
7. Save, exit and Restart Wyoming services
   ```
   sudo systemctl daemon-reload
   ```
   ```
   sudo systemctl restart wyoming-satellite.service
   ```

   
