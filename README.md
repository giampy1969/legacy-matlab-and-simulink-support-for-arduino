# legacy-matlab-and-simulink-support-for-arduino
MATLAB&reg; class and Simulink&reg; blocks for communicating with an Arduino board

NOTE #1: THIS PACKAGE (formerly known as "Arduino IO Package") IS NO LONGER SUPPORTED!
Instead of this package, use one of the OFFICIAL Arduino support packages that are developed and supported by MathWorks:
- MATLAB Support Package for Arduino Hardware: Interactively read, write, and analyze data from Arduino sensors
http://www.mathworks.com/hardware-support/arduino-matlab.html
- Simulink Support Package for Arduino Hardware: Develop algorithms that run standalone on your Arduino
http://www.mathworks.com/hardware-support/arduino-simulink.html

Try to use this legacy package ONLY IF you have already verified that the official packages do not work for you.
Typically this is when one of the following is true:
- You are using MATLAB R2013b or earlier (but not earlier than R2011a).
- You are using unsupported Arduino clones which you have verified that do not work with the official packages.

NOTE #2: (REMINDER): YOU CANNOT, ABSOLUTELY CANNOT, BUILD ANY EXECUTABLE FROM A SIMULINK MODEL WITH THIS PACKAGE!!
Attempting to do so will result in an ERROR saying that msfun_arduino_io_setup.tlc does not exist.
This happens bacause this package is a TETHERED-ONLY solution in which a MATLAB object exchanges messages with a pre-compiled Arduino Script.
If you want to do build executables from Simulink models you need to use the official Simulink support package for Arduino.

[![View legacy-matlab-and-simulink-support-for-arduino on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://www.mathworks.com/matlabcentral/fileexchange/32374-legacy-matlab-and-simulink-support-for-arduino)

Sample usage:
------------------

%-- connect to the board
a = arduino('COM9')

%-- specify pin mode
a.pinMode(4,'input');
a.pinMode(13,'output');

%-- digital i/o
a.digitalRead(4) % read pin 4
a.digitalWrite(13,0) % write 0 to pin 13

%-- analog i/o
a.analogRead(5) % read analog pin 5
a.analogWrite(9, 155) % write 155 to analog pin 9

%-- serial port
a.serial % get serial port
a.flush; % flushes PC's input buffer
a.roundTrip(42) % sends 42 to the arduino and back

%-- servos
a.servoAttach(9); % attach servo on pin #9
a.servoWrite(9,100); % rotates servo on pin #9 to 100 degrees
val=a.servoRead(9); % reads angle from servo on pin #9
a.servoDetach(9); % detach servo from pin #9

%-- encoders
a.encoderAttach(0,3,2) % attach encoder #0 on pins 3 (pin A) and 2 (pin B)
a.encoderRead(0) % read position
a.encoderReset(0) % reset encoder 0
a.encoderStatus; % get status of all three encoders
a.encoderDebounce(0,12) % sets debounce delay to 12 (~1.2ms)
a.encoderDetach(0); % detach encoder #0

%-- adafruit motor shield (with AFMotor library)
a.motorRun(4, 'forward') % run motor forward
a.stepperStep(1, 'forward', 'double', 100); % move stepper motor

%-- close session
delete(a)

Some slides and examples related to this package can be found here:
https://www.mathworks.com/matlabcentral/fileexchange/27843

Finally, more detailed info about use and troubleshooting can be found in the readme.txt file contained in this submission.
