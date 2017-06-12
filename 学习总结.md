# 学习总结

### arguments 



```javascript

Javascrip每个函数都会有一个Arguments对象实例arguments，它引用着函数的实参，可以用数组下标的方式"[]"引用arguments的元素。 arguments.length为函数实参个数，arguments.callee引用函数自身。
arguments他的特性和使用方法
特性：
arguments对象和Function是分不开的。因为arguments这个对象不能显式创建，arguments对象只有函数开始时才可用。
使用方法：
虽然arguments对象并不是一个数组，但是访问单个参数的方式与访问数组元素的方式相同
在js中 不需要明确指出参数名，就能访问它们，例如：

function test() {
        var s = "";
        for (var i = 0; i < arguments.length; i++) {
            alert(arguments[i]);
            s += arguments[i] + ",";
        }
        return s;
    }
    test("name", "age")

输出结果：

name,age
```



### callee

```javascript
//callee

        //返回正被执行的 Function 对象，也就是所指定的 Function 对象的正文. 

        //callee是arguments 的一个属性成员，它表示对函数对象本身的引用，这有利于匿名

        //callee还有个非常有用的应用就是用来判断实际参数跟行参是否一致。

        function calleeLengthDemo(arg1, arg2) {

            alert(arguments.callee.toString());//函数自身的引用

            if (arguments.length == arguments.callee.length) {

                window.alert("验证形参和实参长度正确！");

                return;

            } else {

                alert("实参长度：" + arguments.length);

                alert("形参长度： " + arguments.callee.length);

            }

        }

        //calleeLengthDemo(1);

        //应用场景

        //callee的应用场景一般用于匿名函数

        //var fn = function (n) {

        //    if (n > 0)

        //        return n + fn(n - 1);

        //    return 0;

        //}

        //alert(fn(10));

        //函数内部包含了对自身的引用，函数名仅仅是一个变量名，在函数内部调用即相当于调用一个全局变量，不能很好的体现出是调用自身，这时使用callee会是一个比较好的方法.

        var fn = (function (n) {

            if (n > 0)

                return n + arguments.callee(n - 1);

            return 0;

        })(10);

        alert(fn);

```

### caller

```javascript
//caller的应用场景 主要用于察看函数本身被哪个函数调用

 //caller:

        //functionName.caller返回函数的调用者，如果函数直接被调用，则返回null，如果不是在其他函数体内被调用，则返回上层函数体。

        function caller() {

            if (caller.caller) {

                alert(caller.caller.tostring());

            } else {

                alert("函数直接执行");

            }

        }

        function handlecaller() {

            caller();

        }

        //handlecaller();//弹出caller函数的调用者handleCaller

        //caller();//由于没有在其他函数体内调用,所以caller为null,就执行了 alert("函数直接执行")

```

### 跨域的技巧

```javascript
谷歌浏览器 右击在目标后追加 
--disable-web-security
可以实现跨域
```

