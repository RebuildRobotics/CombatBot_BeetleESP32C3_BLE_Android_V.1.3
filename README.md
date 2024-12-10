****************************************
# CombatBot for Beetle ESP32-C3 - BLE - Android
****************************************

  Free script designed to provide the platform for hobbyists and educational use as a starting point for
  controlling 150-450 g Combat Robots with Android smartphone/tablet via Bluetooth Low Energy (BLE).
  
  Controlling is done with Rebuild {Robotics} - Bot Controller Android app.
  
  Script and controller can also be used to control basic Arduino based bots with servo.

  *****
  FEATURES:
  *****
  - High accuracy tank steering with center brake.
  - Channel mixing between ch1(fwd/bwd) and ch2(left/right) channels.
  - Drive motor rotation inverting and trim.
  - Supports DC motors using HR8833 or TB6612FNG DC motor driver or Brushless motors using ESC's for driving.
  - Support for single servo or brushless motor controlled by ESC as weapon motor.
  - 1-2S LiPo battery voltage monitoring.
  - Failsafe (Stops all functions when disconnected from controller. Same function is used with low voltage guard).
  - Low voltage guard (Protects battery by activating failsafe when battery is running low while keeping controller connected to bot. Failsafe will be deactivated when voltage becomes higher than shutdown level).
    (If facing problems with voltage drops and guard is stopping motors with close to charged battery try to use quality connectors like BT2.0 or XT-30 not JST's, proper cable sizes and possible capacitor near weapons power drain.)
  - Customizable AI slot (ch4, void runAI).
  - Buildin automatic support in Custom AI slot for flippers using DFRobot VL6180X ToF Distance Ranging Sensor.
  - Weapon/servo presets, drive motor directions and trim levels can be set from script presets.
  - Bot name, weapon/servo presets, drive motor directions and trim levels can be updated straight from controller.
  - Signal and variable debugging through serial monitor.
  - Onboard led indicates error-, standby-, bluetooth- and weapon statuses as followed:
      - Blink, dim/slow     =   Standby
      - Blink, bright/fast  =   Script weapon parameter error
      - Solid, dim          =   Bluetooth connected
      - Solid, bright       =   Weapon signal active
      
  *****
  HARDWARE EXAMPLE (150g With DC Motors):
  *****
  - DFRobot - Beetle ESP32-C3
  - DFRobot - Fermion: HR8833 Thumbnail Sized DC Motor Driver 2x1.5A or TB6612FNG 2x1.2A DC Motor Driver
  - DFRobot - Fermion: VL6180X ToF Distance Ranging Sensor 5-100mm (Optional, for flippers.)
  - Rebuild Robotics - ESP32-C3 CombatBot Expansion Board (Prototype) or 5V BEC to convert battery voltage for boards
  - Rebuild Robotics - TinySwitch (Prototype)
  - Rebuild Robotics - TinyLED (Prototype)
  - 6V 600/1000RPM Geared N10/N20 DC motors
  - Servo for flipper or brushless motor and ESC for spinning weapon
  - 2S 180-300mAh LiPo battery
  - 22AWG Wires for drive motors, calculate main power and ESC needs separately
  - BT2.0 Connector pair (Replace battery JST with BT2.0 male connector. Remember to prevent battery shortcut!)
  - 10kOhm pull-down resistor for pin 6 with HR8833 and TB6612 (Included in ESP32-C3 CombatBot Expansion Board)

  *****
  OUTPUTS:
  *****
  - Driving:
    - DC motors:          2 x PWM + 2 digital outputs
    - Brushless motors:   2 x PPM outputs
  - Weapon ESC or servo:  1 x PPM output
  - PPM signals are generated with servo library.
  - If using brushless ESC's they has to be configured separately!
  
  *****
  HOW TO INSTALL:
  *****
  1. Read instructions.
  2. Install Arduino IDE from https://www.arduino.cc/en/software. It is the main program what you will use to manage this script and connection to ESP.
  3. Install board manager by following guide in wiki: https://wiki.dfrobot.com/SKU_DFR0868_Beetle_ESP32_C3 .
  4. Install proper library versions mentioned in this script.
  5. Set up proper pins and presets from script.
  6. Set up board manager presets from toolbars "Tools" dropdown and connect board.
  7. Upload script without battery or weapon being attached.
  8. Connect controller and have fun.
      
  *****
  ARDUINO IDE BOARD MANAGER & LIBRARIES:
  *****
  Tested stable versions:
  - Board:                    esp32 by Espressif Systems v.3.0.7  Install from Arduino IDE      (Uses ESP32 core 3.x)
  - Servo/Weapon control:     ESP32Servo v.3.0.6                  Install from Arduino IDE
  - Distance sensor:          DFRobot_VL6180X v.1.0.1             Install from Arduino IDE
  
  *****
  UPLOADING AND SERIAL MONITORING:
  *****
  Presets needed in Arduino IDE for serial monitoring and uploading script:
  - Tools > Board: > esp32 > DFRobot Beetle ESP32-C3
  - Tools > USB CDC On Boot > Enabled
  - Tools > Upload Speed > 115200
  - Tools > Erase All Flash Before Sketch Upload > Enabled = Erases all bot presets from Eeprom / Disabled = Keeps bot presets in memory.
      
  When updating new version of script flash should always be erased!

  *****
  PRESETS:
  *****
  - Basic presets can be changed from controller or from script below.
  - Presets will be saved into Eeprom when updated from controller.
  - Presets saved in Eeprom will be erased in upload if "Tools > Erase All Flash Before Sketch Upload" is enabled.
  
  *****
  DEBUG:
  *****
  - Debug mode and serial monitoring can be enabled from below by changing "#define DEBUG" to true and reuploading script to ESP.
  - You might have to reset ESP once from button to get clean serial monitor output in start.
  - If facing problems uploading script and having "exit status 2..." error keep Arduino IDE open, plug ESP off from USB port, keep pressing Boot button while plugging ESP back into computer,
    reupload script and let go off from the Boot button when uploading has been started. https://wiki.dfrobot.com/SKU_DFR0868_Beetle_ESP32_C3

  *****  
  COMMUNICATION:
  *****
  - Script uses 2,4GHz Bluetooth Low Energy (BLE) network to receive data from mobile phone controller as string.
  - Can handle incoming bluetooth messages in 20ms intervals.
  - String format ch1:ch2:ch3:ch4\n .
  - ch1 = fwd/bwd speed, ch2 = left/right speed, ch3 = servo angle or weapon speed, ch4 = AI on/off.
  - ch1 and ch2 values are in scale of -100~100, ch3 and ch4 0~100. 0 is stop. Signals are converted to PWM value scale 0~255. Negative numbers are absoluted.

  *****
  CONTROLLER:
  *****
  - Android: Rebuild Robotics - Bot Controller (Download from: https://github.com/RebuildRobotics).
  - Iphone: Not available, hopefully some day.
  - Controller is specially made for controlling combat robots and Arduino based bots.
  - Bot name, weapon/servo presets, drive motor directions and trim levels can be updated straight from controller.
  - When using script with controller primary version numbers should always match (e.g. Controller: 1.2 - Bot Script: 1.2.1 vice versa).

  *****
  SAFETY NOTICE:
  *****
  - Combat robotics is fun and extremely educating but dangerous hobby, always think safety first!
  - Script includes failsafe function to prevent up accidents. Function shuts down drive- and weapon motors when controllers signal is lost.
    This is same kind of option than good RC receivers have and it's required in combat robotics.
  - Remember to set pins correctly, if they are not set right script and failsafe won't work properly!
  - Do not keep battery connected at the same time when USB is connected into powersource!
  - Accidentally motor spins will happen when ESP is powered, script is uploading or wrong board or library version is installed!
    Motor spins at startup can be prevented by using pull-up/pull down resistors or our designed ESP32-C3 CombatBot Expansion Board and tested IDE library versions.
  - Configure ESC properly before connecting controller into bot, or it causes serious hazard!
  - Test bot with precaution and only weapon motor attached, not weapon itself!
  - Do not use any other board manager or library versions than those which are mentioned as tested and safe ones in this scripts read me area!
    It might cause serious injuries because board functionalities are changing. Future updates to this script includes fresher and tested information from later versions.
  - Remember always check that you have correct versions installed before updating script into board.
  - Modify script only if you know what you are doing!
  - Script has been tested only in close range at Combat arenas. When driving outside use precaution.

  *****
  SUPPORTING PROJECTS:
  *****
  You can sponsor this and other projects without this couldn't been done from links below.
  - Coming some day..
  
  *****
  SOURCES:
  *****
  Hardware:
    - https://wiki.dfrobot.com/SKU_DFR0868_Beetle_ESP32_C3
    - https://wiki.dfrobot.com/2x1.2A_DC_Motor_Driver__TB6612FNG__SKU__DRI0044
    - https://wiki.dfrobot.com/Dual_1.5A_Motor_Driver_-_HR8833_SKU__DRI0040
    - https://wiki.dfrobot.com/DFRobot_VL6180X_TOF_Distance_Ranging_Sensor_Breakout_Board_SKU_SEN0427

  Driving:
    - https://youtu.be/Bx0y1qyLHQ4?si=U1tk3dPtz3ZfaxqV
    - https://gist.github.com/ShawnHymel/ccc28335978d5d5b2ce70a2a9f6935f4

  This script has been made respecting the regulations of combat robotics and they should be usable all around the world.
  Script builders and component manufacturers are not responsiple from possible damages.
  Third party script writers hasn't got nothing to do with this project except I'm using their libraries.
