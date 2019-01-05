# Swift(未完待续。。。)


## 可选型

可选型是Swift语言的特色之一，用于表达一个变量/常量可以为nil或者非nil值。可选类型其本质是一个枚举型，包含none和some两种类型。Optional.none就是nil, 非nil的原始值会通过some(T)包装，这也是为什么在使用Optional的时候要拆包的原因, 就是为了从enum里取出来原始值。可选型表示方法如下：
```
var num: Int? = 1
```
nil在Objective-C中表示一个空指针；nil在Swift中不是空指针，nil是个确定的值，用来表示值缺失
```
var view: UIView = nil //报错：Nil cannot initialize specified type 'UIView'
var view: UIView? = nil //正确
```
### 可选型解包
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
### 空合运算符
空合运算符（nil coalecse）“a ?? b” 将对可选类型a进行空判断，如果a非nild就对其进行解包，否则就返回一个默认值b
```
var name: String? = "鹿晗"
var address: String? = nil
print((name ?? "XXX"),"来自", (address ?? "未知地区"))
// print结果为：鹿晗 来自 未知地区
```
### 可选链
可选链(optional chaining)为一种可以在当前值可能为nil的可选值上请求和调用属性、方法及下标的方法。如果可选值有值，那么调用就会成功；如果可选值是nil，那么调用将返回nil。多个调用可以连接在一起形成一个调用链，如果其中任何一个节点为nil，整个调用链都会失败，即返回nil。
```
let name = person.dog?.name?.lowercased()
```
### 隐式可选型
变量或常量后加上!的都是隐式可选变量/常量。首先该变量或常量满足可选类型，其可被当成一般的变量/常量来使用，而不需要每次都验证是否有值。隐式可选型主要用在一个变量/常量在定义瞬间完成之后值一定会存在的情况，例如在类的初始化过程中等。
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
与OC中枚举只能是int类型不同，Swift的枚举支持的数据类型有很多，例如整型(Integer)、浮点数(Float Point)、符串(String)等
```
enum Movement:Int {
    case left = 0
    case right = 1
    case top = 2
    case bottom = 3
}

enum Area: String {
    case SH = "shanghai"
    case GZ = "guangzhou"
    case SZ = "shenzhen"
}

enum Animal {
    case cat
    case dog
    case pig
}

```
### 嵌套枚举
```
enum Area {
    enum ShenZhen {
        case NanShan
        case FuTian
    }

    enum GuangZhou {
        case TianHe
        case CheBei
    }
}

```
### 关联值

```
// 声明枚举Trade
enum Trade {
    case buy(stock:String, amount:Int)
    case sell(stock:String, amount:Int)
}

// 使用枚举Tbrade

let trade = Trade.buy(stock: "00700", amount: 100)

switch trade {
    case .buy(let stock,let amount):
        print("\(trade) 股票:\(stock), 数量:\(amount)")
        
    case .sell(let stock,let amount):
        print("\(trade) 股票:\(stock), 数量:\(amount)")
}

// print输出： buy(stock: "00700", amount: 100) 股票:00700, 数量:100

```
### 方法和属性
```
enum Device {
    case iPad, iPhone, AppleTV, AppleWatch
    
    func introduced() -> String {
        switch self {
            case .iPad: return "This is iPad"
            case .iPhone: return "This is iPhone"
            case .AppleWatch: return "This is AppleWatch"
            case .AppleTV: return "This is AppleTV"
        }
    }
}

print(Device.iPhone.introduced())

// print输出：This is iPhone
```

增加一个存储属性到枚举中不被允许，但你依然能够创建计算型属性。

```
enum Device {
    case iPad, iPhone
    var price: Double {
        switch self {
            case .iPhone: return 8000.0
            case .iPad: return 6000.0
        }
    }
}
```

### 枚举&协议
Swift也允许你在枚举中使用协议(Protocols)和协议扩展(Protocol Extension)。

```
例：Swift标准库中有一个CustomStringConvertible是一个定义了格式化输出的Api的协议。

protocol CustomStringConvertible {
    var description: String { get }
}



enum Trade: CustomStringConvertible{
    case buy(stock:String, amount:Int)
    case sell(stock:String, amount:Int)

    var description: String {
        switch self {
            case .buy(let stock,let amount):
                return " 股票:\(stock), 数量:\(amount)"
            case .sell(let stock,let amount):
                return " 股票:\(stock), 数量:\(amount)"
        }
    }
}

print(Trade.buy(stock: "00700", amount: 100).description)

// print输出： 股票:00700, 数量:100

```
### 枚举的扩展
枚举也可以进行扩展，我们可以将枚举的case和method分离使得代码的可读性更强。

```
enum Trade {
    case buy(stock:String, amount:Int)
    case sell(stock:String, amount:Int)
}

extension Trade: CustomStringConvertible {
    var description: String {
        switch self {
            case .buy(let stock,let amount):
                return " 股票:\(stock), 数量:\(amount)"
            case .sell(let stock,let amount):
                return " 股票:\(stock), 数量:\(amount)"
        }
    }
}

print(Trade.buy(stock: "00700", amount: 100).description)

// print输出： 股票:00700, 数量:100
```
### 枚举&泛型
```
enum Theme<T: UIView> {
    case day(T)
    case night(T)

    func apply() {
        switch self {
            case .day(let view):
                view.backgroundColor = UIColor.white
            case .night(let view):
                view.backgroundColor = UIColor.black
        }
    }
}

let v = UIView(frame: CGRect(x: 0, y: 0, width: 100, height: 100))
Theme.night(v).apply()
```

## 结构体

struct是值类型而class是引用类型，值类型的变量直接包含他们的数据，而引用类型的变量存储对他们的数据引用，因此对一个引用类型变量操作可能影响另一个引用类型变量所引用的对象。对于值类型都有他们自己的数据副本，因此对一个值类型变量操作不可能影响另一个值类型变量。相对于OC中的Struct，Swift中的Struct变得更加强大,不仅有成员变量,还多了成员方法,这些特性使它更加接近于一个类.

### Struct的相对于Class的优缺点
优点：

- 安全性
因为struct是用值类型传递的，每个struct变量各自持有一份单独的内存数据，不会出现被其他持有者改变的现象

- 内存
没有引用数，所以不会因为循环引用导致内存泄漏

- 速度
值类型的内存通常来说是以在栈上分配的，而不是用堆，因此他们比在堆上分配内存的引用类型要快

缺点：

- OC和Swift的混合开发
在混合开发中，Swift的struct不能够被OC调用，因为要在OC里调用Swift代码的话，被调用对象需要继承于NSObject

- 继承
作为面向对象的三大特征之一，继承让开发者高效得实现代码重用，但是struct不支持继承，不过好在struct支持协议,这也体现了Swift面向协议的编程思想


### Swift中类和结构体的共同点

- 定义属性用于存储值
- 定义方法用于提供功能
- 定义下标脚本用于访问值
- 定义构造器用于生成初始化值
- 通过扩展以增加默认实现的功能
- 实现协议以提供某种标准功能

### Swift中类和结构体的不同点

- 结构体不具有继承性
- 结构体没有析构器
- 结构体不使用引用计数（值类型）


### mutating关键字

Swift中结构体和枚举可以定义自己的方法，但是默认情况下实例方法中是不可以修改自身属性值，当你需要修改自身属性值需要在函数前加mutating

```
struct Point {
    var x = 0, y = 0

    mutating func move() {
        x += 1
        y += 1
    }
}

```


## 面向对象

### 属性
- 存储型属性
存储型属性就是存储特定类的一个常量或者变量。常量存储的属性使用let关键字定义，变量存储的属性使用var关键字定义

```
class Test {
    var propertyA: Int?
    let propertyB: Int = 10
}
```

- 懒存储属性
懒存储属性是指当被第一次调用的时候才会生成其初始值的属性，一个懒存储属性通过在属性声明的前面加上lazy来标示

```
class Person {
    lazy var propertyLazy: Test = Test()
}
```

- 计算型属性
计算型属性不存储值，它需要提供getter或setter来进行获取值或者赋值（赋值需要另外声明一个变量用于存储值）。getter使用get关键字进行定义，setter使用set关键字进行定义

```
class Person {
    var height: Double {
        get {
            return 180.0
        }
    }
}
```

- 属性观察器
属性观察器包括willSet和didSet，其中属性值改变前会触发willSet，属性改变后会触发didSet
(1)willSet有一个名为newValue的默认参数代表即将设置的新值
(2)didSet有一个名为oldValue的默认参数代表修改之前的旧值
(3)属性初始化时，willSet和didSet不会调用。只有在初始上下文之外，当设置属性值时才会调用。另外，在didSet的实现体内给属性赋值，也不会再次调用属性的属性观察器
(4)即使是设置的值和原来的值相同，willSet和didSet也会被调用

```
class Person {
    var age: Int {
        willSet {
            print("willSet, newValue =", newValue)
        }
        didSet {
            print("didSet, oldValue =", oldValue)
        }
    }

    init() {
        age = 10
    }
}

```
- 类型属性
类型属性与实例对象无关，不需要对类进行实例化就可以使用。
类型属性使用关键字static来定义，结构体、枚举和类都可以定义类型属性。在为类定义类型属性时，可以使用class关键字来代替static关键字。跟实例的存储属性不同，类型的存储属性必须指定默认值，因为类型本身无法在初始化过程中使用构造器给类型属性赋值

```
class Person {
    static var propertyA: Int = 10
    static var propertyB: Int {
        return 20
    }
    class var propertyC: String {
        return "TTTTTTT"
    }
}
```


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






