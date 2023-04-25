
[![LiaScript](https://raw.githubusercontent.com/LiaScript/LiaScript/master/badges/course.svg)](https://liascript.github.io/course/?https://raw.githubusercontent.com/Mr-Nair/Hiwi-Arduino/main/Guide.md)

# Guide For Raspberry Pi - Arduino Interaction  
![Into](Images\Arduino_Uno.jpg "")

## 1. Prepare And Save Script

Prepare your Arduino Script (**in ".ino" format**) in the programming software of your choosing. Rename the script with a unique name and save it in a new folder with the same name. 

![Step1.1](Images\GStep1.2.png "")

> In this example:    
>
> Programming Software: VS Code
>
> Folder Path: “E:\OneDrive\Desktop\**GuideFolder**” 
>
> File Name: "**GuideFolder.ino**"

![Step1.2](Images\GStep1.3.png "")

![Step1.3](Images\GStep1.1.png "")

## 2. Upload To Raspberry Pi

* Connect to Dr Jacob’s Raspberry Pi 3+’s Wi-Fi Network. (**Password:"learningwithdoctor"**)
* Open a new console window by: 

    * Press Win+R, then type CMD into the window and press enter.
  ![Step2](Images\GStep2.png "")  

* Enter the following command: **scp -pr [pathToYourFolder] [user]@[ipadress]:[pathToDestination]** 

    * where,

    * [pathToYourFolder] = the path to your folder which contains the script file (From step 1).
    * [user] = “student” !! WARNING case sensitive !! 
    * [ipadress] = The ip address of the raspberry (10.3.141.1).
    * [pathToDestination] = “/home/student/uploadpoint” – Please use the same path.  

> In this example:
> 
> **scp -pr** E:\OneDrive\Desktop\GuideFolder **student@10.3.141.1:/home/student/uploadpoint** 
>
> TIP: Only [pathToYourFolder]( ie. E:\OneDrive\Desktop\GuideFolder) will be different from the example, You may copy paste the rest.

![Step2.2](Images\GStep2.2.png "") 


* User can Enter **“learning”** as password when prompted. !! WARNING case sensitive !!

    * Please note that the password will not be visible while typing!

## 3. Connect To Raspberry Pi via SSH

* Enter the following command in console: **ssh [user]@[ipadress]**

    * where,

    * [user] = “student” !! WARNING case sensitive !! 
    * [ipadress] = The ip address of the raspberry (10.3.141.1).


> In this example:
> 
> **ssh student@10.3.141.1**

* User can enter **“learning”** as password when prompted. !! WARNING case sensitive !!

    * Please note that the password will not be visible while typing!

![Step3](Images\GStep3.png "")

* You are now successfully connected to the Raspberry Pi.

## 4. Find Your Folder 

You can find the folder which you have uploaded in step 2 under “**uploadpoint**” directory in the Raspberry Pi via "**cd**" command, as shown here:

![Step4](Images\GStep4.png "")

You might see other folders created by students, please don't forget to clean up YOUR FOLDER after your work. (The Raspberry Pi has limited storage) 

## 5. Check Arduino Connection

To check whether the Arduino is connected to the Raspberry Pi, enter the following command in console: **arduino-cli board list**

![Step5](Images\GStep5.png "")

It informs that the Arduino is connected to the Raspberry Pi via the ttyACM0 Port and also shows the type of the Arduino used. Here, Arduino Uno is used.

## 6. Compile Script

* Enter the following command in console: **arduino-cli compile -b [FQBN] [directory]** 

    * where,

    * [FQBN] = the Arduino type 
    * [directory] = your script directory 

> In this example:
> 
> **arduino-cli compile -b arduino:avr:uno** Guidefolder/ 

A successful compilation will look like this: 

![Step6](Images\GStep6.png "")

> If the Raspberry compiler reports an error, It is recommended to re-upload the corrected file by repeating the above steps. If you have experience, then you may use the internal editor by entering the following command: **nano [filename]** 

## 7. Upload Script To Arduino

* Enter into your Folder directory via "**cd**" command, as shown here:

![Step7.1](Images\GStep7.1.png "")

> Please note that only one user can interact with the arduino at a time!

* Enter the following command in console: **arduino-cli upload -b [FQBN] -p [Port]** 

    * where,

    * [FQBN] = the Arduino type 
    * [Port] = /dev/ttyACM0 (From Step 5) 

> In this example:
> 
> **arduino-cli upload -b arduino:avr:uno -p /dev/ttyACM0** 

Once the RPi has uploaded your script, it will replace the currently employed script with yours and you can Arduino away!

By adding “ -v” at the end of the upload command, you could have a console output to see the process.

![Step7.2](Images\GStep7.2.png "")

## 8. Remove Your Data

Please don't forget to remove your uploaded directory.

To do so, Enter the following command in console: **rm -rf uploadpoint/[YourFolderName]/**

The function is depicted here:

![Step8](Images\GStep8.png "")

> Please be careful and only delete your own data.

