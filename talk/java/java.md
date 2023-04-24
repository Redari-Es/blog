## java

### 编译

带jar包编译
例如我需要使用jdbc中的mysql
- javac 编译成class文件
- java 运行

在两者中都需要指定jar包

> java -cp ~/java/lib/mysql-connector-j-8.0.31.jar: 需要编译的文件

> -d指编译后的路径 当前或者指定一个新的

#### 命令替换

alias jar="java -cp ~/java/lib/mysql-connector-j-8.0.31.jar:"
