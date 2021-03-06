# switch

- `else if`可以处理多条分支，但是重复计算多条`if`语句中的条件表达式是非常浪费的做法

- switch 的语法

```markdown
switch(expression){
case value: statement
break;
case value: statement
break;
case value: statement
break;
case value: statement
break;
default: statement
}
```

- 例子

```javascript
switch (n) {
  case 1: // 如果 n === 1，从这里开始执行
    // 执行代码块 1
    break; // 在这里停止执行switch语句
  case 2: // 如果 n === 2，从这里执行
    // 执行代码块 2
    break; // 在这里停止执行switch语句
  case 3: // 如果 n === 3，从这里执行
    // 执行代码块 3
    break; // 在这里停止执行switch语句
  default:
    // 如果所有的条件都不匹配
    // 执行代码块 4
    break; // 在这里停止执行switch语句
}
```

---

```javascript
if (i === 25) {
  console.log("25");
} else if (i === 35) {
  console.log("35");
} else if (i === 45) {
  console.log("45");
} else {
  console.log("Other");
}
```

> 等价于

```javascript
switch (i) {
  case 25:
    console.log("25");
    break;
  case 35:
    console.log("35");
    break;
  case 45:
    console.log("45");
    break;
  default:
    console.log("Other");
}
```

> 避免使用带有副作用的`case`表达式，比如函数调用表达式和赋值表达式。 最安全的做法是在`case`表达式中使用**常量表达式**
