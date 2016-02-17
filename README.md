# Stusz JS-SDK DOCUMENT & DEMO

## Overview

Stusz JS-SDK (JavaScript SDK) is a Stusz·APP-based WebAPP development toolkit provided by the StuszTeam for Stusz·APP-based WebAPP developers.

Through the Stusz JS-SDK, WebAPP developers can easily use native mobile features including getting user information, pulish topics, reply topics, browse topics detail and location from within Stusz. Developers may also provide Stusz users with a better WebAPP user experience by directly tapping into Stusz-specific features such as sharing, QR code scanning, images preview and calling WeChat Payment.

This document describes how to use the Stusz JS-SDK and contains relevant precautions for Stusz·APP-based WebAPP developers.

## Steps for Using the JS-SDK

#### Step 1: Register an Stusz account
Using iPhone or Android moblie phone download Stusz·APP with latest version: http://app.stusz.com

Personal developers please register in Stusz·APP.

Organization developers please contact us, we will tell you how to register: hy@stusz.com

#### Step 2: Import the Stusz JS Library File
Import the following JS library file in the page where the Stusz JS API is to be called: 
```
http://www.stusz.com/app/bridge/StuszJS.js
```

#### Step 3: Shelter alert function for avoid special BUG
All pages requiring the code must be add between `<head>` and `</head>`.
```
<script> 
window.s_alert = window.alert;
    window.alert = function(str) 
        { 
                return; 
                //Shelter
        } 
        window.alert("Can not show"); 
        alert("Can not show"); 
</script>
```
Note: If you need to use `alert` function, please replaced by `window.s_alert()`

#### Step 4: Calling Stusz JS
All pages requiring the code must be add between `<body>` and `</body>`.
```
connectAppbymeJavascriptBridge(function(bridge){
                               
    bridge.initShake(3000,function(){
        window.s_alert('2.0 Yaoyiyao');
    });
      
    bridge.setShareCallBack(function(data){
        window.s_alert(data.errInfo);
    });
                               
    bridge.setScanCallBack(function(data){
        window.s_alert(data.errInfo + ' ' +data.url);
    });
    
});
```

## Basic API

#### API for determining whether Stusz·APP environment supports
```
function StuszAppWeb(){
    if(navigator.userAgent.indexOf('Appbyme') > -1){
        window.s_alert("Stusz·APP environment");
    }else{
        window.s_alert("Not Stusz·APP");
    }
}
```

## User API

#### API for calling page of logging in
```
function login(){
    AppbymeJavascriptBridge.login(function(data){
    });
}
```

#### API for logging out present account
```
function logout(){
    AppbymeJavascriptBridge.logout(function(data){
    });
}
```

#### API for obtaining user information
API will return data in JSON. 
```
function userInfo(){
    AppbymeJavascriptBridge.getUserInfo(function(data){
	     window.s_alert(JSON.stringify(data));
    });
}
```

#### API for calling appointed user homepage
```
function userCenter(){
    AppbymeJavascriptBridge.getUserInfo(function(data){
    });
    AppbymeJavascriptBridge.userCenter(userId);  //userId is a number
}
```

## Topic API

#### API for calling appointed topic detail
```
function topicDetail(){
    AppbymeJavascriptBridge.topicDetail(529,22,1);
    //type: Uniform fill in "1"
    //topicDetail(topicId,boardId,type)
}
```

#### API for calling pulish new topic
```
function pulishTopic(){
    AppbymeJavascriptBridge.pulishTopic(function(data){
        alert(data.errInfo);
    },1,61,'1',1);
    //type: 1:Common 2:Classified 3:Vote
    //pulishTopic(callBack,type,boardId,boardName,classifyId,isTitle)
}
```

#### API for calling reply appointed topic
```
function replyTopic(){
    AppbymeJavascriptBridge.replyTopic(function(data){
         alert(data.errInfo);
    },529,36,61);
    //replyTopic(callBack,topicId,referenceTopicId,boradId)
}
```

## Sharing API

#### API for obtaining share status for "Share" and customizing sharing contents
```
function share(){
    AppbymeJavascriptBridge.share("Sharing title", "Sharing description", "Sharing link", function(data){
         window.s_alert(data.errInfo);
    });
}
```

## Intelligent API

#### API for obtaining geographic location
```
function getLocation(){
    AppbymeJavascriptBridge.getLocation(function(data){
         window.s_alert(JSON.stringify(data));
    });
}
```

#### API for obtaining equipment information
```
function getVersion(){
    AppbymeJavascriptBridge.getVersion(function(data){
        window.s_alert(JSON.stringify(data));
    });
}
```

#### API for obtaining encryption mode
```
function encrypt(str){
    AppbymeJavascriptBridge.encrypt(function(data){
        alert(JSON.stringify(data));
    },str);
}
```

## Other API

#### API for calling images preview
```
function imagePreview(){
    var imageArray=['http://www.stusz.com/data/attachment/forum/201512/21/184924rdpmjmmpxz75pjh5.jpeg','http://www.stusz.com/data/attachment/forum/201512/21/184811dotgtrtutrug7v0u.jpg'];
    //imagePreview(imageArray, position);
    AppbymeJavascriptBridge.imagePreview(imageArray,1);
}
```

#### API for closing appointed webpage
```
function closeActivity(){
    AppbymeJavascriptBridge.closeActivity();
}
```

#### API for calling WeChat Payment
Key Account Only, please contact: 
```
hy@stusz.com, Mr. Huang
```

## Sample code & Demo webpage
Demo webpage URL: 
```
http://www.stusz.com/app/bridge/demo.html
```
Sample code in Github: 
```
https://github.com/iStusz/js
```

## Legal Statement
Shenzhen Stusz Technology Co.,Ltd. All Rights Reserved.
