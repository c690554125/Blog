# 数值扩展
扩充了一些API。

## 支持二进制和八进制表示法
二进制以`0b/0B`开头，八进制以`0o/0O`开头
```js
  0b11 === 3 // true 二进制表示3
  0o3 === 3 // true 八进制表示3
```

## Number.isFinite()，Number.isNaN()
`Number.isFinite()`判断是否是有限的数值，只能判断`Number`类型，`不做类型转换`。非数值类型直接返回false
`Number.isNaN()`更安全的判断一个值是否是非数字，ES6前我们使用的是window.isNaN，会将非数字转为Number类型再进行处理，所以类似`isNaN('NaN')`会得到`true`。

## Number.isInteger() 和 Number.isSafeInteger
`Number.isInteger()`判断是否是整数，`不做类型转换`。但由于JS采用的双精度浮点数，不一定判断准确。
`Number.isSafeInteger()`判断是否是安全整数，在-2^53到2^53之间

## Number.EPSILON
JS可接受的最小误差

## Math.trunc()
去除一个小数的小数部分，只返回整数部分。感觉像是Math.floor，但是负数情况会不一样哦！该函数会将`非Number先转换为Number再进行处理`。无法获取整数部分的，则返回NaN。
```js
  console.log(Math.floor(4.9)) // 4
  console.log(Math.floor(-4.9)) // -5
  console.log(Math.trunc(-4.9)) // -4

  Math.trunc(undefined); // NaN
  Math.trunc('foo'); // NaN
  Math.trunc(null); // 0 就你特殊
```

## Math.sign()
这个函数功能很常用，判断一个数值，到底是整数，负数，还是0，还是非数值。
参数为正数，返回+1；
参数为负数，返回-1；
参数为 0，返回0；
参数为-0，返回-0;
其他值，返回NaN。

## 其他
Math还扩充了十几个数学相关的函数。
