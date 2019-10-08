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
	* [四、数据分析](#四数据分析)
		* [1、回归分析](#1回归分析)
		* [2、决策树分析](#2决策树分析)
		* [3、支持向量机SVM](#3支持向量机SVM)
		* [4、随机森林算法](#4随机森林算法)
		* [5、时间序列分析](#5时间序列分析)
		* [6、卡方检验](#6卡方检验)
		* [7、聚类分析](#7聚类分析)
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
![图](/code/img/3/3d_pie_chart.jpg)
### 与四、数据分析
### 1、回归分析
- 回归分析用于建立两个变量之间的关系模型。 这些变量之一称为预测变量，其值通过实验收集。 另一个变量称为响应变量，其值来自预测变量。<br>
lm()函数创建预测变量与响应变量之间的关系模型
- 线性回归例子：根据一个人的已知身高来预测人的体重
```
setwd("H:/R_Excavate/code/img/4")
x <- c(151, 174, 138, 186, 128, 136, 179, 163, 152, 131)
y <- c(63, 81, 56, 91, 47, 57, 76, 72, 62, 48)
relation <- lm(y~x)
# Give the chart file a name.
png(file = "linearregression.png")
# Plot the chart.
plot(y,x,col = "blue",main = "身高和体重回归",
     abline(lm(x~y)),cex = 1.3,pch = 16,xlab = "体重(Kg)",ylab = "身高(cm)")
# Save the file.
dev.off()
```
![图](/code/img/4/linearregression.png)
### 2、决策树分析
- 决策树是以树的形式表示选择及其结果的图形。图中的节点表示事件或选择，并且图形的边缘表示决策规则或条件。它主要用于使用R的机器学习和数据挖掘应用程序<br>
- 决策的例子：将接收的邮件预测是否为垃圾邮件，根据这些信息中的因素，预测肿瘤是癌症或预测贷款作为良好或不良的信用风险。
- 使用ctree()函数创建决策树并查看其生成的图表
```
#install.packages("party")
setwd("H:/Workspaces/pycharm/R_Excavate/code/img/4")
library(party)
# Create the input data frame.
input.dat <- readingSkills[c(1:102),]
# Give the chart file a name.
png(file = "decision_tree.png")
# Create the tree.
output.tree <- ctree(
  nativeSpeaker ~ age + shoeSize + score, 
  data = input.dat)
# Plot the tree.
plot(output.tree)
# Save the file.
dev.off()
```
![图](/code/img/4/decision_tree.png)
### 3、支持向量机SVM
- 支持向量机(SVM)是一种线性和非线性数据的分类方法，支持向量机可用于回归、分类和异常检验，前者即为支持向量机回归，后者为支持向量机分类。<br>
- 支持向量机的例子：手写数字识别、对象识别、演说人识别，以及基准时间序列预测检验。
- 使用kernlab包创建支持向量机
```
library(kernlab)
irismodel <- ksvm(Species ~ ., data = iris,              
                  type = "C-bsvc", kernel = "rbfdot",                    
                  kpar = list(sigma = 0.1), C = 10,                    
                  prob.model = TRUE)
irismodel
predict(irismodel, iris[c(3, 10, 56, 68, 107, 120), -5], type = "probabilities")
```
![图](/code/img/4/svm.png)
### 4、随机森林算法
- 随机森林拥有广泛的应用前景，从市场营销到医疗保健保险，既可以用来做市场营销模拟的建模，统计客户来源，保留和流失，也可用来预测疾病的风险和病患者的易感性。<br>
```
library(party)
library(randomForest)
# Create the forest.
output.forest <- randomForest(nativeSpeaker ~ age + shoeSize + score,data = readingSkills)
# View the forest results.
print(output.forest) 
```
![图](/code/img/4/randomForest.png)<br>
结论：从上面显示的可以得出结论，鞋码和成绩是决定如果某人是母语者或不是母语的重要因素。 此外，该模型只有1%的误差，这意味着我们可以预测精度为99%。
### 5、时间序列分析
- 时间序列分析是定量预测方法之一。它包括一般统计分析(如自相关分析，谱分析等)，统计模型的建立与推断，以及关于时间序列的最优预测、控制与滤波等内容<br>
- 多时间序列：通过将两个系列组合成一个矩阵，在一个图表中绘制多个时间序列
```
setwd("H:/Workspaces/pycharm/R_Excavate/code/img/4")
rainfall1 <- c(799,1174.8,865.1,1334.6,635.4,918.5,685.5,998.6,784.2,985,882.8,1071)
rainfall2 <- 
  c(655,1306.9,1323.4,1172.2,562.2,824,822.4,1265.5,799.6,1105.6,1106.7,1337.8)
# Convert them to a matrix.
combined.rainfall <-  matrix(c(rainfall1,rainfall2),nrow = 12)
# Convert it to a time series object.
rainfall.timeseries <- ts(combined.rainfall,start = c(2012,1),frequency = 12)
# Print the timeseries data.
print(rainfall.timeseries)
# Give the chart file a name.
png(file = "rainfall_combined.png")
# Plot a graph of the time series.
plot(rainfall.timeseries, main = "Multiple Time Series")
# Save the file.
dev.off()
```
![图](/code/img/4/rainfall_combined.png)
### 6、卡方检验
- 卡方检验是一种确定两个分类变量之间是否存在显着相关性的统计方法。 这两个变量应该来自相同的人口，他们应该是类似 - 是/否，男/女，红/绿等<br>
- 用于执行卡方检验的函数是chisq.test()。
- 实例：在“MASS”图书馆中获取Cars93数据，该图书馆代表1993年不同型号汽车的销售额，找出所售的汽车类型和安全气囊类型之间的任何显着的相关性
```
setwd("H:/Workspaces/pycharm/R_Excavate/code/img/4")
rainfall1 <- c(799,1174.8,865.1,1334.6,635.4,918.5,685.5,998.6,784.2,985,882.8,1071)
rainfall2 <- 
  c(655,1306.9,1323.4,1172.2,562.2,824,822.4,1265.5,799.6,1105.6,1106.7,1337.8)
# Convert them to a matrix.
combined.rainfall <-  matrix(c(rainfall1,rainfall2),nrow = 12)
# Convert it to a time series object.
rainfall.timeseries <- ts(combined.rainfall,start = c(2012,1),frequency = 12)
# Print the timeseries data.
print(rainfall.timeseries)
# Give the chart file a name.
png(file = "rainfall_combined.png")
# Plot a graph of the time series.
plot(rainfall.timeseries, main = "Multiple Time Series")
# Save the file.
dev.off()
```
![图](/code/img/4/car.png)<br>
结论：结果显示p值小于0.05，这表明字符串相关
### 7、聚类分析
- 聚类分析，对样品或指标进行分类的一种分析方法，依据样本和指标已知特性进行分类。
- 实例：现有5个样本，每个样本只有一个指标，分别为1，2，6，8，11，样本间的距离选用Euclide距离，用最短距离法，最长距离法等进行聚类分析，画出相应的树状图。
```
# 数据读取
x<-c(1,2,6,8,11)
# 定义矩阵
dim(x)<-c(5,1)
#计算距离
d<-dist(x)
#聚类分析
hc1<-hclust(d, "single")
hc2<-hclust(d, "complete")
hc3<-hclust(d, "median")
hc4<-hclust(d, "mcquitty")
#绘图分栏
par(mfrow = c(2, 2))
#绘图
plot(hc1,hang=-1)
plot(hc2,hang=-1)
plot(hc3,hang=-1)
plot(hc4,hang=-1)
par(opar)
#演示plot的用法
dend1<-as.dendrogram(hc1)
opar <- par(mfrow = c(2, 2),mar = c(4,3,1,2))
plot(dend1)
plot(dend1, nodePar=list(pch = c(1,NA), cex=0.8, lab.cex=0.8), type = "t", center=TRUE)
plot(dend1, edgePar=list(col = 1:2, lty = 2:3), dLeaf=1, edge.root = TRUE)
plot(dend1, nodePar=list(pch = 2:1, cex=.4*2:1, col=2:3), horiz=TRUE)
par(opar)
```
![图](/code/img/4/cluster.png)<br>