### Basic Features

#### （变量、**不可变量**、常量）三者的重要概念和区别

* 变量认不可变
```
# Compilation fails
let x = 1;
x = 2;
println!("x value: {}", x);
```
* 可变变量：通过mut声明```let mut x = 1;```，不可变变量具有Shadow机制。

    * 不可变变量的Shadow机制
    ```
    let x = 1;
    let x = x + 2; // Note: Variable names are reused, not original variables
    let x = x * 3;
    // x value is 9
    ```
    
    Shadow机制注意事项：
    ```Shadow```隐藏机制区别于```mut```：
    * 1.语法层面当尝试修改不可变变量赋值必须使用let关键字重新为变量赋值，则会导致编译错误。
    * 2.隐藏机制与mut区别：重复使用let关键字会**创建出新的变量**，所以在复用变量名称的同时**可以改变它的类型**。

* 常量(const): 
    * 绑定到常量上的值无法代码层修改，作用域内已定义常量不能重新声明。
    * 不可变量有Shadow隐藏机制，常量无此机制。

* 注意事项：由于rust语言本身的特性、编译环境、编译时评估以及运行时评估等等特性相关，可变性是相对的，以上是基于一般安全性的说明。

