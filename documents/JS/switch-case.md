# switch 中的 case 语句

> If there is no break then the execution continues with the next case without any checks.
> 
> 如果被命中的 `case` 语句中没有 **`break`** 关键字，则后面所有的 `case` 语句中内容都会被顺序执行(不做条件匹配检查)，直到遇到 **`break`** 关键字。

例：

```javascript
let a = 2 + 2;

switch (a) {
  case 3:
    console.log( 'Too small' );
  case 4:
    console.log( 'Exactly!' );
  case 5:
    console.log( 'Too big!' );
  case 6:
    console.log( 'Too big second!');
    break; // (*)
  case 7:
  	 console.log( 'Too big third!');
  default:
    console.log( "I don't know such values!" );
}
```

输出结果：

```javascript
> Exactly!
> Too big!
> Too big second!
```

`switch(a)` 语句在运行时，遇到 `case 4` 时匹配成功；由于该 case 语句没有 `break` 关键字，所以会一直向后运行，直到 **`(*)`** 所在行时遇到 `break` 关键字，switch 语句结束。

**注：Get it from [The "switch" statement](https://javascript.info/switch#an-example).**


## <span id="links">参考</span>

* [The "switch" statement](https://javascript.info/switch#an-example)

## <span id="author">作者 🙉</span>

* [GitHub](https://github.com/Tao-Quixote)
* e-mail: <web.taox@gmail.com>