# Swift(未完待续。。。)


## 可选型

可选型是swift语言的特色之一，用于表达一个变量/常量可以为nil或者非nil两种状态。可选类型其本质是一个枚举型，包含none和some两种类型。Optional.none就是nil, 非nil的原始值会通过some(T)包装，这也是为什么在使用Optional的时候要拆包的原因, 就是为了从enum里取出来原始值。可选型表示方法如下：
```
var num: Int? = 1
```
nil在Objective-C中表示一个空指针；nil在swift中不是空指针，nil是个确定的值，用来表示值缺失
```
var view: UIView = nil //报错：Nil cannot initialize specified type 'UIView'
var view: UIView? = nil //正确
```
可选型解包
```
// 解包方式1
var name: String? = "令狐冲"
if name != nil {
    print("姓名\(name!)") // 使用!强制解包
} else {
    print("name 为 nil")
}

```

```
// 使用可选绑定获取可选类型的值（官方推荐）
var name: String? = "令狐冲"
if let name = name {
    print("姓名\(name)") // 使用!强制解包
} else {
    print("name 为 nil")
}
```
空合运算符（nil coalecse）“a ?? b” 将对可选类型a进行空判断，如果a非nild就对其进行解包，否则就返回一个默认值b
```
var name: String? = "鹿晗"
var address: String? = nil
print((name ?? "XXX"),"来自", (address ?? "未知地区"))
// print结果为：鹿晗 来自 未知地区
```
可选链(optional chaining)为一种可以在当前值可能为nil的可选值上请求和调用属性、方法及下标的方法。如果可选值有值，那么调用就会成功；如果可选值是nil，那么调用将返回nil。多个调用可以连接在一起形成一个调用链，如果其中任何一个节点为nil，整个调用链都会失败，即返回nil。
```
let name = person.dog?.name?.lowercased()
```
变量或常量后加上!的都是隐式可选变量/常量。首先该变量或常量满足可选类型，其可被当成一般的变量/常量来使用，而不需要每次都验证是否有值。
```

class Dog {
    weak var owner: Person?
    init(owner: Person) {
        self.owner = owner
    }
}

class Person {
    var dog: Dog!
    init() {
    
        /**
        * 这里我们希望dog在Person初始化之后即可立即使用所以在这里dog不应该设置为可选型。
        * 如果dog不是可选型 self.dog = Dog(owner: self)这行代码就会报错如下：
        * 'self' used before all stored properties are initialized
        * 原因是我们必须在Person所有的非可选型存储变量初始化之后才可以使用self变量，而这里
        * 我们的Dog初始化又需要一个Person类型参数，在这种情况下就可以将dog设置为隐式可选型
        */
        self.dog = Dog(owner: self) 
    }
}

```

## 枚举
raw value
raw value 与 associate value互斥
可选型实质上是枚举类型
枚举也可以定义方法

## 结构体
自定义构造函数之后，默认构造函数失效
可失败构造函数
结构体和枚举都是值类型，赋值即拷贝
结构体（和枚举）函数内部修改自身属性值需要在函数前加mutating

## 面向对象
判断类对象是否相等 ===（也可以重载==运算符） （值语义对象是否相等用 ==）

属性和方法
计算型属性（例：center） 必须声明为var
类型属性（type property）static var 。。。
类型方法 （）
属性观察器（property observer）注意：didset和willset在初始化阶段不会调用

懒加载属性

访问控制

单例模式 private init

两段式构造 先初始化，再做其他具体设置

构造函数继承原则：
1.如果子类没有实现父类的任何制定构造函数，则自动继承父类的所有制定构造函数
修正版：1.如果子类没有实现任何指定构造函数，则自动继承父类的构造函数（包括指定和便利）
2.如果子类实现了父类所有的构造函数，则自动继承父类所有便利函数
修正：

下标

运算符重载

嵌套类型


## 泛型

swift协议
1.struct和类都可以遵守协议，也可以限制协议只给类遵守，用 : class 标识
2.协议可以制定构造函数
3.类型别名和关联类型
4.可以在协议扩展中实现协议中的某些方法（默认实现）
5.协议聚合 protocol<p1, p2>
6.泛型约束
7.协议：可选协议方法
8.异常处理
9.控制转移：defer

## 类型检查和转换
1.检查 is
2.转换 as
3.nsobject anyobject any








You can use the [editor on GitHub](https://github.com/gsdios/Notebook/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/gsdios/Notebook/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
