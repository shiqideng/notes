# FA自动化报告流程

## 一、目的

实现自动化出具FA报告，降低人力资源

## 二、实现步骤：

1. 检测下机数据、自动导出胶图插入报告模版中
2. 在第一步的基础上自动化出具模版
3. 根据提供的文库类型，操作软件实现片段大小的填入

## 三、配置

语言：Python

环境及软件：Windows 10，Python 3.9，PROsize 3.0，Chrome，chromedrive

编译器：Pycharm、VScode、sublime

## 四、文件列表

```shell
./AutoFregmentAnalyzeSystem 	# 主文件夹
  |-configer.py					# 运行文件（调用所有包）
  |-Path.py							# 所有路径拼接
  |-copy.py							# 复制所有文件到特定文件夹中
  |-sample.py						# 读取点样表，获取点样位置
  |-FileCheck.py				# 所有文件检查
  |-FAsoftcontrol				# FA分析软件操作（曝光调整，调整积峰,导出PDF胶图）
  |-GelImage.py					# 截取PDF中的胶图，插入word中
  |_Report.py				    # 报告模板制作
```



## 五、变量名

当前日期：date_tady

远程FA下机数据文件夹：file_fa

FA下机数据文件夹：file_fa_locat

远程FA上样顺序表：csv_sample

FA上样顺序表：csv_sample_locat



