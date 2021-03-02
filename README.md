# Intro
    
    VMware on a Raspberry Pi 4 (ESXi Install)

# What do you need?
    
    1. Raspberry Pi 4 (4GB or 8GB)
    2. SD card (16GB or smaller) (for RPI UEFI firmware)
    3. A small USB drive: (16GB or smaller) (for ESXI boot)
    4. A big USB/SSD drive: (128GB or larger) (For storage)
    5. Raspberry Pi Imager: https://www.raspberrypi.org/software/
    6. Download the latest firmware https://github.com/raspberrypi/firmware/archive/master.zip
    7. Download the latest community firmware https://github.com/pftf/RPi4/releases/download/v1.20/RPi4_UEFI_Firmware_v1.20.zip
    8. Download ESXI on ARM edition https://flings.vmware.com/esxi-arm-edition
    9. Download Rufus, https://rufus.ie/

# Update your Raspberry Pi
    
    UPDATE COMMANDS:
    $ sudo rpi-eeprom-update
    $ sudo rpi-eeprom-update -a

# Get your SD Card ready for VMWare
    
    1. Format your SD card as FAT32
    2. Extract firmware-master.zip from earlier
    3. Delete all 4 of the kernel WinImage files after extraction completes
    4. Copy the boot directory contents to the SD card
    5. Extract RPi4_UEFI_Firmware_v1.20.zip from earlier
    6. Copy everything within RPi4_UEFI_Firmware_v1.20 to the SD card – Overwrite existing files when prompted If you have the 4GB Raspberry Pi, open config.txt and add the following to a new line at the end of the file (no spaces): gpu_mem=16

# Install VMWare ESXi on your Raspberry Pi

    Using Rufus write the ISO to the smaller USB drive
    
    1. Open the tool
    2. Select the ISO
    3. Select your USB drive (The one you want to use as the installer)
    4. Create the image
    
    Now insert your USB drive into your Pi

# Setup booting

    1. Insert both your newly created USB installer drive and the blank USB drive into the Raspberry Pi
    2. Ensure the HDMI cable and keyboard are also connected
    3. Connect the USB-C power
    4. Hit the ESC key until the UEFI loads
    5. Navigate to Boot Manager
    6. Select your USB drive with the installation files
    7. Navigate to Boot Maintenance Manager > Boot Options > Change Boot Order
    8. Hit enter
    9. Highlight your USB drive with the up and down arrows
    10. Use the + key to move the USB drive to the top of the list
    11. Once it’s at the top, hit enter to complete
    12. F10 to save
    13. Y to confirm
    14. Hit ESC x3
    15. Then navigate down to Continue
    16. Hit Enter and ESXi will load!
    
    Now you can login to the ESXi host on the IP address displayed on the screen (if you have DHCP running on your network) or set a static IP as normal.


# ESXi installation
    
    1. Quickly hit the SHIFT and O (letter O) key at the same time
    2. At the bottom of the screen, append to the existing text: autoPartitionOSDataSize=8192
        This will ensure that only 8GB of the USB drive is used for the ESXi installation. We can use the rest for a datastore, more on that later
    3. Hit enter to continue
    4. Follow the prompts as you would for any other ESXi installation
    5. Ensure you select the correct device to install ESXi onto
        Congratulations, you now have a functioning copy of ESXi running on your Raspberry Pi!
    6. Connect a Network cable and remove the USB installer drive

# Create your first VM!!

# Add more storage

    From the local host web GUI
    1. Host > Actions > SSH Console
    2. Accept the fingerprint <Yes>
    3. Enter the server/host password <enter>
    4. $ /ect/init.d/usbarbitrator stop <enter>
    5. $ chkconfig usbarbitrator off <enter>
