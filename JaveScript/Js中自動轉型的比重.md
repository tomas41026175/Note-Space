1. 字符串和数字的运算：如果一个操作数是字符串类型，另一个操作数是数字类型，则 JavaScript 会将字符串类型的操作数转换为数字类型。
```
console.log("10" + 5); // 输出 "105"
console.log("10" - 5); // 输出 5
```
2. 字符串和布尔值的运算：如果一个操作数是字符串类型，另一个操作数是布尔值类型，则 JavaScript 会将布尔值类型的操作数转换为数字类型（0 或 1），然后将其转换为字符串类型。
```
console.log("hello" + true); // 输出 "hellotrue"
console.log("world" + false); // 输出 "worldfalse"
```
3. 数字和布尔值的运算：如果一个操作数是数字类型，另一个操作数是布尔值类型，则 JavaScript 会将布尔值类型的操作数转换为数字类型（0 或 1），然后进行数字运算。例如：
```
console.log(10 + true); // 输出 11
console.log(5 - false); // 输出 5
```
4. 对象和原始值的运算：如果一个操作数是对象类型，另一个操作数是原始值类型，则 JavaScript 会尝试将原始值类型的操作数转换为对象类型。例如：
```
console.log({} + 5); // 输出 "NaN"
console.log(true + {}); // 输出 "true[object Object]"
```