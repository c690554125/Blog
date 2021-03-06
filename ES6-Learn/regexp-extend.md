# 正则扩展
ES6针对正则做了一些新的扩展，如新的修饰符，构造函数传参改变。本文只记录可能会常用的。

## 构造函数传参
ES6之前，`new RegExp(reg)`，如果你传参传的是一个正则表达式，那只允许传这么一个参数。传第二个参数会报错。
```js
  var regex = new RegExp(/xyz/, 'i');
  // Uncaught TypeError: Cannot supply flags when constructing one RegExp from another
```
ES6中支持传入第二个参数，也就是修饰符，会替换掉第一个参数中的修饰符
```js
  let reg = new RegExp(/\d/ig, 'g')
```

## y修饰符
类似`g修饰符`，也是全局匹配，不同于`g修饰符`的地方，在于`y修饰符`的匹配，严格从上一次匹配位置的下一个字符开始，而`g修饰符`不在乎上一次和下一次的匹配之间到底隔了多少。
```js
  let a = 'aaa_aa_a'
  let r1 = /a+/g
  let r2 = /a+/y
  console.log(r1.exec(a)) // aaa
  console.log(r1.exec(a)) // aa 直接跳到aa_a开始匹配
  console.log(r1.exec(a)) // a

  console.log(r2.exec(a)) // aaa
  console.log(r2.exec(a)) // null 这是从_aa_a开始匹配的
```

## u修饰符
用来匹配Unicode，可以正确处理大于`\uFFFF`的Unicode字符。
```js
  let s = '\uD83D\uDC2A' // 这是一个由2个双字节组成的Unicode字符，是一个整体
  /^\uD83D/.test('\uD83D\uDC2A') // true 这里返回true，说明并没有把超出\uFFFF的Unicdoe字符正常匹配。
  /^\uD83D/u.test('\uD83D\uDC2A') // false 使用u修饰符，正则结果正常。
```

## flags属性
获取正则表达式的标志字符串如`/abs/g`的`g`，`reg.flags`就可以获取到`g`了，`reg.source`获取到`abs`
