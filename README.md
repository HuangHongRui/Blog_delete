# JavaScript代码收录-筆記
> 客户端检测
>> 客戶端能力檢測
>
```
//检测浏览器下测试任何对象的某个特性是否存在——不保证永远可靠
//该方法目前(书中)：可靠
// 作者： Peter Michaux
function isHostMethod(object, property) {
  var t = typeof object[property];
  return t == 'function' ||
    (!!(t == 'object' && object[property])) ||
    t == 'unknown';
}
result = isHostMethod(xhr, "open");
result = isHostMethod(xhr, "foo");
```
>>一次性檢測
>
```
var hasNsPlug = !!(navigator.plugins && navigator.plugins.length);
// 確定瀏覽器是否支持Netscape風格的插件
```
```
var hasDOM1 = !!(document.getElementById && document.createElement && document.getElementsByTagName);
//確定瀏覽器是否具有DOM1級規定的能力
```
>>怪癖檢測(bug檢測)
>
```
var hasDontEnumQuirk = function() {
  for (var prop in o) {
    if (prop == "toString") {
      return false;
    }
  }
  return true;
}()
```
>>用戶代理檢測
>
```
var client=function(){

   var engine={    //呈现引擎
      trident:0,
      gecko:0,
      webkit:0,
      khtml:0,
      presto:0,
      ver:null     //具体的版本号
   };
   var browser={   //浏览器
      ie:0,
      firefox:0,
      safari:0,
      konq:0,
      opera:0,
      chrome:0,
      ver:null     //具体的版本号
   };
   var system={    //操作系统
      win:false,
      mac:false,
      x11:false
   };

   var ua=navigator.userAgent;
   if(/AppleWebKit\/(\S+)/.test(ua)){        //匹配Webkit内核浏览器（Chrome、Safari、新Opera）
      engine.ver=RegExp["$1"];
      engine.webkit=parseFloat(engine.ver);
      if(/OPR\/(\S+)/.test(ua)){             //确定是不是引用了Webkit内核的Opera
         browser.ver=RegExp["$1"];
         browser.opera=parseFloat(browser.ver);
      }else if(/Chrome\/(\S+)/.test(ua)){    //确定是不是Chrome
         browser.ver=RegExp["$1"];
         browser.chrome=parseFloat(browser.ver);
      }else if(/Version\/(\S+)/.test(ua)){   //确定是不是高版本（3+）的Safari
         browser.ver=RegExp["$1"];
         browser.safari=parseFloat(browser.ver);
      }else{                                 //近似地确定低版本Safafi版本号
         var SafariVersion=1;
         if(engine.webkit<100){
            SafariVersion=1;
         }else if(engine.webkit<312){
            SafariVersion=1.2;
         }else if(engine.webkit<412){
            SafariVersion=1.3;
         }else{
            SafariVersion=2;
         }
            browser.safari=browser.ver=SafariVersion;
      }
   }else if(window.opera){                 //只匹配拥有Presto内核的老版本Opera 5+(12.15-)
      engine.ver=browser.ver=window.opera.version();
      engine.presto=browser.opera=parseFloat(engine.ver);
   }else if(/Opera[\/\s](\S+)/.test(ua)){  //匹配不支持window.opera的Opera 5-或伪装的Opera
      engine.ver=browser.ver=RegExp["$1"];
      engine.presto=browser.opera=parseFloat(engine.ver);
   }else if(/KHTML\/(\S+)/.test(ua)||/Konqueror\/([^;]+)/.test(ua)){
      engine.ver=browser.ver=RegExp["$1"];
      engine.khtml=browser.konq=parseFloat(engine.ver);
   }else if(/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){ //判断是不是基于Gecko内核
      engine.ver=RegExp["$1"];
      engine.gecko=parseFloat(engine.ver);
      if(/Firefox\/(\S+)/.test(ua)){                //确定是不是Firefox
         browser.ver=RegExp["$1"];
         browser.firefox=parseFloat(browser.ver);
      }
   }else if(/Trident\/([\d\.]+)/.test(ua)){         //确定是否是Trident内核的浏览器（IE8+）
      engine.ver=RegExp["$1"];
      engine.trident=parseFloat(engine.ver);
      if(/rv\:([\d\.]+)/.test(ua)||/MSIE ([^;]+)/.test(ua)){   //匹配IE8-11+
         browser.ver=RegExp["$1"];
         browser.ie=parseFloat(browser.ver);
      }
   }else if(/MSIE ([^;]+)/.test(ua)){               //匹配IE6、IE7
      browser.ver=RegExp["$1"];
      browser.ie=parseFloat(browser.ver);
      engine.ver=browser.ie-4.0;                    //模拟IE6、IE7中的Trident值
      engine.trident=parseFloat(engine.ver);
   }

   var p=navigator.platform;                        //判断操作系统
   system.win=p.indexOf("Win")==0;
   system.mac=p.indexOf("Mac")==0;
   system.x11=(p.indexOf("X11")==0)||(p.indexOf("Linux")==0);
   if(system.win){
      if(/Win(?:dows )?([^do]{2})\s?(\d+\.\d+)?/.test(ua)){
         if(RegExp["$1"]=="NT"){
            system.win = ({
               "5.0" : "2000",
               "5.1" : "XP",
               "6.0" : "Vista",
               "6.1" : "7",
               "6.2" : "8",
               "6.3" : "8.1",
               "10" : "10"
            })[RegExp["$2"]] || "NT";
         }else if(RegExp["$1"]=="9x"){
            system.win="ME";
         }else{
            system.win=RegExp["$1"];
         }
      }
   }

   return {
      ua:ua,          //用户浏览器Ua原文
      engine:engine,  //包含着用户浏览器引擎（内核）信息
      browser:browser,//包括用户浏览器品牌与版本信息
      system:system   //用户所用操作系统及版本信息
   };

}();
```
```
var client=function(){

   var engine={    //呈现引擎
      trident:0,
      gecko:0,
      webkit:0,
      khtml:0,
      presto:0,
      ver:null     //具体的版本号
   };
   var browser={   //浏览器
      ie:0,
      firefox:0,
      safari:0,
      konq:0,
      opera:0,
      chrome:0,
      ver:null     //具体的版本号
   };
   var system={    //操作系统
      win:false,
      mac:false,
      x11:false
   };

   var ua=navigator.userAgent;
   if(/AppleWebKit\/(\S+)/.test(ua)){        //匹配Webkit内核浏览器（Chrome、Safari、新Opera）
      engine.ver=RegExp["$1"];
      engine.webkit=parseFloat(engine.ver);
      if(/OPR\/(\S+)/.test(ua)){             //确定是不是引用了Webkit内核的Opera
         browser.ver=RegExp["$1"];
         browser.opera=parseFloat(browser.ver);
      }else if(/Chrome\/(\S+)/.test(ua)){    //确定是不是Chrome
         browser.ver=RegExp["$1"];
         browser.chrome=parseFloat(browser.ver);
      }else if(/Version\/(\S+)/.test(ua)){   //确定是不是高版本（3+）的Safari
         browser.ver=RegExp["$1"];
         browser.safari=parseFloat(browser.ver);
      }else{                                 //近似地确定低版本Safafi版本号
         var SafariVersion=1;
         if(engine.webkit<100){
            SafariVersion=1;
         }else if(engine.webkit<312){
            SafariVersion=1.2;
         }else if(engine.webkit<412){
            SafariVersion=1.3;
         }else{
            SafariVersion=2;
         }
            browser.safari=browser.ver=SafariVersion;
      }
   }else if(window.opera){                 //只匹配拥有Presto内核的老版本Opera 5+(12.15-)
      engine.ver=browser.ver=window.opera.version();
      engine.presto=browser.opera=parseFloat(engine.ver);
   }else if(/Opera[\/\s](\S+)/.test(ua)){  //匹配不支持window.opera的Opera 5-或伪装的Opera
      engine.ver=browser.ver=RegExp["$1"];
      engine.presto=browser.opera=parseFloat(engine.ver);
   }else if(/KHTML\/(\S+)/.test(ua)||/Konqueror\/([^;]+)/.test(ua)){
      engine.ver=browser.ver=RegExp["$1"];
      engine.khtml=browser.konq=parseFloat(engine.ver);
   }else if(/rv:([^\)]+)\) Gecko\/\d{8}/.test(ua)){ //判断是不是基于Gecko内核
      engine.ver=RegExp["$1"];
      engine.gecko=parseFloat(engine.ver);
      if(/Firefox\/(\S+)/.test(ua)){                //确定是不是Firefox
         browser.ver=RegExp["$1"];
         browser.firefox=parseFloat(browser.ver);
      }
   }else if(/Trident\/([\d\.]+)/.test(ua)){         //确定是否是Trident内核的浏览器（IE8+）
      engine.ver=RegExp["$1"];
      engine.trident=parseFloat(engine.ver);
      if(/rv\:([\d\.]+)/.test(ua)||/MSIE ([^;]+)/.test(ua)){   //匹配IE8-11+
         browser.ver=RegExp["$1"];
         browser.ie=parseFloat(browser.ver);
      }
   }else if(/MSIE ([^;]+)/.test(ua)){               //匹配IE6、IE7
      browser.ver=RegExp["$1"];
      browser.ie=parseFloat(browser.ver);
      engine.ver=browser.ie-4.0;                    //模拟IE6、IE7中的Trident值
      engine.trident=parseFloat(engine.ver);
   }

   var p=navigator.platform;                        //判断操作系统
   system.win=p.indexOf("Win")==0;
   system.mac=p.indexOf("Mac")==0;
   system.x11=(p.indexOf("X11")==0)||(p.indexOf("Linux")==0);
   if(system.win){
      if(/Win(?:dows )?([^do]{2})\s?(\d+\.\d+)?/.test(ua)){
         if(RegExp["$1"]=="NT"){
            system.win = ({
               "5.0" : "2000",
               "5.1" : "XP",
               "6.0" : "Vista",
               "6.1" : "7",
               "6.2" : "8",
               "6.3" : "8.1",
               "10" : "10"
            })[RegExp["$2"]] || "NT";
         }else if(RegExp["$1"]=="9x"){
            system.win="ME";
         }else{
            system.win=RegExp["$1"];
         }
      }
   }

   return {
      ua:ua,          //用户浏览器Ua原文
      engine:engine,  //包含着用户浏览器引擎（内核）信息
      browser:browser,//包括用户浏览器品牌与版本信息
      system:system   //用户所用操作系统及版本信息
   };

}();


alert(client.ua);

var browserName="";             //保存当前使用的浏览器品牌信息
var browserVer=0;               //保存当前使用的浏览器版本信息
for(var i in client.browser){
   if(client.browser[i]){
      browserName=i;
      browserVer=client.browser[i];
      break;
   }
}

var useEngine="";               //保存当前浏览器引擎（内核）名称
var engineVer=0;                //保存当前使用的浏览器引擎版本
for(var i in client.engine){
   if(client.engine[i]){
      useEngine=i;
      engineVer=client.engine[i];
      break;
   }
}

var useSystem="";               //保存当前操作系统信息
for(var i in client.system){
   if(client.system[i]){
      i== "win"?useSystem = "Windows "+client.system[i]:useSystem=i;
      break;
   }
}

alert( "当前使用的浏览器："+browserName
     + "\n浏览器版本："+browserVer
     + "\n浏览器内核："+useEngine
     + "\n内核版本："+engineVer
     + "\n当前操作系统："+useSystem);

```
