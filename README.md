# JavaScript代码收录-筆記
## 客户端检测

> 客戶端能力檢測
>```//检测浏览器下测试任何对象的某个特性是否存在——不保证永远可靠
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
