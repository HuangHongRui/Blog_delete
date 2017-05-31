## ATM机允许4或6位数的PIN码，PIN码不能包含任何东西，只有4位数字或正好6位数字。

## 如果函数传递一个有效的PIN字符串，则返回true，否则返回false。

>例如：
```
validatePIN("1234") === true
validatePIN("12345") === false
validatePIN("a234") === false
```

>解法：
```
    function validatePIN(pin) {
      return /^(\d{4}|\d{6})$/.test(pin)
    }
```
