# edgeengine-embedded-os
edgeEngine for Embedded Operating Systems (QNX)

# About:
In this document you will learn how to install and run edgeEngine on a QNX system. You will optionally be able to run 1 or 2 instances of edgeEngine running on different ports. 

# Prerequisite:
- You must have a mimik developer account
  - With a project created and you have a clientID
  - You have a developerID Token for corresponding clientID 

- 1 raspberry pi device 

- 1 Development PC 
  -Have visual studio installed with REST client extension 

- Valid QNX licence and image 

-You should already have QNX image running on raspberry pi device
 - In the instructions below we assume that we you can telnet into the system via command line
 - You must have the IP of the QNX system to do this
 - You must have the root login and password

# Instructions:

1. Take the SD-Card that has the QNX image on it and plug it into your development PC 

2. Open file explorer and view the files on SD-Card

3. Download qnx-two-edge-instances.zip 

4. Unzip the package 

5. Find and copy the entire “qnx-disk” folder to SD card. Remember the location of where you placed the folder

6. unplug SD card from the development PC and plug it into the raspberry Pi device. 

7. Boot up Raspberry Pi device    

8. telnet into running QNX system from the command line. Replace <QNX-IP> with the IP of your QNX system
```
telnet <QNX-IP>
```
9. Enter the root username of your system 

10. Enter the root password of your system 

11. Navigate to where you placed “qnx-disk” and go into /mimik folder

```
cd .../qnx-disk/mimik
```
12. From there you will see 2 folders, /instance1 and /instance2

13. Navigate into /instance1

```
cd /instance1
```

14. run start script 

```
./start.sh
```  
15. This will run edgeEngine, you should see logs printed to the screen. These are edgeEngine logs

16. On development PC, open visual studio code

17. Open the contents of the unzipped qnx-two-edge-instances.zip folder in the visual studio code

18. Open instance1.http within /local folder

19. make sure you have REST client extension installed  

20.At the top of the file you will see:
```
 @ip=
```
21. Place the IP of the QNX device after the equal sign
```
@clientId=
```
22. Place your clientID after the equal sign. You should have a client ID after creating a project in the mimik developer console 
```
@developerIdToken=
```
23. Place your developerID token after the equal sign. You should have a developer ID token after creating a project in the mimik developer console 

24. You should see the “send request” button in instance1.http in the visual studio code 
  - If you do not see this, you did not install the REST client correctly 

25. Click every “send request” button in the order they appear, this will associate your edgeEngine instance running on the QNX system with the project you created in the developer console and deploy mDebug microservice 

26. After successfully running all API calls, open a browser and navigate to the URL box

27. in the URL box place the IP address of your QNX device and the port where edgeEngine is running and the “MCM.BASE_API_PATH"to mDebug microservice. IE:
```
http://<QNX-IP>:8083/9f8241cc-ef15-42be-98ee-b6518ee3f87a/mdebug/v1/gui
```
  -Your MCM.BASE_API_PATH will be different. place yours after the port number

28. You can build your mDebug API by like below:

```
http://<QNX-IP>:<PORT-NUMBER>/<MCM.BASE_API_PATH>/gui
```
29. You can retrieve your MCM.BASE_API_PATH by making the /containers api call from instance1.http 

```
####
GET {{host}}/mcm/v1/containers
Authorization: Bearer {{edgeToken}}
```
30. Once the URL is placed in the URL box press enter to reach mDebug microservice GUI
  

# Optional:
  
To run another instance of edgeEngine in addition to the instance ran above, follow the instructions below.

1. Repeat above steps 8-13 in a new bash window. (be sure not to close or stop the instance1 window)

2. On Step 13 be sure to navigate into the/instance2 folder

```
cd /instance2
```
3. run start script: 

```
./start.sh
```
4. This will run edgeEngine, you should see logs printed to the screen. These are edgeEngine logs

5. On development PC, open visual studio code

6. Open the contents of the unzipped qnx-two-edge-instances.zip folder in the visual studio code

7. Open instance2.http within /local folder

8. make sure you have the REST client extension installed  

9. At the top of the file you will see:
```
 @ip=
```
10. Place the IP of the QNX device after the equal sign(Same as instance1)
```
@clientId=
```
11. Place your clientID after the equal sign. You should have a client ID after creating a project in the mimik developer console(Same as instance1)
```
@developerIdToken=
```
12. Place your developer ID token after the equal sign. You should have a developer ID token after creating a project in mimik developer console(Same as instance1)

13. You should see the “send request” button in instance1.http in the Visual Studio Code 

14. If you do not see this, you did not install the REST client correctly 

15. Click every “send request” button in the order they appear, this will associate your edgeEngine instance running on the QNX system with the project you created

16. You can optionally repeat steps to deploy mDebug microservice on the new instance 

NOTE:

Be sure to remember that if you run both instances of edgeEngine, you will only be able to communicate with them via specific PORT_NUMBER
  
# Resources
- Learn how to use mDebug (Video Tutorial): [mDebug Tutorial](https://vimeo.com/showcase/mimik-developer-tools)
- Try Out edgeEngine on Instruqt: [Getting Started with edgeEngine](https://play.instruqt.com/mimik/invite/cguo4srusweo) 
