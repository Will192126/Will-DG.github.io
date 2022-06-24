# Kotlin基础语法
## 变量
```
/*
关键字     变量类型
 ↓          ↓           */
var price: Int = 100;   /*
     ↑            ↑
   变量名        变量值   */
```

### 可省略分号
```
var price: Int = 100
```

### 支持类型推到
```
var price = 100 // 默认推导类型为： Int
```

### val和var关键字
- **val**声明的变量，叫**不可变变量**，它的值在初始化后无法再次被修改，相当于Java里面的final变量
- **var**声明的变量，叫**可变变量**，相当于Java里的普通变量
- 在Kotlin中尽可能多地使用val

## 基础类型
包括常见的数字类型、布尔类型、字符类型，以及前面这些类型组成的数组

### 一切都是对象
| Type   | Bit width |     备注 |
| :----- | :--: | :-: |
| Double |  64  | Kotlin没有double |
| Float |  32  | Kotlin没有float |
| Long |  64  | Kotlin没有long |
| Int |  32  | Kotlin没有int/Integer |
| Short |  16  | Kotlin没有short |
| Char |  16  | Kotlin没有char |
| Byte |  8  | Kotlin没有byte |
| Boolean |  8  | Kotlin没有boolean |

### 空安全

### 数字类型
- 整形默认会被推导为“Int”类型
- Long类型需要使用“L”后缀
- 小数默认会被推导为“Double”类型
- Float类型需要使用“F”后缀
- 使用“0x”来表示十六进制字面量
- 使用“0b”来表示二进制字面量

#### 类型转换
Java可以饮食转换数字类型，Kotlin更推崇显示转换。  
显示转换可以增强代码的可读性，将来更容易维护。
- Java
  ```
  int i = 100;
  long j = i;
  ```
- Kotlin
  ```
  // 错误做法
  val i = 100
  val j: Long = i // 编译器报错
  
  // 正确做法
  val i = 100
  val j: Long = i.toLong() // 编译通过
  ```

### 布尔类型

### 字符: Char

### 字符串: String
```
val s = "Hello Kotlin!"
```

#### 字符串模板
```
val name = "Kotlin"
print("Hello $name!")
/*            ↑
    直接在字符串中访问变量
*/
// 输出结果：
Hello Kotlin!

val array = arrayOf("Java", "Kotlin")
print("Hello ${array.get(1)}!")
/*            ↑
      复杂的变量，使用${}
*/
// 输出结果：
Hello Kotlin!
```

#### 原始字符串
用于存放复杂的多行文本，并且它定义的时候是什么格式，最终打印也会是对应的格式
```
val s = """
       当我们的字符串有复杂的格式时
       原始字符串非常的方便
       因为它可以做到所见即所得。 """

print(s)
```

### 数组
- 使用arrayOf()创建数组，括号中可以传入数组元素用于初始化
- Kotlin编译器会根据传入的参数进行类型推导
- 虽然Kotlin的数组仍然不属于集合，但它的一些操作是跟集合统一的
  ```
  val arrayInt = arrayOf(1, 2, 3)
  val arrayString = arrayOf("apple", "pear")
  println("Size is ${array.size}")
  println("First element is ${array[0]}")
  
  // 输出结果：
  Size is 2
  First element is apple
  ```

## 函数
### 声明
```
/*
关键字    函数名          参数类型   返回值类型
 ↓        ↓                ↓       ↓      */
fun helloFunction(name: String): String {
    return "Hello $name !"
}/*   ↑
   花括号内为：函数体
*/
```

### 单一表达式函数
函数体只有一行代码，可以直接使用“=”来连接，将其变成一种类似变量赋值的函数形式
```
fun helloFunction(name: String): String = "Hello $name !"
```
因为Kotlin支持类型推导，单一表达式函数的返回值类型可以省略
```
fun helloFunction(name: String) = "Hello $name !"
```

### 调用
- 支持**命名参数**，调用函数的时候传入“形参的名字”
  ```
  // 函数声明
  fun createUser(
      name: String,
      age: Int,
      gender: Int,
      friendCount: Int,
      feedCount: Int,
      likeCount: Long,
      commentCount: Int
  ) {
      //..
  }
  
  // 函数调用
  createUser(
      name = "Tom",
      age = 30,
      gender = 1,
      friendCount = 78,
      feedCount = 2093,
      likeCount = 10937,
      commentCount = 3285
  )
  ```
- 支持**参数默认值**
  ```
  // 函数声明
  fun createUser(
      name: String,
      age: Int,
      gender: Int = 1,
      friendCount: Int = 0,
      feedCount: Int = 0,
      likeCount: Long = 0L,
      commentCount: Int = 0
  ) {
      //..
  }
  
  // 函数调用
  createUser(
      name = "Tom",
      age = 30,
      commentCount = 3285
  )
  ```

## 流程控制
### if
Kotlin的if，既能作为**程序语句(Statement)**，也可作为**表达式(Expression)**
```
// Statement
val i = 1
if (i > 0) {
    print("Big")
} else {
    print("Small")
}

输出结果：
Big


// Expression
val i = 1
val message = if (i > 0) "Big" else "Small"

print(message)

输出结果：
Big
```

使用**Elvis表达式**简化空判断
```
/* 
如果 text 不为空，我们就算出它的长度；
如果它为空，长度就取 0 
*/
fun getLength(text: String?): Int {
  return text?.length ?: 0
}
```

### when
- 当代码逻辑只有两个分支时，一般会使用if/else，而大于两个逻辑分支的情况，会使用when
- when可以作为程序语句，也可作为表达式，为变量赋值
- when要求它里面的逻辑分支必须是完整的

```
val i: Int = 1

val message = when(i) {
    1 -> "一"
    2 -> "二"
    else -> "i 不是一也不是二" // 如果去掉这行，会报错
}

print(message)
```

### 循环迭代while和for
#### while
Kotlin while的使用与Java无异

#### for
- 迭代数组和集合
  ```
  val array = arrayOf(1, 2, 3)
  for (i in array) {
      println(i)
  }
  ```
- 迭代区间
  ```
  val oneToThree = 1..3 // 代表 [1, 3]
  
  for (i in oneToThree) {
      println(i)
  }
  
  输出结果：
  1
  2
  3
  
  
  // 逆序区间迭代
  /*
     逆序区间[6,0]     指定步长为2
            ↓           ↓           */
  for (i in 6 downTo 0 step 2) {
      println(i)
  }
  
  输出结果：
  6
  4
  2
  0
  ```
