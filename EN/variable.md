### 变量和常量

#### 常量(const): 
* 绑定到常量上的值无法代码层修改，作用域内已定义常量不能重新声明。
* 不可变量有shadow遮蔽机制，常量无此机制。

#### Rust引入不可变变量的主要原因：
* 基于灵活性和安全性的综合考量
* 运行时```runtime```性能上的提升，避免过多的runtime检查 

#### 变量绑定(let)

* Rust使用变量绑定而非一般赋值的关键因素是内存管理上采用所有权ownership机制。变量值有所属权，
* 忽略未使用的变量 **(下划线开头)**：使用下划线开头忽略未使用的变量，例``` let _x = 1;```，编译器会给出警告(```warning: unused variable: ```),
注意此一般用于前期规划设计和DEBUG场景功能调试场景，不建议正式环境使用。

#### 变量解构

* 变量解构：```let (a, mut b): (bool,bool) = (true, false);```

#### 变量遮蔽(shadow)
* Rust 允许声明相同的变量名，在后面声明的变量会遮蔽掉前面声明。
* 变量遮蔽的作用：
在某作用域内无需再使用之前的变量（在被遮蔽后，无法再访问到之前的同名变量），就可以重复的使用变量名字，而不用再重新引入一个新的中间变量。**注意只是变量名字的复用，实际上是创建了新的变量。**

#### （变量、**不可变量**、常量）三者的重要概念和区别

* 变量默认不可变
```
# Compilation fails
let x = 1;
x = 2;
println!("x value: {}", x);
```
* 可变变量：通过mut声明```let mut x = 1;```，不可变变量具有Shadow机制。

* 不可变变量：
    * 不可变变量的Shadow机制
    ```
    let x = 1;
    let x = x + 2; // Note: Variable names are reused, not original variables
    let x = x * 3;
    // x value is 9
    ```
    
    shadow机制注意事项：
    ```shadow```遮蔽机制区别于```mut```：
    * 1.语法层面当尝试修改不可变变量赋值必须使用let关键字重新为变量赋值，则会导致编译错误。
    * 2.shadow遮蔽机制与mut区别：重复使用let关键字会**创建出新的变量**，所以在复用变量名称的同时**可以改变它的类型**。
    * shadow机制特点：**变量类型改变，但变量含义不变**。在连续地对一个值或对象处理过程中避免引入额外中间变量，另外可以便捷达到转换某变量的类型。但考虑代码可读性等多因素最好是谨慎使用，非语义明确的场景下避免过多地引入。

* 常量(const): 
    * 绑定到常量上的值无法代码层修改，作用域内已定义常量不能重新声明。
    * 不可变量有shadow遮蔽机制，常量无此机制。

* 注意事项：由于rust语言本身的特性、编译环境、编译时评估以及运行时评估等等特性相关，可变性是相对的，以上是基于一般安全性的说明。
