title: Android Studio 使用技巧
categories: android
tags:
  - android
  - Android Studio
---

### 全文搜索 ###

*	`Text to find` ：要查找的字符  
*	`Replace with` ：替换为  
*	`Options` ：
	*	`General` ：  
		*	`Case sensitive` ：区分大小写
		*	`Preserve case` ：不区分大小写
		*	`Whole words only(may be faster)` ：匹配整个单词
		*	`Reqular Expression[Help]` ：使用正则表达式
		*	`Context`：
			*	`anywhere` ：任何地方查找
			*	`in comments` ：在注释中查找
			*	`in string literals` ：在字符串中查找
			*	`except comments` ：除了注释（注释之外查找）
			*	`except string literals` ：除了字符串 (在字符串之外查找)
			*	`except comments and string literals` ：除了注释和字符串(在注释和字符串之外查找)
	*	`Scope`：查找范围
		*	`Whole project` ：整个项目
		*	`Module` ：对应的模块
		*	`Directory` ：对应的目录
		*	`Recursively` ：递归进入子目录查找
		*	`Custom` ：自定义
	*	`File name filter` ：根据文件名称过滤
		*	`File mask(s)`
	*	`Result options`
		*	`Open in new tab`

### 自定义 Live Template ###

创建Toast方法（自带的）

*	进入活动模板界面：File -> Settings -> Editor -> Live Templates
*	点击加号选择 `Template Group` ，输入活动模块的分组的名称 `Wii`，选中 `Wii` 再点击加号选择 `Live Template` ，输入要创建的活动模块名 `Toast` 。

		Toast.makeText($className$.this, "$text$", Toast.LENGTH_SHORT).show();

### 自定义 File Template ###

创建单例class（自带饿汉）

*	进入活动模板界面：File -> Settings -> Editor -> File and Code Templates
*	点击加号 ，输入模板名称 `WiiSingleton` 。

		#if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME};#end
		#parse("File Header.java")
		public class ${NAME}{

		    private static ${NAME} instance;

		    private ${NAME}() {}

		    public static ${NAME} getInstance() {
		        if(instance == null){
		            synchronized (${NAME}.class) {
		                if (instance == null) {
		                    instance = new ${NAME}();
		                }
		            }
		        }
		        return instance;
		    }
		}

> PS：可以创建一些 `activity` 的模板