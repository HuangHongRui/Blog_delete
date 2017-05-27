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
```
```
