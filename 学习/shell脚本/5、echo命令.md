# echo命令

shell的`echo`命令用于字符串的直接输出。命令格式：

```shell
echo string
```

echo命令还可以实现更复杂的输出格式控制。

### 1、显示普通字符串

```shell
echo "It is a test"
```

这里的双引号完全可以省略，下面命令和上面的实例输出结果一致：

```shell
echo It is a test
```

### 2、显示转义字符

```shell
echo "\"It is a test\""
```

结果将是：

```shell
"It is a test"
```

同样，双引号也可以省略。

### 3、显示变量

read 命令从标准输入中读取一行，并把输入行的每个字符的至指定给shell变量

```shell
#!/bin/sh
read name
echo "$name It is a test"
```

输出结果为：

```shell
[root@*** ~]# sh test.sh
OK				# 标准输入
OK It is a test # 输出
```

### 4、显示换行

```shell
echo -e "OK! \n" # -e 开启转义
echo "It is a test"
```

输出结果为：

```shell
OK!
It is a test
```

### 5、显示不换行

```shell
#!/bin/sh
echo -e "OK! \c" # -e 开启转义 \c 不换行
echo "It is a test"
```

输出结果为：

```shell
OK! It is a test
```

### 6、显示结果定向到文件

```shell
echo "It is a test" > file_name
```

### 7、原样输出字符串，不进行专业或取变量（用单引号）

```shell
echo '$name\"'
```

输出结果为：

```shell
$name\"
```

### 8、显示命令执行结果

```shell
echo `date`
```

**注意：**这里使用的反引号，而不是使用单引号。

结果将显示当前日期

```shell
Fri Jan 22 17:08:57 CST 2021
```

