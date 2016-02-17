# Stusz JS-SDK DOCUMENT & DEMO

## Overview

Stusz JS-SDK (JavaScript SDK) is a Stusz·APP-based WebAPP development toolkit provided by the StuszTeam for Stusz·APP-based WebAPP developers.

Through the Stusz JS-SDK, WebAPP developers can easily use native mobile features including getting user information, pulish topics, reply topics, browse topics detail and location from within Stusz. Developers may also provide Stusz users with a better WebAPP user experience by directly tapping into Stusz-specific features such as sharing, QR code scanning, images preview and calling WeChat payments.

This document describes how to use the Stusz JS-SDK and contains relevant precautions for Stusz·APP-based WebAPP developers.

## Steps for Using the JS-SDK

#### Step 1: Register an Stusz account
Using iPhone or Android moblie phone download Stusz·APP with latest version: http://app.stusz.com

Personal developers please register in Stusz·APP.

Organization developers please contact us, we will tell you how to register: hy@stusz.com

#### Step 2: Import the Stusz JS Library File
Import the following JS library file in the page where the Stusz JS API is to be called: 
```
http://www.stusz.com/app/bridge/StuszJS.js.
```

#### Step 3: Shelter alert function for avoid special BUG
All pages requiring the code must be add between `<head>` and `</head>`.
```
<script> 
window.s_alert = window.alert;   //临时保存 
    window.alert = function(str) 
        { 
                return; 
                //什么事也不做，等于屏蔽了它 
        } 
        window.alert( "已无法弹出"); 
        alert( "已无法弹出"); 
        //window.alert   =   window.s_alert; 
		//若需恢复执行上行即可
</script>
```

#### Step 4: Calling Stusz JS
All pages requiring the code must be add between `<body>` and `</body>`.
```
connectAppbymeJavascriptBridge(function(bridge){
                               
    bridge.initShake(3000,function(){
        alert('2.0 Yaoyiyao');
    });
      
    bridge.setShareCallBack(function(data){
        alert(data.errInfo);
    });
                               
    bridge.setScanCallBack(function(data){
        alert(data.errInfo + ' ' +data.url);
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
