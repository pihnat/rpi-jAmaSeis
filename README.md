# How to install jAmaSeis on a Raspberry Pi.

1. Ensure you have the latest version of Raspian installed (currently Buster), the system updated and your Pi connected to the internet. If you like you can change the name of your Raspberry Pi to **Seismograph** in the Raspberry Pi Configuration menu.


![screenshot](/screenshots/Name.png)

2. Now, let's download jAmaSeis.
Run the web browser Chromium on your raspi and go to the following site:

    https://www.iris.edu/hq/jamaseis/

    After entering your details you'll see options for downloading jAmaSeis for Windows 64bit, MAC and Linux. Download the Linux version. At the bottom left of Chromium's window you'll see the progress of the download.
    
![screenshot](/screenshots/Download.png)
    
    When done it'll say

    **This type of file can harm your computer. Do you want to keep jAmaSeis_1_xxxxx.sh anyway?**

    Click the **Keep** box then close your browser.

![screenshot](/screenshots/Keep.png)


3. Next, install the java serial comms library and link it. Open a Terminal window and type the following commands exactly, paying attention to case:

    sudo apt install librxtx-java
    
    sudo ln -s /usr/lib/jni/librxtxSerial.so /usr/lib/


4. Now you're ready to install jAmaSeis. Go to the folder where you downloaded jAmaSeis, usually /home/pi/Downloads   and run the script ie in the Terminal window type the following commands:

    cd /home/pi/Downloads
    
    ls
    
    sh jAmaSeis_1_xxxxx.sh

    (replace "_1_xxxxx" with the actual version of jAmaSeis you downloaded as shown by the **ls** command).

![screenshot](/screenshots/Install.png)


The installer will run in a separate window, just use the defaults for all answers.

-----------------------------------------------------------------------------------------

Notes:
1. If an icon for jAmaSeis doesn't appear on the desktop after installation go to the **Applications Menu** and under **Other** right click **jAmaSeis** and select **Add to desktop**.

    When you double click the jAmaSeis icon to run it, if a popup box asking **What do you want to do with it?** appears click Cancel, go to File Manager and under menu item **Edit** select **Preferences**. Tick the box that says **Don't ask options on launch executable file**.

![screenshot](/screenshots/DontAsk.png)


2. In jAmaSeis when you create a local station your USB data acquisition device will appear as /dev/USB0, etc.
You can also use the Raspberry Pi's serial port (pins 8 & 10 on the GPIO connector) if you have a device to connect to it.
    To use the serial port enable it first:
    - from the Applications Menu under **Preferences**, **Raspberry Pi Configuration** select the **Interfaces** tab
    - **Enable** the Serial Port and
    - **Disable** Serial Console.

![screenshot](/screenshots/Interfaces.png)

    
The Raspberry Pi's serial port will appear as /dev/ttyS0 in jAmaSeis.

3. Remember the Raspberry Pi's SD card doesn't have a high storage capacity so if you let jAmaSeis save all data from your seismograph or remote station it will eventually fill the card. Current versions of jAmaSeis allow you to set the **Max Days of Data to Keep**. Look for it in the Settings menu.
The alternative is to use external USB storage for the data files or, as in my case, I installed Raspian on a 1TB portable USB hard drive so the operating system and all data reside there (it doesn't use an SD card at all). It's a headless setup with VNC enabled. 

4. When jAmaSeis checks for updates there normally isn't a problem in downloading and installing the update. Either a pop-up box will open saying there's an update available, **Would you like to download the installer now?** or you can do it manually by going to **About** in the main menu and selecting **Check For Updates**.
But occasionally the newer version of jAmaSeis requires a newer version of java. You can check the currently installed version of java by opening a Terminal window and typing:

    java -version

    Java can be updated by typing the following commands:

    sudo apt update
    
    sudo apt install default-jdk

    However if there's been a major update of Linux then java may also have been updated and the above process probably won't work. For example jAmaSeis_1_11_0_136.sh and jAmaSeis_1_11_1_184.sh were ok with java 1.8 running under Raspian Stretch but the next update jAmaSeis_1_11_3_125.sh now requires java 11 which isn't available for Raspian Stretch. It does come preinstalled with Raspian Buster so this time you would need to do a major Raspian re-install. In my case I copied the whole jamaseisData folder using file transfer in VNC to my laptop, installed Buster from scratch using Etcher, re-installed jAmaSeis and copied the jamaseisData folder back.

