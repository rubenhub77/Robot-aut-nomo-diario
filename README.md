1. Mobility Management
The mobility design is based on a two-wheel drive differential chassis, powered by two DC motors controlled by an H-bridge.
● Chassis: A base chassis was selected and modified to increase internal space. This allowed for a clean integration of the H-bridge, ESP32, voltage regulator, and 2800 mAh Li-Po battery, ensuring a balanced center of gravity. (This supports criterion 7).
● Motor Control (H-bridge): Pulse-width modulation (PWM) is used on pins pinEN1 (12) and pinEN2 (13) using the function analogWrite(pinENx, 100). The value of 100/255 (approximately 39% of the maximum speed) was chosen to provide a balance between speed and torque, allowing for quick turns and stable control.
● Movement Patterns: The implemented logic allows for four main movements: Forward, Backward, Right Turn, and Left Turn (see details in Criterion 3).

2. Power and Sensor Management
Power management and sensor information are critical for autonomy and navigation.
● Power Source: A 2800 mAh Li-Po battery is used to power the system. This type of battery provides high energy density, essential for operating time.
   ○ Voltage Regulation: A voltage regulator was implemented that converts the Li-Po output (motor voltage) to the 5V/3.3V required by the ESP32 and sensors, protecting the logic components. 

● Sensors (Senses): Three ultrasonic sensors are used for environmental perception, providing 180-degree coverage:
   ○ Front (echeo: 35, trige: 32): Primary obstacle detection.
   ○ Left (echeoi: 26, trigi: 27): Clear path assessment to the left.
  ○ Right (echod: 21, trigd: 23): Clear path assessment to the right.

● Wiring (Concept): The GND pins of all sensors were soldered together and connected to the OUT- of the regulator. Similarly, the VCC/DCC pins of the sensors were connected to the OUT+ of the regulator. This practice ensures a common ground and a clean, stable voltage supply for all sensors. 

3. Obstacle Management
The main strategy is Active Obstacle Avoidance, using the logic of the three ultrasonic sensors.
● Decision Logic (Pseudocode):
START
Set Speed ​​(EN1=100, EN2=100)
Read Distance Ahead (D1), Left (D2), Right (D3)

IF D1 < 20 cm
 IF D2 D3 (Closer obstacle to the left, turn right)
  Move BACKWARDS (1000 ms)
  Turn RIGHT
 IF NOT (D2 >= D3) (Closer obstacle to the right or equal distance, turn left)
   Move BACKWARDS (1000 ms)
   Turn LEFT
IF NOT (D1 >= 20 cm)
 Move FORWARD
END

Code Comments (Relevant Section): The robot uses a reverse and turn pattern when it detects a frontal obstacle (< 20 cm). The decision to turn right or left is based on the sensor indicating the greatest clearance (i.e., the sensor with the shortest relative distance to the obstacle is the one avoided).
Adjustments Made to the Remote Controlled Vehicle
Internal Electronic Dismantling
The remote control vehicle's body or casing was opened to access its interior. The original printed circuit board, essential for its primary operation, was removed. To do this, the set of cables connecting the following elements was disconnected:
● 1.1. Lighting System: Wiring for the vehicle's front and rear lights.
● 1.2. Propulsion and Steering Modules: Connections to the front motor (responsible for steering or the Ackerman mechanism) and the rear motor (responsible for forward and reverse movement).
● 1.3. Main Switch: The ignition switch was also disconnected.

2. Disabling the Four-Wheel Drive System (4x4): The vehicle's ability to operate in four-wheel drive was eliminated.
Both the front and rear drive mechanisms, which enabled the 4x4 function, were removed. Power was transmitted to the front wheels via a connecting shaft. This shaft was removed, thus disabling traction on the front axle.

3. Interior Space Optimization
The available internal volume of the chassis was increased.
The compartment originally intended to house the factory batteries was modified.
Since this space had become redundant or unnecessary after the electronic disconnections, a section was cut away to gain more cavity and free space inside the vehicle.
