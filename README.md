objective-c-best-practice
=========================

Objective C编程最佳实践 - Giko Luo


本实践用于Objective-C开发人员编程指引。主要涉及

1. 编码规范
2. 编码实践


# 编码规范

## 缩进 / 空行 /  空格

1.	程序块使用缩进方式编写， 缩进为四个空格。
2.	相对独立的代码块之间、变量说明之后，必须加空格。
3.	较长的语句分多行书写。长表达式要在低优先级操作符处划分新行, 操作符放在新行之首,划分出的新行要进行适当的缩进,使排版整齐,语句可读。
4.	函数定义、类定义中，左花括号另起一行
5.	if, while, for 等结构语句中，左花括号与结构语句在同一行
6.	每一个if执行语句，无论语句多少都用花括号括起来
7.	空的if等结构体语句，也必须使用花括号，并增加明确注释说明
8.	逗号、分号只在后面加空格
9.	一行程序以小于80字符为宜

```objective-c
//缩进范例
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
    
    NSInteger x, y;
    NSInteger z = 4,
              sum = 0;
    
    while (x == y) {
        [Object something];
        [Object somethingelse];
        
        if (someError) {
            /* the curly braces around this code block could be omitted */
            [Object doCorrectSomething];
        }
        else if(otherError) {
            ; //nothing need to do when this error.
        }
        else {
            [Object continueAsUsual];
        }
        
        for (NSInteger i; i < 10; ++i) {
            sum += i;
        }
    }
    
    [Object finalthing];

    // Override point for customization after application launch.
    self.window.backgroundColor = [UIColor whiteColor];
    [self.window makeKeyAndVisible];
    return YES;
}
```


## 变量名、函数名、类名、协议名
1. 变量名以小写字母开头，并使用驼峰风格
2. 变量名的意义，需为名词格式
3. 指针变量申明时，指针紧跟变量名
4. 函数名称使用小写字母开头，并使用骆驼风格
5. 函数名的意义，需为动词格式
6. 变量名使用英文名词
7. 类名、协议使用英文名词， 已大写开头，使用驼峰风格
8. 子类以其父类作为命名后缀
9. 常量使用全大写，单词之间使用下划线分割
10. 变量名缩写规则：
    >	短单词使用去元音字母的方式
    >	长单词使用前几个字母的方式，保留前两~三个发音音
11. 禁止使用单字母等无意义的变量名，i,j,k等循环体内变量除外。


## 常量
1.	禁止在程序逻辑中使用具体数值，数值必须以常量的方式进行定义
1.	局部常量需在.m文件的头部声明
1.	全局常量需在.h文件中声明。
1.	相同意义的常量，需以 typedef NS_OPTIONS 的方式声明
1.	如果常量的意义，无法由其名称自注释，则需在常量上方，或者右侧增加注释




