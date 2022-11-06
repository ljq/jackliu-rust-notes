### 流程控制（Flow Control）


#### 循环（for、while 和 loop）

###### for
语法总结：
| 使用方法                    | 等价使用方式                                    | 所有权     |
| :-------------------------- | :---------------------------------------------- | :--------- |
| for item in collection      | for item in IntoIterator::into_iter(collection) | 转移所有权 |
| for item in &collection     | for item in collection.iter()                   | 不可变借用 |
| for item in &mut collection | for item in collection.iter_mut()               | 可变借用   |


* 迭代循环索引操作：
```
let a = [2, 1];
// `.iter()` 方法把 `a` 数组变成一个迭代器
for (i, v) in a.iter().enumerate() {
    println!("第{}个元素是{}", i + 1, v);
}
```

* 下标循环索引操作

###### 次数简化方式:
```
for _ in 0..10 {
  // ...
}
// _ 的含义是忽略该值或者类型，否则编译器会给你一个变量未使用的的警告
```

循环方式优劣对比:
* 性能：
    第一种 collection[index] 的索引访问会因为边界检查(Bounds Checking)导致运行时的性能损耗 —— Rust 会检查并确认 index 是否落在集合内。    
    第二种直接迭代的方式就不会触发这种检查，因为编译器会在编译时就完成分析并证明这种访问是合法的
* 安全：
    第一种方式里对 collection 的索引访问是非连续的，存在一定可能性在两次访问之间，collection 发生了变化，导致脏数据产生。  
    第二种直接迭代的方式是连续访问，因此不存在这种风险（这里是因为所有权吗？是的话可能要强调一下）

###### while

* for安全性优于while

###### loop

* loop本身是表达式，支持返回值（类似 return）
* loop内break可单独使用, 支持带一个返回值
* loop适用于大部分循环场景，慎用无限循环
```
loop { 
    // break 支持返回值
}
```
* 


注意事项：
* **复杂集合循环时使用引用，否则引用所有权会被转移（move）到 for 语句块中。**
* ```copy```特征的简单数组类型(例如 [i32; 10] ):  
for item in array 并不会把 arr 的所有权转移，而是直接对其进行了拷贝，因此循环之后仍然可以使用 arr




