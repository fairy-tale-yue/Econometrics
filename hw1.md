
# <center>第一次作业

**<center> 171870568 刘悦 金融工程 </center>**

&emsp;&emsp;以下内容是结合ppt第二、第三章内容，利用python对其中的一些主要内容进行了简单的实现，目的是为了对python处理数据的基本操作有一个更加熟悉的了解。下面用到的数据来自于第三章PPT第72页用到的`grilic.dta`，先用stata将其格式转化为`grilic.xls`，随后用python进行后续的处理。


```python
#导入需要用到的工具包
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from pylab import *
mpl.rcParams['font.sans-serif'] = ['SimHei']#为了正常显示中文
matplotlib.rcParams['axes.unicode_minus']=False#为了正常显示负号
```

### 一、导入数据

&emsp;&emsp;首先将excel中的数据导入程序。


```python
data = pd.read_excel('G:\\grilic.xls')
data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rns</th>
      <th>mrt</th>
      <th>smsa</th>
      <th>med</th>
      <th>iq</th>
      <th>kww</th>
      <th>age</th>
      <th>s</th>
      <th>expr</th>
      <th>tenure</th>
      <th>lnw</th>
      <th>wage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>8</td>
      <td>93</td>
      <td>35</td>
      <td>19</td>
      <td>12</td>
      <td>0.462</td>
      <td>0</td>
      <td>5.900</td>
      <td>365.037506</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>14</td>
      <td>119</td>
      <td>41</td>
      <td>23</td>
      <td>16</td>
      <td>0.000</td>
      <td>2</td>
      <td>5.438</td>
      <td>229.981812</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>14</td>
      <td>108</td>
      <td>46</td>
      <td>20</td>
      <td>14</td>
      <td>0.423</td>
      <td>1</td>
      <td>5.710</td>
      <td>301.871094</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>12</td>
      <td>96</td>
      <td>32</td>
      <td>18</td>
      <td>12</td>
      <td>0.333</td>
      <td>1</td>
      <td>5.481</td>
      <td>240.086655</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>6</td>
      <td>74</td>
      <td>27</td>
      <td>26</td>
      <td>9</td>
      <td>9.013</td>
      <td>3</td>
      <td>5.927</td>
      <td>375.027771</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>753</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>8</td>
      <td>113</td>
      <td>45</td>
      <td>26</td>
      <td>16</td>
      <td>0.000</td>
      <td>1</td>
      <td>6.023</td>
      <td>412.815094</td>
    </tr>
    <tr>
      <th>754</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>7</td>
      <td>93</td>
      <td>39</td>
      <td>22</td>
      <td>12</td>
      <td>0.692</td>
      <td>1</td>
      <td>5.176</td>
      <td>176.973526</td>
    </tr>
    <tr>
      <th>755</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>12</td>
      <td>101</td>
      <td>38</td>
      <td>25</td>
      <td>12</td>
      <td>4.828</td>
      <td>0</td>
      <td>5.784</td>
      <td>325.056793</td>
    </tr>
    <tr>
      <th>756</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>7</td>
      <td>100</td>
      <td>33</td>
      <td>23</td>
      <td>12</td>
      <td>2.489</td>
      <td>2</td>
      <td>5.628</td>
      <td>278.105286</td>
    </tr>
    <tr>
      <th>757</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>8</td>
      <td>102</td>
      <td>32</td>
      <td>19</td>
      <td>12</td>
      <td>0.277</td>
      <td>1</td>
      <td>5.075</td>
      <td>159.972168</td>
    </tr>
  </tbody>
</table>
<p>758 rows × 12 columns</p>
</div>



&emsp;&emsp;上表显示其中共有758个数据项，每个数据项有12个属性。从左到右每个属性对应的中文解释如下：

|$rns$   |$mrt$   |$smsa$  |$med$  |$iq$|$kww$|$age$|$s$|$expr$|$tenure$|$lnw$|$wage$|
|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
|是否住在美国南方|是否结婚|是否住在大城市|母亲受教育年限|智商|kww测试成绩|年龄|受教育年限|工龄|在现单位工作年限|工资对数|工资|

### 二、数据预处理

&emsp;&emsp;由于后续过程只需用到$lnw,s,expr,tenure,smsa,rns$这几个变量，因此删除其他变量，并将变量名改为中文。随后显示出表格的前5个数据项。


```python
del data['mrt'],data['med'],data['iq'] ,data['kww'],data['age'],data['wage']
data.rename(columns={'rns':'是否住南方','smsa':'是否在大城市','s':'教育年限','expr':'工龄','tenure':'工作年限','lnw':'工资对数'},\
            inplace = True)
data.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>是否住南方</th>
      <th>是否在大城市</th>
      <th>教育年限</th>
      <th>工龄</th>
      <th>工作年限</th>
      <th>工资对数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>12</td>
      <td>0.462</td>
      <td>0</td>
      <td>5.900</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>16</td>
      <td>0.000</td>
      <td>2</td>
      <td>5.438</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>1</td>
      <td>14</td>
      <td>0.423</td>
      <td>1</td>
      <td>5.710</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>1</td>
      <td>12</td>
      <td>0.333</td>
      <td>1</td>
      <td>5.481</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>1</td>
      <td>9</td>
      <td>9.013</td>
      <td>3</td>
      <td>5.927</td>
    </tr>
  </tbody>
</table>
</div>



### 三、一些基本操作

####  1. 查看数据的基本信息


```python
data.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>是否住南方</th>
      <th>是否在大城市</th>
      <th>教育年限</th>
      <th>工龄</th>
      <th>工作年限</th>
      <th>工资对数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>758.000000</td>
      <td>758.000000</td>
      <td>758.000000</td>
      <td>758.000000</td>
      <td>758.000000</td>
      <td>758.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.269129</td>
      <td>0.704485</td>
      <td>13.405013</td>
      <td>1.735429</td>
      <td>1.831135</td>
      <td>5.686739</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.443800</td>
      <td>0.456575</td>
      <td>2.231828</td>
      <td>2.105542</td>
      <td>1.673630</td>
      <td>0.428949</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>9.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>4.605000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>12.000000</td>
      <td>0.281500</td>
      <td>1.000000</td>
      <td>5.380000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.000000</td>
      <td>1.000000</td>
      <td>12.000000</td>
      <td>0.960000</td>
      <td>1.000000</td>
      <td>5.684000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>16.000000</td>
      <td>2.440000</td>
      <td>2.000000</td>
      <td>5.991000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>18.000000</td>
      <td>11.444000</td>
      <td>10.000000</td>
      <td>7.051000</td>
    </tr>
  </tbody>
</table>
</div>



上表列出了各个变量的描述性统计结果。从中可以看出平均教育年限为13年，相当于中学教育程度。

####  2. 按照变量进行排序


```python
data.sort_values(by='教育年限',inplace = True)
data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>是否住南方</th>
      <th>是否在大城市</th>
      <th>教育年限</th>
      <th>工龄</th>
      <th>工作年限</th>
      <th>工资对数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>257</th>
      <td>0</td>
      <td>1</td>
      <td>9</td>
      <td>3.583</td>
      <td>1</td>
      <td>5.846</td>
    </tr>
    <tr>
      <th>564</th>
      <td>1</td>
      <td>0</td>
      <td>9</td>
      <td>10.609</td>
      <td>1</td>
      <td>6.064</td>
    </tr>
    <tr>
      <th>677</th>
      <td>1</td>
      <td>1</td>
      <td>9</td>
      <td>0.000</td>
      <td>1</td>
      <td>5.075</td>
    </tr>
    <tr>
      <th>402</th>
      <td>0</td>
      <td>1</td>
      <td>9</td>
      <td>0.462</td>
      <td>1</td>
      <td>4.860</td>
    </tr>
    <tr>
      <th>463</th>
      <td>1</td>
      <td>1</td>
      <td>9</td>
      <td>2.500</td>
      <td>2</td>
      <td>5.481</td>
    </tr>
  </tbody>
</table>
</div>



####  3. 计算相关系数矩阵


```python
corrdf = data.corr()
corrdf
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>是否住南方</th>
      <th>是否在大城市</th>
      <th>教育年限</th>
      <th>工龄</th>
      <th>工作年限</th>
      <th>工资对数</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>是否住南方</th>
      <td>1.000000</td>
      <td>-0.161126</td>
      <td>-0.064848</td>
      <td>0.005821</td>
      <td>-0.036551</td>
      <td>-0.149566</td>
    </tr>
    <tr>
      <th>是否在大城市</th>
      <td>-0.161126</td>
      <td>1.000000</td>
      <td>0.102055</td>
      <td>-0.033159</td>
      <td>0.033147</td>
      <td>0.215582</td>
    </tr>
    <tr>
      <th>教育年限</th>
      <td>-0.064848</td>
      <td>0.102055</td>
      <td>1.000000</td>
      <td>-0.241779</td>
      <td>-0.049568</td>
      <td>0.502738</td>
    </tr>
    <tr>
      <th>工龄</th>
      <td>0.005821</td>
      <td>-0.033159</td>
      <td>-0.241779</td>
      <td>1.000000</td>
      <td>0.230744</td>
      <td>0.084615</td>
    </tr>
    <tr>
      <th>工作年限</th>
      <td>-0.036551</td>
      <td>0.033147</td>
      <td>-0.049568</td>
      <td>0.230744</td>
      <td>1.000000</td>
      <td>0.163767</td>
    </tr>
    <tr>
      <th>工资对数</th>
      <td>-0.149566</td>
      <td>0.215582</td>
      <td>0.502738</td>
      <td>0.084615</td>
      <td>0.163767</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



从中可以看出教育年限和工资对数的相关系数较高，达到了0.5027，在一定程度上能够说明受教育时间更长，工资相应的要更高。

#### 4. 画散点图


```python
plt.scatter(data['教育年限'],data['工资对数'])
plt.xlabel('教育年限')
plt.ylabel('工资对数')
plt.show()
```


![png](output_22_0.png)


从上面的散点图可以看出，虽然二者的相关系数不低，但工资水平并非由受教育的年限所决定。并且在教育年限相同的情况下，不同人的工资水平也有较大的差异。

#### 5. 画频率分布直方图


```python
plt.hist(data['工资对数'],bins=25,density=1,edgecolor='black')
plt.xlabel('工资对数')
plt.ylabel('频数')
plt.show()
```


![png](output_25_0.png)


#### 6. 画核密度估计图


```python
from scipy.stats import *
sns.distplot(data['工资对数'],hist_kws={"color":"blue","edgecolor":"k","label":"频率分布直方图"},\
             kde_kws={"color": "red", "label": "核密度估计"},\
             fit=norm,fit_kws={"color": "k", "label": "正态分布"},axlabel='工资对数')
plt.legend()
```




    <matplotlib.legend.Legend at 0x26845f833c8>




![png](output_27_1.png)


从上图可以看出工资对数的分布接近于正态分布，也基本对称。

#### 7. 一些特殊的分布


```python
x = np.linspace(-5,5,100)
y = np.linspace(0.01,8,100)
plt.plot(x,norm.pdf(x),label='正态分布')
plt.plot(y,chi2.pdf(y,4),label='卡方分布')
plt.plot(x,t.pdf(x,1),label='t分布')
plt.plot(y,f.pdf(y,10,1),label='f分布')
plt.vlines(0,0,0.5,color='k',linestyles='dashed')
plt.legend()
```




    <matplotlib.legend.Legend at 0x2684980df48>




![png](output_30_1.png)


上图分别画出了标准正态分布、自由度为4的卡方分布、自由度为1的t分布和自由度为10,1的f分布。
