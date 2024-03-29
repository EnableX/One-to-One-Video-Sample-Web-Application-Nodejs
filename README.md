# Building a 1-to-1 Real-Time Video Chat Web App with EnableX Web Toolkit and Node.js

1-to-1 RTC Web App: EnableX Web Toolkit 

Explore a Sample Web App showcasing the utilization of EnableX platform APIs for conducting seamless 1-to-1 RTC (Real-Time Communication). This application is designed to illustrate API usage and facilitate developers in accelerating app development by hosting it on their personal devices, without the need for external servers. 

RTC Applications on the EnableX platform operate seamlessly on supported web browsers, eliminating the need for additional plugin downloads. 

This basic 1-to-1 Video Chat Application is created using HTML, CSS, Bootstrap v4.0.0-alpha.6, JavaScript, jQuery, Node V8.9.1, and EnxRtc (EnableX Web Toolkit) 

>The details of the supported set of web browsers can be found here:
https://developer.enablex.io/release-notes/#cross-compatibility

## 1. Important!

When developing a Client Application with EnxRtc.js ( present in client/js ), make sure to replace the old EnxRtc.js with updated EnxRtc.js polyfills from https://developer.enablex.io/video-api/client-api/web-toolkit/ for RTCPeerConnection and getUserMedia. Otherwise your application will not work in web browsers.


## 2. Trial

Try a quick Video Call: https://try.enablex.io/ 
Sign up for a free trial https://portal.enablex.io/cpaas/trial-sign-up/



## 3. Installation


### 3.1 Pre-Requisites

#### 3.1.1 App Id and App Key 

* Create a free account on EnableX [https://portal.enablex.io/cpaas/trial-sign-up/]
* Create your Project
* Get the App ID and App Key generated against the Project
* Clone or download this repository `git clone https://github.com/EnableX/One-to-One-Video-Sample-Web-Application-Nodejs.git --recursive`
### ![#f03c15](https://via.placeholder.com/15/f03c15/000000?text=+) Please note `--recursive` option. Repo should be cloned recursively to download `client` app. 


#### 3.1.2 SSL Certificates or Self-Signed Certificates

The Application needs to run on https. So, you need to use a valid SSL Certificate for your Domain and point your application to use them. 

However you may use self-signed Certificate to run this application locally. There are many websites to get a self-signed certificate generated for you.
* https://letsencrypt.org/
* https://www.sslchecker.com/csr/self_signed
* https://www.akadia.com/services/ssh_test_certificate.html  

The following below can also be used to create a self-signed certificate. 


Mac/Linux
```
  `cd One-to-One-Video-Sample-Web-Application-Nodejs`
  `mkdir certs`
  `sudo openssl req -x509 -newkey rsa:4096 -keyout ./certs/localhost.key -out ./certs/localhost.crt -days 10000 -nodes`
  `sudo chmod 755 ./certs/localhost.*`
```

Windows(Use Git Bash)
```
  `cd One-to-One-Video-Sample-Web-Application-Nodejs`
  `mkdir certs`
  `openssl req -x509 -newkey rsa:4096 -keyout ./certs/localhost.key -out ./certs/localhost.crt -days 10000 -nodes`
  `chmod 755 ./certs/localhost.*`
```

#### 3.1.3 Configure

Before you can run this application by hosting it locally you need to customize `server/vcxconfig.js` to meet your needs.

`nano ./server/vcxconfig.js`

```javascript 
vcxconfig.SERViCE = {
  name: "EnableX Sample Web App",     // Name of the Application [Change optional]
  version: "1.0.0",                   // Version [Change optional]
  path: "/v1",                        // Route [Default /v1]
  domain: "yourdomain.com",           // FQDN of  your hosting enviornment
  port  : "4443",                     // FQDN of  your hosting port. You need sudo permission if you want to use standard 443
  listen_ssl : true                   // SSL on/off key  [ Set always to "true" ]
};

vcxconfig.Certificate = {
    ssl_key: 	"../certs/localhost.key",            // Path to .key file or registered key
    ssl_cert: 	"../certs/localhost.crt"             // Path to .crt file or registered crt
// sslCaCerts :  ["../cert/yourdomain.ca-bundle"]    // Use the certificate CA[chain] [self signed or registered]
};

vcxconfig.SERVER_API_SERVER = {
  host: 'api.enablex.io',             // Hosted EnableX Server API Domain Name
  port: '',
};

vcxconfig.clientPath  = "../client";    // UI files location
vcxconfig.APP_ID      = "YOUR_APP_ID";  // Enter Your App ID you received from registered email
vcxconfig.APP_KEY     = "YOUR_APP_KEY"; // Enter Your App Key you have received from registered email
```

### 3.2 Build

Run `npm install --save` to build the project and the build artifacts will be stored in the `./node_modules` directory.


#### 3.2.1 Run Server

Run `node server.js` inside `server` folder to start your server. 

```
  `cd server`
  `node server.js`
```
Server started. Listening on Port 4443

#### 3.2.2 Test Video Call

* Open a browser and go to `https://localhost:4443/`. The browser should load the App. Go to -> Advanced -> Proceed to localhost
* Don't have a Room ID? Create here (create a new RoomID)
* Store the Room ID for future use or share
* Enter a username (e.g. test0)
* Join and allow access to camera and microphone when prompted to start your first webRTC call through EnableX
* Open another browser tab and enter `https://localhost:4443/`
* Enter the same roomID previously created and add a different username (test1) and click join
* Now, you should see your own video in both the tabs!


## 4 Server API

EnableX Server API is a Rest API service meant to be called from Partners' Application Server to provision video enabled 
meeting rooms. API Access is given to each Application through the assigned App ID and App Key. So, the App ID and App Key 
are to be used as Username and Password respectively to pass as HTTP Basic Authentication header to access Server API.
 
For this application, the following Server API calls are used: 
* https://developer.enablex.io/latest/server-api/rooms-route/#get-rooms - To get list of Rooms
* https://developer.enablex.io/latest/server-api/rooms-route/#get-room-info - To get information of the given Room
* https://developer.enablex.io/latest/server-api/rooms-route/#create-token - To create Token for the given Room

To know more about Server API, go to:
https://developer.enablex.io/latest/server-api/


## 5 Client API

Client End Point Application uses Web Toolkit EnxRtc.js to communicate with EnableX Servers to initiate and manage RTC Communications.  

To know more about Client API, go to:
https://developer.enablex.io/latest/client-api/
