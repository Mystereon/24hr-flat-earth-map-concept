Esp32 D1mini Flat Earth wall clock concept with 60 led neo pixel ring 

This is a code for a NeoPixel clock that displays the time with three LED "hands" (hour, minute, and second) on a ring of 60 LEDs. The clock connects to a WiFi network and synchronizes the time with a NTP server.

The code begins by importing the necessary libraries for the project. The NtpClientLib.h library is used to connect to the NTP server and synchronize the clock. The ESP8266WiFi.h library is used to connect to the WiFi network. The DNSServer.h and ESP8266WebServer.h libraries are used for WiFi configuration. The WiFiManager.h library is used for a WiFi configuration wizard. The Adafruit_NeoPixel.h library is used to control the NeoPixel LEDs.

Next, some constants are defined. NUMPIXELS is set to 60 to represent the number of NeoPixel LEDs. PIN is set to 2 to represent the digital pin on the ESP8266 for the NeoPixel data line. mirror_hands is a boolean variable that is used to control the orientation of the LED ring.

Then, the hour_hand, minute_hand, second_hand, and previous_second variables are declared. These will be used to keep track of the position of the LED "hands" on the clock.

The pixels object is created using the Adafruit_NeoPixel library, with the number of LEDs and the data pin specified.

The clearHands() function is defined to turn off all the LEDs on the ring. It loops through all the LEDs and sets their color to black.

The drawHands() function is defined to draw the current time on the NeoPixel ring. It starts by calling clearHands() to turn off all the LEDs.

Then, it sets the color of the LED at the position of the hour_hand to red. If the hour_hand and minute_hand positions are the same, it sets the color of the LED at that position to yellow. Otherwise, it sets the color of the LED at the minute_hand position to green.

Finally, it sets the color of the LED at the second_hand position to white. It calls pixels.show() to display the LEDs that have been set to a color. It also prints a debug message to the serial monitor to show the current time and LED positions.

In the setup() function, the serial connection is started, and the WiFiManager object is created. wifiManager.autoConnect() is called to connect to the WiFi network with the specified SSID and password.

Then, the NTP.begin() function is called to connect to the NTP server and synchronize the clock. NTP.setInterval() is called to set the interval between clock updates.

Finally, the pixels.begin() function is called to initialize the NeoPixel ring. The pixels.setBrightness() function is called to set the brightness of the LEDs.

In the loop() function, the current time is read from the system clock using the hour(), minute(), and second() functions. The position of the hour_hand is calculated based on the current hour and minute. If the current hour is greater than or equal to 12, the hour_hand is set to the current hour minus 12 multiplied by 5, plus the hour offset. Otherwise, the hour_hand is set to the current hour multiplied by 5, plus the hour offset.

If mirror_hands is set to true, the orientation of the LED ring is inverted, so the hour_hand, minute_hand, and second_hand are opposite to normal.

The setup() function does the following:

Initializes the serial communication with a baud rate of 115200.
Creates a WiFiManager instance which will allow the ESP8266 to act as an access point and prompt the user to enter the credentials for their WiFi network. This will be done only once, since the credentials will be stored in the device's memory.
Connects the ESP8266 to the internet by calling wifiManager.autoConnect(). This function will block the execution until the ESP8266 has successfully connected to the WiFi network.
Calls NTP.begin() to initialize the NtpClientLib library and set the NTP server to be used as "es.pool.ntp.org". The third argument specifies the UTC offset of the time zone, which is -8 in this case (for Pacific Standard Time).
Calls NTP.setInterval() to set the interval at which the NTP server will be queried for the current time. In this case, it is set to 63 seconds.
Calls pixels.begin() to initialize the Adafruit_NeoPixel library and pixels.setBrightness() to set the overall brightness of the LEDs to 254 out of 255.
The loop() function does the following:

Reads the current minute and hour from the system clock using the minute() and hour() functions provided by the Arduino Time library.
Calculates the position of the hour hand and the minute hand based on the current hour and minute values. The calculation takes into account the fact that there are 12 hours on a clock face and 60 minutes in an hour, so each hour mark is spaced 5 LEDs apart (since there are 60 LEDs in total).
If the mirror_hands flag is set to true, the code adjusts the position of the hands so that they are mirrored or flipped along the horizontal axis. This is useful if the NeoPixel ring is wired in the opposite direction or orientation.
Draws the hands on the clock by setting the colors of the appropriate LEDs using the pixels.setPixelColor() function and then displaying them using the pixels.show() function. It also prints out some debug information to the serial console using Serial.printf().
Overall, this code uses the ESP8266 WiFi module, an LED ring, and the Arduino Time library to create a clock that automatically sets the time from an NTP server and displays it on the LED ring. The clock also has an option to mirror the hands for different wiring configurations.
