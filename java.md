# 安装环境
## 安装OpenJDK
安装 openjdk 11 JDK
```
sudo apt-get install openjdk-11-jdk
```
选择版本
```
sudo update-alternatives --config java
sudo update-alternatives --config javac
```
## 编译运行
```
javac Test.java
java Test
```

# Java的基本程序设计结构
## 源文件基本结构
```java
// java应用程序的所有内容都必须放置在类中
// 源代码的文件名必须与公共类名字相同
// 一个源文件内仅能有唯一公共类
public class HelloWorld { //类名大写开头，驼峰命名
    public static void main(String[] args){ //程序入口
        System.out.println("Hello World"); //对于一个方法，即使没有参数也要使用空括号
    }
}
// 一个源文件内可以有任意数目的非公有类
class OtherClass {}
```
## 基本数据类型
### 整型
byte (1 byte) <br/>
short (2 bytes) <br/>
int (4 bytes)  <- 主要使用 <br/>
long (8 bytes) <br/>