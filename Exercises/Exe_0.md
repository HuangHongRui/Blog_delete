### 基本正则表达式任务。编写一个接受任何长度的数字代码的函数。该函数将检查代码以1,2或3开头，如果是，则返回true。否则返回false。

您可以假设输入将始终为nuber。

>最佳做法
```
  function validataCode (code) {
    return /^[1-3]/.test(code);
//  return /^[123]/.test(cide);
  }
```

>个人所答..
```
  function validateCode (code) {
    return /(^1|^2|^3)/.test(code);
  }
```

