# Using the ADHD VM On Apple Silicon
## Downloading the Virtual Machine
1. Access the Class Virtual Machine at https://introclassjs.s3.us-east-1.amazonaws.com/WINADHD04_23.7z.  

**NOTE** This is a large download and may take a considerable amount of time depending on your network connection!

## Installing UTM
1. The UTM installation is very straightforward and you can read more about it here (https://docs.getutm.app/installation/macos/).  UTM can be installed directly from the AppStore, via HomeBrew or via GitHub (https://github.com/utmapp/UTM/releases/latest/download/UTM.dmg).  Note that the version hosted on Github is free and Open Source. 
2. After downloading the installer, double-click the DMG file and follow the installer directions. 
## Convert the ADHD VM 
1. Unzip the `WINADHD04_23.7z` file. 
2. If you don't have QEMU installed, please install it via HomeBrew on macOS.  (For more information about HomeBrew, please visit https://brew.sh/ for more details.)
   `$ brew install qemu`
3. Identify the `.vmdk` file in your VMware image directory. This is the disk image that you'll convert to a format compatible with UTM.
4. Use the `qemu-img` command to convert the `.vmdk` file to a QCOW2 file, which is compatible with UTM.  Make sure to edit the paths to reflect your download and unzip locations.
   `$ qemu-img convert -O qcow2 path/to/WINADHD-disk1.vmdk path/to/WINADHD-disk1.qcow2`
5. Launch UTM and click the `+` button to create a new virtual machine.
6. Choose **Emulate** to ensure functionality with x86/x64 virtual machines. Click **Continue**
7. For **Operating System**, click **Custom** > **Other**, then **Continue**. 
8. Change **Boot Device** to `None` and click **Continue**
9. For **Architecture**, choose `x86_64`, **System** as `Standard PC`, **Memory** 4096, **CPU Cores** 2.  Click **Continue**. 
10. Set **Storage Size** to 50GB. Click **Continue**. 
11. For **Shared Directory**, click **Continue**. 
12. At the **Summary** screen, choose a name, and select **Open VM Settings** before clicking **Save**. 
13. From the **Settings** window that opens, under the **Drives** section, select **New** > **Import** and then choose the `.qcow2` file you just created. You can then go back to the **Settings** menu under drives and click on the empty IDE entry and then **Delete**. 

![Alt text](https://github.com/n3tl0kr/BlueTeam/blob/main/assets/utm_1.png)

14. Note that the first boot may be very slow.  After the desktop has stabilized, click the **Drive Options** button at the top of the **UTM** windows and select **Install Windows Guest Tools** 

![Alt text](https://github.com/n3tl0kr/BlueTeam/blob/main/assets/utm_2.png)

### References
https://www.antisyphontraining.com/john-strand-training-lab-download-instructions/
https://docs.getutm.app/installation/macos/
