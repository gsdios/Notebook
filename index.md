## Swift(未完待续。。。)


### 可选型

optional chaining
nil coalecse
隐式可选型

### 枚举
raw value
raw value 与 associate value互斥
可选型实质上是枚举类型
枚举也可以定义方法

### 结构体
自定义构造函数之后，默认构造函数失效
可失败构造函数
结构体和枚举都是值类型，赋值即拷贝
结构体（和枚举）函数内部修改自身属性值需要在函数前加mutating

### 面向对象
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


### 泛型

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

### 类型检查和转换
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
