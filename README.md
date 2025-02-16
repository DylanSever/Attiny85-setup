# Attiny85-setup
This is an updated solution to help fix any issues with the outdated / loss of support URLs, depositories, and boards for the ATTINY 85 and arduino IDE
Trial & Error:
Out of Date?:
http://digistump.com/package_digistump_index.json
when placed in the Arduino Ide preferences (File >> preferences >> additional boards manager URLs) it would fail to download or install. When looking up the digistall or attiny85 board it would not come up.

Successful:
https://raw.githubusercontent.com/digistump/arduino-boards-index/master/package_digistump_index.json 
How to Build a Rubber Ducky USB With Arduino Using a Digispark Module | Arduino | Maker Pro

Drivers: 
https://objects.githubusercontent.com/github-production-release-asset-2e65be/28220127/e05aa054-9020-11e6-9de6-61504f7ad160?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=releaseassetproduction%2F20250216%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250216T021425Z&X-Amz-Expires=300&X-Amz-Signature=f09d62a19eecd887433825ecb5e95e05b753e26022fb72682b0a312846e74469&X-Amz-SignedHeaders=host&response-content-disposition=attachment%3B%20filename%3DDigistump.Drivers.zip&response-content-type=application%2Foctet-stream  

Putting it all together:
First you want to give the Arduino IDE the URLs to be able to pull the boards that the ATTINY 85 needs to access. To do this go to File >> preferences >> additional boards manager URLs. Click the icon on the far right of where you can paste a link. Then make sure to include the following links separated by commas. Also, I recommend installing the drivers onto the device you are planning to test/run this on. I encountered difficulties of the ATTINY 85 timing out before I installed the drivers.
Links: 
https://github.com/LilyGO/DigiSpark-ATtiny85-driver-install/blob/master/Digistump.Drivers.zip
https://github.com/micronucleus/micronucleus/blob/v1.06/micronucleus-t85_winDriver.zip
https://raw.githubusercontent.com/digistump/arduino-boards-
	Next, you will want to choose the boards necessary for operating the ATTINY 85. To do this select Tools >>Board >>Boards Manager. Look up Digistump and then install the Digistump AVR Boards by Digistump. To be safe make sure you download the 1.6.7 version of the board.
	Then, go to  Tools >>Board>> Digistump AVR Boards>> DIgispark (Default – 16.5mhz). Tools >>Programmer>> Micronucleus. 
Writing the code:
Here is a sample we used where the rubber ducky will pull up Never Gonna Give You Up by Rick Astley when plugged in:
#include "DigiKeyboard.h"
void setup() {
  //empty
}
void loop() {
  DigiKeyboard.delay(2000);
  DigiKeyboard.sendKeyStroke(0);
  DigiKeyboard.sendKeyStroke(KEY_R, MOD_GUI_LEFT);
  DigiKeyboard.delay(600);
  DigiKeyboard.print("https://youtu.be/dQw4w9WgXcQ?t=43s");
  DigiKeyboard.sendKeyStroke(KEY_ENTER);
  DigiKeyboard.delay(5000);
  DigiKeyboard.sendKeyStroke(KEY_F11);
  for (;;) { /*empty*/
  
Here is our code to write a file to a location when plugged in:
/*

*\

Uploading and Running:
	Many sources recommend to go to Sketch>>Uploading Using Programmer when ready to upload the code to run the script with the ATTINY 85.  Although, personally I ran into code errors when following that step. I recommend just hitting the upload button in the Arduino IDE menu. Once pressed, it will begin the process and prompt you to insert the device after a couple of seconds. Then insert the device and give it about 10 seconds to finish the upload process. Upon completion it will run the script. For future uses you can insert the device and it will recognize the device and run the uploaded script.

Expected Output:
Sketch uses 2798 bytes (46%) of program storage space. Maximum is 6012 bytes.
Global variables use 124 bytes of dynamic memory.
Running Digispark Uploader...
Plug in device now... (will timeout in 60 seconds)
> Please plug in the device ...
> Press CTRL+C to terminate the program.
> Device is found!
connecting: 16% complete
connecting: 22% complete
connecting: 28% complete
connecting: 33% complete
> Device has firmware version 1.6
> Available space for user applications: 6012 bytes
> Suggested sleep time between sending pages: 8ms
> Whole page count: 94  page size: 64
> Erase function sleep duration: 752ms
parsing: 50% complete
> Erasing the memory ...
erasing: 55% complete
erasing: 60% complete
erasing: 65% complete
>> Eep! Connection to device lost during erase! Not to worry
>> This happens on some computers - reconnecting...
>> Reconnected! Continuing upload sequence...
> Starting to upload ...
writing: 70% complete
writing: 75% complete
writing: 80% complete
> Starting the user app ...
running: 100% complete
>> Micronucleus done. Thank you!




Demo:
https://youtube.com/shorts/F8wKizGJy9o?si=PS8Zoj1ZPRkeeHFM
