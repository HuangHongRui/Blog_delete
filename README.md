# JavaScript代码收录-筆記
## 客户端检测

> 客戶端能力檢測
```
function isHostMethod(object, property) {
var t = typeof object[property];
return t == 'function' ||
  (!!(t == 'object' && object[property])) ||
  t == 'unknown';
}
result = isHostMethod(xhr, "open");
result = isHostMethod(xhr, "foo");
```
