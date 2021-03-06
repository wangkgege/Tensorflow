# 快速入门
[源码-start.py](./start.py)
```
#首先引入tensorflow 代码块是同一.py中
import tensorflow as tf
```
 ## 张量tensor
	> 什么是张量？张量相当于表,又有点类似于树    
	> 0 维张量=标量 如12  shape[]  
	> 1 维张量=向量:0维张量的向量 如[1,2,45,5] 类似python中的list,shape[4]  
	> 2 维张量=1维张量的向量 如[[12,333,],[312323,23]] ,shape[2,2]   
	> 3 维张量=2维张量的向量 ~~~   
	> n维向量=n-1维张量的向量~~~
- 流图Graph 
> 由一系列节点(node)汇聚而成的tf操作(option)

##  常量constant  
方法[tf.constant](https://www.tensorflow.org/api_docs/python/tf/constant)

- 构造函数
```
constant(
    value,
    dtype=None,
    shape=None,
    name='Const',
    verify_shape=False
)
```

- 举例
```
node1= tf.constant([True,True])
node2= tf.constant(12)
node3=tf.constant("hello")
node4=tf.constant("world")
print(node1)#打印Tensor("Const:0", shape=(2,), dtype=bool)
print(node2)#打印Tensor("Const_1:0", shape=(), dtype=int32)
print(node3)#打印Tensor("Const_2:0", shape=(), dtype=string)
sess=tf.Session()#获取会话
print(sess.run(node1))#打印[True,True]
print(sess.run(node2))#打印12  
print(sess.run(node3))#打印b'hello'
print(sess.run(node4))#打印b'world'
#要想获取平常的值如12 必须通过sess.run()进行，不然输入还是tensor格式
```

## 加法  
方法[tf.add](https://www.tensorflow.org/api_docs/python/tf/add)  
[更多数学运算](https://www.tensorflow.org/api_guides/python/math_ops#Arithmetic_Operators)

- 构造函数
```
add(
    x,
    y,
    name=None
)
```

- 举例
```
node5=tf.constant(-1)
n_add=tf.add(node2,node5)
print(sess.run(n_add))#打印11
node6=tf.constant(-2)
n_add2=node5+node6
print(sess.run(n_add2))#打印-3 说明两种形式的加法也可以的 
```

## 占位符
方法[tf.placeholder](https://www.tensorflow.org/api_docs/python/tf/placeholder)  
相当于数学函数的右侧的变量
构造函数
```
placeholder(
    dtype,
    shape=None,
    name=None
)
```	
例子
```
p1=tf.placeholder(tf.float32)
p2=tf.placeholder(tf.float32)
n_add3=p1+p2
a=sess.run(n_add3,{p1:23,p2:32})#用法正确
#a=(n_add3,{p1:23,p2:32})错误 只能和sess一起使用
print(a)#55.0
print(sess.run(n_add3,{p1:23,p2:32}))#用法正确 打印55.0
```

## 变量
[tf.Variable](https://www.tensorflow.org/api_docs/python/tf/Variable)

- 构造函数
```
__init__(
    initial_value=None,
    trainable=True,
    collections=None,
    validate_shape=True,
    caching_device=None,
    name=None,
    variable_def=None,
    dtype=None,
    expected_shape=None,
    import_scope=None
)
```

- 实例
```
v1=tf.Variable(12)
v2=tf.Variable(23)#定义一个变量
init = tf.global_variables_initializer()#进去全部变量的初始化
sess.run(init)
x=tf.placeholder(tf.int32)
a_line=v1*x+v2#使用和常量类似
v3=sess.run(a_line,{x:[1,2]})
print(v3)#[35 47]
#重新赋值
v1=tf.assign(v1,-2)
v2=tf.assign(v2,3)
add4=v1+v2
v4=sess.run(add4)
print(v4)#1

```
## END
