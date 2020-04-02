# azure-iot-sphere
Azure Sphere DevKit


Using VS Code with the Azure Sphere SDK for Window
(need to install RTA - https://docs.microsoft.com/en-us/azure-sphere/install/development-environment-windows#real-time-capable-application-development)



# Installation & Initial setup

## Creating an Azure Sphere Tenant & Claim device
https://docs.microsoft.com/en-us/azure-sphere/install/overview

```
C:\Users\mimarusa\Documents>azsphere tenant create --name "MMA IOT X"
warn: You have logged in with the following account:
warn: michal.marusan@gmail.com (e6b397b8-59fc-4ff7-bcc5-f01010d32672)
warn: Do you want to use this account to create a new Azure Sphere tenant using the attached device?
warn: You cannot change the tenant name 'MMA IOT X' once it has been created.
Enter 'yes' to continue. Enter anything else to exit.
> yes
Created a new Azure Sphere tenant:
 --> Tenant Name: MMA IOT X
 --> Tenant ID:   0f8a18fb-b1a9-4a93-8150-cde69cbd4186
Selected Azure Sphere tenant 'MMA IOT X' as the default.
You may now wish to claim the attached device into this tenant using 'azsphere device claim'.
```

## Device Claim
```
C:\Users\mimarusa\Documents>azsphere device claim
Claiming device.
Successfully claimed device ID '0784E8E6F13E6ADAEF3D80BF674868E6594595C46E17581977D10099C8841CD8DC734E4389D18E504B202874A3205596D270E77C38FAAE263315198DC543B3B9' into tenant 'MMA IOT X' with ID '0f8a18fb-b1a9-4a93-8150-cde69cbd4186'.

```

## Update device with Recovery
```
C:\Users\mimarusa\Documents>azsphere device show-deployment-status
Your device is running Azure Sphere OS version 19.05.
The Azure Sphere Security Service is targeting this device with Azure Sphere OS version 20.03.
warn: Your device is running an older Azure Sphere OS version (19.05). It has not yet started receiving the available update to version 20.03.
warn: Your device is not connected to Wi-Fi. Your device may be connected via Ethernet. If not, please check the Wi-Fi configuration on your device and try again.
Go to aka.ms/AzureSphereUpgradeGuidance for further advice and support.

C:\Users\mimarusa\Documents>azsphere device recover
Downloading recovery images...
Download complete.
Starting device recovery. Please note that this may take up to 10 minutes.
Board found. Sending recovery bootloader.
Erasing flash.
Sending 17 images. (5339104 bytes to send)
Sent 1 of 17 images. (5337128 of 5339104 bytes remaining)
Sent 2 of 17 images. (5305692 of 5339104 bytes remaining)
Sent 3 of 17 images. (5202952 of 5339104 bytes remaining)
Sent 4 of 17 images. (5202560 of 5339104 bytes remaining)
Sent 5 of 17 images. (4932580 of 5339104 bytes remaining)
Sent 6 of 17 images. (4916672 of 5339104 bytes remaining)
Sent 7 of 17 images. (4896732 of 5339104 bytes remaining)
Sent 8 of 17 images. (2405632 of 5339104 bytes remaining)
Sent 9 of 17 images. (832532 of 5339104 bytes remaining)
Sent 10 of 17 images. (807956 of 5339104 bytes remaining)
Sent 11 of 17 images. (721728 of 5339104 bytes remaining)
Sent 12 of 17 images. (123492 of 5339104 bytes remaining)
Sent 13 of 17 images. (57744 of 5339104 bytes remaining)
Sent 14 of 17 images. (41164 of 5339104 bytes remaining)
Sent 15 of 17 images. (32768 of 5339104 bytes remaining)
Sent 16 of 17 images. (16384 of 5339104 bytes remaining)
Sent 17 of 17 images. (0 of 5339104 bytes remaining)
Finished writing images; rebooting board.
Device ID: 0784E8E6F13E6ADAEF3D80BF674868E6594595C46E17581977D10099C8841CD8DC734E4389D18E504B202874A3205596D270E77C38FAAE263315198DC543B3B9
Device recovered successfully.
```


Result:
```
C:\Users\mimarusa\Documents>azsphere device show-deployment-status
Your device is running Azure Sphere OS version 20.03.
The Azure Sphere Security Service is targeting this device with Azure Sphere OS version 20.03.
Your device has the expected version of the Azure Sphere OS: 20.03.
```


## Enable Development
```
C:\Users\mimarusa\Documents>azsphere device enable-development
Device ID: '0784E8E6F13E6ADAEF3D80BF674868E6594595C46E17581977D10099C8841CD8DC734E4389D18E504B202874A3205596D270E77C38FAAE263315198DC543B3B9'
Downloading device capability configuration.
Application updates have already been disabled for this device.
Enabling application development capability on attached device.
Applying device capability configuration to device.
The device is rebooting.
Installing debugging server to device.
Deploying 'C:\Program Files (x86)\Microsoft Azure Sphere SDK\DebugTools\gdbserver.imagepackage' to the attached device.
Image package 'C:\Program Files (x86)\Microsoft Azure Sphere SDK\DebugTools\gdbserver.imagepackage' has been deployed to the attached device.
Application development capability enabled.
Successfully set up device for application development, and disabled application updates.
(Device ID: '0784E8E6F13E6ADAEF3D80BF674868E6594595C46E17581977D10099C8841CD8DC734E4389D18E504B202874A3205596D270E77C38FAAE263315198DC543B3B9')

```

## Setup WiFi
https://docs.microsoft.com/en-us/azure-sphere/install/configure-wifi

Result:
```
C:\Users\mimarusa\Documents>azsphere device wifi show-status
SSID                : Erik
Configuration state : enabled
Connection state    : connected
Security state      : psk
Frequency           : 2412
Mode                : station
Key management      : WPA2-PSK
WPA State           : COMPLETED
IP Address          : 192.168.1.27
MAC Address         : 00:02:b5:03:53:9c
```



## Setup IOT Hub
Create IOT Hub and DPS
download certificate
```
C:\Users\mimarusa\Documents>azsphere tenant download-CA-certificate --output CAcertificate.cer
Saving the CA certificate to 'C:\Users\mimarusa\Documents\CAcertificate.cer'.
Saved the CA certificate to 'CAcertificate.cer'.
```

validate certificate
```
C:\Users\mimarusa\Documents>azsphere tenant download-validation-certificate --output ValidationCertification.cer --verificationcode XXXXXXX
Saving the validation certificate to 'C:\Users\mimarusa\Documents\ValidationCertification.cer'.
Saved the validation certificate to 'ValidationCertification.cer'.

```