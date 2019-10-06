R语言数据分析与挖掘
=========
## 运行环境
     R 3.6.1 ，RStudio
## 目录
* [R语言数据分析与挖掘](#R语言数据分析与挖掘)
	* [一、R的基本数据结构](#一R的基本数据结构)
		* [1、向量](#1向量)
		* [2、列表](#2列表)
		* [3、矩阵](#3矩阵)
		* [4、数组](#4数组)
		* [5、因子](#5因子)
		* [6、数据帧](#6数据帧)
	* [二、获取外部数据](#二获取外部数据)
		* [1、R读写文件](#1R读写文件)
		* [2、R操作数据库](#2R操作数据库)
	* [三、数据可视化](#三数据可视化)
		* [1、条形图](#1条形图)
		* [2、箱形图](#2箱形图)
		* [3、直方图](#3直方图)
		* [4、线形图](#4线形图)
		* [5、散点图](#5散点图)
		* [6、饼状图](#6饼状图)
### 一、R的基本数据结构
### 1、向量
- 向量对象有六种数据类型的原子向量，其他R对象是建立在原子向量之上的。六类向量类型包括逻辑、数字值、整数、复数、字符、原生<br>
当要创建具有多个元素的向量时，应该使用c()函数，表示将元素组合成一个向量<br>
```
> # Create a vector.
> apple <- c('red','green',"yellow");
> apple <- c('red','green',"yellow");
> print(apple);
[1] "red"    "green"  "yellow"
> 
> # Get the class of the vector.
> print(class(apple));
[1] "character"
> 
```
### 2、列表
- 列表是一个R对象，它可以包含许多不同类型的元素，如向量，函数，甚至其中的另一个列表<br>
```
> # Create a list.
> list1 <- list(c(2,5,3),21.3,sin);
> # Print the list.
> print(list1);
[[1]]
[1] 2 5 3

[[2]]
[1] 21.3

[[3]]
function (x)  .Primitive("sin")
> 
```
### 3、矩阵
- 矩阵是二维矩形数据集。 它可以使用向量输入到矩阵函数来创建<br>
```
> # Create a matrix.
> M = matrix( c('a','a','b','c','b','a'), nrow = 2, ncol = 3, byrow = TRUE)
> print(M)
     [,1] [,2] [,3]
[1,] "a"  "a"  "b" 
[2,] "c"  "b"  "a" 
> 
```
### 4、数组
- 矩阵只能有两个维度，数组可以是任意数量的维数。数组函数采用一个dim属性，创建所需的维数。 下面创建一个有两个元素的数组，每个元素都是3x3个矩阵
```
> # Create an array.
> a <- array(c('green','yellow'),dim = c(3,3,2))
> print(a)
, , 1
     [,1]     [,2]     [,3]    
[1,] "green"  "yellow" "green" 
[2,] "yellow" "green"  "yellow"
[3,] "green"  "yellow" "green" 
, , 2
     [,1]     [,2]     [,3]    
[1,] "yellow" "green"  "yellow"
[2,] "green"  "yellow" "green" 
[3,] "yellow" "green"  "yellow"
>  
```
### 5、因子
- 因子是使用向量创建的R对象。 它将向量存储在向量中的元素的不同值作为标签。标签始终是字符，无论它是输入向量中是数字，还是字符或布尔等。它们在统计建模中很有用。
因子使用factor()函数创建。nlevels函数给出了级别的计数
```
> # Create a vector.
> apple_colors <- c('green','green','yellow','red','red','red','green')
> # Create a factor object.
> factor_apple <- factor(apple_colors)
> # Print the factor.
> print(factor_apple)
[1] green  green  yellow red    red    red    green 
Levels: green red yellow
> print(nlevels(factor_apple))
[1] 3
> 
```
### 6、数据帧
- 数据帧是表格数据对象。与数据帧中的矩阵不同，每列可以包含不同的数据模式。 第一列是数字，而第二列可以是字符，第三列可以是逻辑类型。它是一个长度相等的向量列表。
数据帧使用data.frame()函数创建。
```
> # Create the data frame.
> BMI <-     data.frame(
+   gender = c("Male", "Male","Female"), 
+   height = c(152, 171.5, 165), 
+   weight = c(81,93, 78),
+   Age = c(42,38,26)
+ )
> print(BMI)
  gender height weight Age
1   Male  152.0     81  42
2   Male  171.5     93  38
3 Female  165.0     78  26
> 
```
### 二、获取外部数据
### 1、R读写文件
- R可以读取和写入各种文件格式，如：csv，excel，xml、json等。<br>
```
setwd("D:/R")
data <- read.csv("test.csv")
print(data)
```
### 2、R操作数据库
- R可以很容易地连接到许多关系数据库，如：MySQL，Oracle，Sql Server等，并将它们作为数据帧提取。<br>
```
library("RMySQL");
mysqlconnection = dbConnect(MySQL(), user = 'root', password = '123456', dbname = 'testdb',
   host = 'localhost')
dbListTables(mysqlconnection)
```
### 三、数据可视化
### 1、条形图
- R使用barplot()函数来创建条形图。R可以在条形图中绘制垂直和水平条。 在条形图中，每个条可以被赋予不同的颜色<br>
```
setwd("H:/R_Excavate/code/img/3")
H <- c(7,12,28,3,41)
M <- c("一月","二月","三月","四月","五月")
# Give the chart file a name.
png(file = "barchart.png")
# Plot the bar chart.
barplot(H,names.arg = M,xlab = "月份",ylab = "收入量",col = "green",
        main = "收入图表",border = "red")
# Save the file.
dev.off()
```
![图](/code/img/3/barchart.png)
### 2、箱形图
- R中的箱形图通过使用boxplot()函数来创建，表示数据集中的最小值，最大值，中值，第一四分位数和第四四分位数。 通过为每个数据集绘制箱形图，比较数据集中的数据分布也很有用。
```
setwd("H:/R_Excavate/code/img/3")
png(file = "boxplot.png")
# Plot the chart.
boxplot(mpg ~ cyl, data = mtcars, 
        xlab = "气缸数",
        ylab = "每加仑里程", 
        main = "里程数据",
        notch = TRUE, 
        varwidth = TRUE, 
        col = c("blue","green","red"),
        names = c("高","中","低")
)
# Save the file.
dev.off()
```
![图](/code/img/3/boxplot.png)
### 3、直方图
- R使用hist()函数创建直方图。 该函数将一个向量作为输入，并使用一些更多的参数绘制直方图。
```
setwd("H:/R_Excavate/code/img/3")
v <- c(9,13,21,8,36,22,12,41,31,33,19)
# Give the chart file a name.
png(file = "histogram.png")
# Create the histogram.
hist(v, main="直方图示例-2", xlab = "重量", ylab="高度",col = "blue",border = "red", xlim = c(0,40), ylim = c(0,5),
   breaks = 5)
# Save the file.
dev.off()
```
![图](/code/img/3/histogram.png)
### 4、线形图
- R中通过使用plot()函数来创建线形图，可以使用lines()函数在同一个图表上绘制多个直接。
```
setwd("H:/R_Excavate/code/img/3")
# Create the data for the chart.
v <- c(7,12,28,3,41)
t <- c(14,7,6,19,3)
# Give the chart file a name.
png(file = "line_chart.png")
# Plot the bar chart.
plot(v,type = "o",col = "red", xlab = "月份", ylab = "降雨量", 
     main = "降雨量图表")
lines(t, type = "o", col = "blue")
# Save the file.
dev.off()
```
![图](/code/img/3/line_chart.png)
### 5、散点图
- R中简单散点图使用plot()函数来创建，可通过使用pairs()函数来创建散点图的矩阵。
```
setwd("H:/R_Excavate/code/img/3")
png(file = "scatterplot.png")
pairs(~wt+mpg+disp+cyl,data = mtcars,main = "散点图矩阵")
# Save the file.
dev.off()
```
![图](/code/img/3/scatterplot.png)
### 6、饼状图
- 在R中，使用将正数作为向量输入的pie()函数创建饼状图。附加参数用于控制标签，颜色，标题等。可以使用附加包来绘制具有3个维度的饼图。软件包plotrix中有一个名为pie3D()的函数，用于此效果
```
setwd("H:/R_Excavate/code/img/3")
library("plotrix")
# Create data for the graph.
x <-  c(21, 62, 10,53)
lbl <- c("70后", "80后", "90后", "00后")
# Give the chart file a name.
png(file = "3d_pie_chart.jpg")
# Plot the chart.
pie3D(x,labels = lbl,explode = 0.1, main = "出生年龄段 - 饼状图")
# Save the file.
dev.off()
```
![图](/code/img/3/3d_pie_chart.png)