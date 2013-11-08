objective-c-best-practice
=========================

Objective C编程最佳实践 - Giko Luo


本实践用于Objective-C开发人员编程指引。主要涉及

1. [编码规范](#编码规范)
2. [编码实践](#编码实践)

# 编码规范

## 缩进 / 空行 /  空格

1.  程序块使用缩进方式编写， 缩进为四个空格。
2.  相对独立的代码块之间、变量说明之后，必须加空格。
3.  较长的语句分多行书写。长表达式要在低优先级操作符处划分新行, 操作符放在新行之首,划分出的新行要进行适当的缩进,使排版整齐,语句可读。
4.  函数定义、类定义中，左花括号另起一行
5.  if, while, for 等结构语句中，左花括号与结构语句在同一行
6.  每一个if执行语句，无论语句多少都用花括号括起来
7.  空的if等结构体语句，也必须使用花括号，并增加明确注释说明
8.  逗号、分号只在后面加空格
10. 比较操作符, 赋值操作符"="、 "+=",算术操作符"+"、"%",逻辑操作符"&&"、 "&",位域操作符"<<"、"^"等双目操作符的前后加空格。
11. 单元操作符，如"++","--", "!", "~" 等前后不加空格
12. 指针操作符， 如"->", "."前后都不加空格
13. if、for、while、switch 等与后面的括号间应加空格,使 if 等关键字更为突出、 明显。
14. case条件与switch对齐，语句块执行向右缩进四个空格
9.  一行程序以小于80字符为宜


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
        [Object somethingElse];
        
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


## 命名： 变量名、函数名、类名、方法名、协议名、参数名
1. 标识符的命名要清晰、明了,有明确含义,同时使用完整的单词或大家基本可以理解的缩写,避免使人产生误解。
2. 坚持使用一致的命名风格和缩写
2. 变量名以小写字母开头，并使用驼峰风格 (camel-case-first-lower)
2. 变量名的意义，需为名词格式
3. 指针变量申明时，指针紧跟变量名
4. 函数名、方法名使用小写字母开头，并使用骆驼风格
5. 参数名规则与变量名规则相同

        - (void)readFromFilepath:(NSString*)filepath
                           error:(NSError**)errorOrNil;

5. 函数名的意义，需为动词格式
6. 变量名使用英文名词
7. 类名、协议使用英文名词， 已大写开头，使用驼峰风格
8. 子类以其父类作为命名后缀
10. 变量名缩写规则：

        短单词使用去元音字母的方式
        长单词使用前几个字母的方式，保留前两~三个发音音

11. 禁止使用单字母等无意义的变量名，i,j,k等循环体内变量除外。
12. UI控件（IBOutlets）必须以其控件名称为后缀。如
        
        @property (nonatomic, retain) UILabel* titleLabel;   // preferred
        @property (nonatomic, retain) UILabel* title; // misleading

    控件名称使用控件全称，如 Label, Text, Switch, View, ImageView
13. UI方法 （IBActions）使用动词，并能充分说明起含义。 如：

        - (IBAction)showDetailsAction;  // 推荐
        - (IBAction)showDetails;       // 
        - (IBAction)button1Action;    // 不推荐，无意义的名称

14. UI方法（IBActions）也可使用事件的方式命名，命名方式为 控件名称+事件名称， 但必须转交给另一个实际意义的函数处理

        - (void) showDetail {
            ; //do something
        }

        - (IBAction) submitBtnTapped: (id) sender {
            [self showDetail];
        }
        

## 常量
1.  禁止在程序逻辑中使用具体数值，数值必须以常量的方式进行定义
1. 常量以k开头，后跟大写开头的驼峰命名
1.  相同意义的常量，需以 `typedef` 的方式声明
        #define kMagickNumber 3.14

        typedef enum
        {
            ResultAllGood,
            ResultUnexpectedError,
            ResultUnknown
        } Result;

        typedef NS_OPTIONS(NSUInteger, DeviceStatus) {
            DEVICE_STATUS_OFFLINE    = 1,
            DEVICE_STATUS_ONLINE     = 2,
            DEVICE_STATUS_REMOTE     = 4,
            DEVICE_STATUS_LOADING    = 8
        };
        
5.  如果常量的意义，无法由其名称自注释，则需在常量上方，或者右侧增加注释
6. BOOL 常量坚持使用 `YES` , `NO` 。


## 注释
1. 程序尽量可自注释。使用可读的有意义的变量名，函数名，类名等
2. 外部接口，必须提供注释
3. 全局常量，必须提供注释
4. 与业务相关的具体数值, 必须提供注释
5. 源文件头部应进行注释，大致列出文件名、项目名、项目版本、作者、生成日期

        //
        //  GikoAppDelegate.h
        //  jfpal3
        //
        //  Created by Luo Chunhui on 8/8/13.
        //  Copyright (c) 2013 Luo Chunhui. All rights reserved.
        //

 通过在Terminal中执行以下语句可完成公司名称的自动填充：

        defaults write com.apple.Xcode PBXCustomTemplateMacroDefinitions '{"ORGANIZATIONNAME" = "your CompanyName";}' 

6. 类中的方法，需按照功能、protocol进行分组，并提供`#pragma mark - UITableViewDataSource`标示
7. 重要业务方法或算法函数头部应进行注释
8. 函数注释应列出:函数的目的/功能、输入参数、输出参数、返回值、调用资源(函数、表、远程资源)等。
9. 注释应放在被注释内容的上方或右侧。
10. case条件中，如需跳跃式条件，或case语句块中无Break，需明确注释说明

        switch (x) {
        case 1:
            [Object doFirstThing];
            break;
        // 2 is default
        case 3:
            ;                        //do nothing
            break;
        case 4:
            [Object do4ThenGo5];
            //YES, no break and goto 5
        case 5:
            [Object doForthThing];
        default:               
            [Object soSomethingElse];
            break;
        }

###注释最佳实践
1. 写代码之前编写注释。 写代码之前，就可以先将自己的思路、业务文档、算法思路、参考代码作为注释的方式放在源码中。
2. 边写代码边写注释。 在写代码过程中，将遇到的疑问，可能的bug，可能的异常，或者TODO事项，已注释方式卸载代码的相应位置。
3. 写代码之后完善注释。 代码写完之后，将无用的注释、过期的注释进行清理，并记入版本管理。如果代码中有很独特的业务模式或算法，需补充完整的注释。
4. 严防注释的二义性，注释必须清晰明了，含义准确，切忌留下过期的与实际代码不符的注释
5. 避免在注释中使用缩写。
6. 勇敢的用短英文单句写注释
7. 终极建议：优秀的代码，是自注释的。 通过重构，调整类、函数、过程、变量、结构以及使用正确的命名、合理地组织代码的结构, 使代码成为自注释的。这是关于注释的最佳实践。



#编码实践

##结构
1. 除非万不得已，不使用全局变量


### Categories
Categories可非常方便的增加类的方法，特别是你可以为那些你无法完全控制的外部资源增加方法，如内置的类或第三方的类。
TODO

### 使用对象， 而非字典

在项目中，经常需要传递或持久化一个结构化数据。最笨的方式是构造一个字典（Dictionary），然后将结构化数据作为该字典的key & value。如：

```
{"name": "Giko", "email": "spam@gmail.com”}
```

此方式易于保存，读取，但不具备可读性，也不利于编译检查。
建议讲起重构为User对象：

```
@interface User : NSObject
@property (nonatomic, retain) NSString* name;
@property (nonatomic, retain) NSString* phone;
@end
```

如果需要持久化，则增加Coding protol， 完整代码：
```
@interface User : NSObject <NSCoding>

@property (strong, nonatomic) NSString *pk;
@property (strong, nonatomic) NSString *name;
@property (strong, nonatomic) NSString *phone;
- (void) setFromDictionary: (NSDictionary *) dict;
+ (instancetype) userWithDictionary:(NSDictionary *)dict;

@end



@implementation User

- (void)encodeWithCoder:(NSCoder *)coder
{
    [coder encodeObject:[self pk] forKey:@"pk"];
    [coder encodeObject:[self name] forKey:@"name"];
    [coder encodeObject:[self password] forKey:@"phone"];
}

- (id)initWithCoder:(NSCoder *)coder
{
    self = [[User alloc] init];
    if(self) {
        self.pk = [coder decodeObjectForKey:@"pk"];
        self.name = [coder decodeObjectForKey:@"name"];
        self.phone = [coder decodeObjectForKey:@"phone"];
    }
    return self;
}

+ (instancetype) userWithDictionary:(NSDictionary *)dict {
    return [[User alloc] initWithDictionary:dict];
}

- (instancetype) initWithDictionary:(NSDictionary *)dict {
    self = [self init];
    if(self != nil) {
        [self setFromDictionary:dict];
    }
    return self;
}

- (void) setFromDictionary: (NSDictionary *) dict
{
	//这里，用来映射服务器等数据源返回的字典数据
    self.pk = dict[@"pk"];
    self.name = dict[@"name"];
    self.phone = dict[@"phone"];
}

@end


//数据持久化调用
//保存
User *u = [User userWithDictionary: dict];
NSData *userData = [NSKeyedArchiver archivedDataWithRootObject:u];
[USER_DEFAULT setObject:userData forKey:kUserInfo];
[USER_DEFAULT synchronize];

//获取
User *u = [NSKeyedUnarchiver unarchiveObjectWithData:[USER_DEFAULT dataForKey:kUserInfo]];


```











