# PetTutor-SDK-Demos
This is a set of demo applications to help anyone jump start their development for the Pet Tutor animal training device.

# Prerequisites To Accessory Development:
The Pet Tutor SDK currently uses Punch Through Design's Light Blue Bean to allow of an open source solution to developing for the device. To learn more about the Bean and how to setup their software (required before development) go to:

https://punchthrough.com/bean/getting-started-osx/ (OSX Development Install Guide)
https://punchthrough.com/bean/getting-started-windows/ (Windows Development Install Guide)
https://punchthrough.com/bean/ (general info)

# Accessory Development
Accessories are easily developed by programming the Light Blue Beans. These accessories can interface with the Pet Tutor feeder through the free Pet Tutor Blu mobile app. https://itunes.apple.com/us/app/pettutor-blu/id934260904?mt=8 Unfortunately there is no way to achieve direct bean to bean communicaton so an intermediate communication system has been built into our application.

The process is simple: 1) Build an accessory, 2) Include the code to trigger the feeder, 3) Use the Pet Tutor app to connect your accessory to the Feeder device. 

You can also submt your .hex file to us at: tech [at] smartanimaltraining  com and we will post it on our mini-app store for free. This allows other Makers to use your ardunio apps.

# Triggering a Feed Cycle from the Arduino:

```c
Serial.write("CMD-ACCESSORY-FEED");
```

You can also trigger the feed command through the scratch banks with:

```c
Bean.setScratchNumber(5, 1);
```

# iOS/OSX Applicaiton Development
Currently you can build iOS and OSX applications to trigger feed cycles directly to the feeder. This allows for a mobile phone or BLE supported laptop to communicate with the feeder. 

You must first include the Punch Through Design Bean SDK in your app:
https://github.com/PunchThrough/Bean-iOS-OSX-SDK

Then setup and detect the Bean devices (please review our iOS code for a jump start on this!)

Then to trigger a feed via iOS/OSX:
```objective-c
[bean sendSerialString:@"CMD-FEED"];
```
When the feeder receives the command it will issue an ACK! message back to the sender.


You can also trigger a feed command via the scratch bank registers on the device. We reserved Scratch Bank 5 on feeder for feed commands. If you set Scratch Bank 5 to a value of 1 the feeder will cycle. You can then read scratch bank 5 to see if the feeder acknowledged the command. A value of 2 is the same as receiving a ACK! serial message from the feeder.

```objective-c
int feedValue = 1;
[selectedBean setScratchBank:5 data:[NSData dataWithBytes:&feedValue length:sizeof(feedValue)]];
```

# Other Platforms
Android is the big request and we are currently working on. Punch Through Design currently has a Pre-Release SDK and an Unofficial SDK available for development. We're working to develop a set of demo applications for you to jump start your Pet Tutor development. As soon as those are available we'll update them here and let the community know!

Windows requires 8.1+ and currently can only be used for developing accessories and not windows applications.

# Questions? Concerns? Contact us today!

http://pettutor.biz




