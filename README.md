# offer-topic
一些前端常见面试题和一些js奇巧淫技

##面试题

------

### ['1', '2', '3'].map(parseInt) what & why

map函数入参(item,index,arr)。然后parseInt函数说明：

| 参数   | 描述                                                         |
| :----- | :----------------------------------------------------------- |
| string | 必需。要被解析的字符串。                                     |
| radix  | 可选。表示要解析的数字的基数。该值介于 2 ~ 36 之间。如果省略该参数或其值为 0，则数字将以 10 为基础来解析。如果它以 “0x” 或 “0X” 开头，将以 16 为基数。如果该参数小于 2 或者大于 36，则 parseInt() 将返回 NaN。 |

解析：

```
第一次运行传入 parseInt(1,0),返回1
第二次parseInt(2,1),返回NaN。
第三次parseInt(3,2)，基数为2的2进制数最大值小雨3，因而返回NaN
```

变形

```javascript
let unary = fn => val => fn(val)
let parse = unary(parseInt)
console.log(['1.1', '2', '0.3'].map(parse))
```

解析：

​		拆解箭头函数等效于

```javascript
let unnarCopy = function (fn) {
    return function (val) {
    return parseInt(val);
    };
};
```

这样看起来就比较明朗了，每次只传入一个值，重复上面的解析步骤[1，2，0]