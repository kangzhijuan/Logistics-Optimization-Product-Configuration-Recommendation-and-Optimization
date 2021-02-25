# **三级分类——统型算法**

## **1 算法介绍**
统型目标：压缩元器件选用清单的条目数量（不超出选用清单范围）

统型要求：当两个元器件有替代关系时，保留国产的。

## **2 文件列表**
### 2.1 数据文件
<table>
   <tr>
      <td>名称</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>ID-5</td>
      <td>元器件数量为5的选用清单</td>
   </tr>
   <tr>
      <td>ID-10</td>
      <td>元器件数量为10的选用清单</td>
   </tr>
   <tr>
      <td>ID-20</td>
      <td>元器件数量为20的选用清单</td>
   </tr>
   <tr>
      <td>ID-50</td>
      <td>元器件数量为50的选用清单</td>
   </tr>
   <tr>
      <td>ID-100</td>
      <td>元器件数量为100的选用清单</td>
   </tr>
   <tr>
      <td>replacement-5</td>
      <td>元器件数量为5的替代关系</td>
   </tr>
   <tr>
      <td>replacement-10</td>
      <td>元器件数量为10的替代关系</td>
   </tr>
   <tr>
      <td>replacement-20</td>
      <td>元器件数量为20的替代关系</td>
   </tr>
   <tr>
      <td>replacement-50</td>
      <td>元器件数量为50的替代关系</td>
   </tr>
   <tr>
      <td>replacement-100</td>
      <td>元器件数量为100的替代关系</td>
   </tr>
</table>

### 2.2 算法文件
<table>
   <tr>
      <td>名称</td>
      <td>典型算法模型</td>
      <td>实现方法</td>
      <td>描述</td>
   </tr>
   <tr>
      <td>gurobi</td>
      <td>精确解统型模型、近似解统型模型</td>
      <td>0-1整数规划</td>
      <td>运用gurobi求解器进行统型</td>
   </tr>
   <tr>
      <td>SCIP</td>
      <td>精确解统型模型、近似解统型模型</td>
      <td>0-1整数规划</td>
      <td>运用SCIP求解器进行统型</td>
   </tr>
</table>

## **3 算法流程图**
根据以上提出的统型目标和统型要求，统型算法步骤如下：

首先，输入元器件选用清单和元器件替代关系清单，其中元器件选用清单是包括元器件编号、规格型号、生产厂商、质量等级、封装形式、国产/进口等信息的待统型清单，元器件替代关系清单则表示可以互相替代的元器件关系；

其次，根据根据统型要求对元器件替代关系进行修正，进口元器件不能替代国产元器件；

再次，使用统型算法对元器件选用清单和修正后的元器件替代关系清单进行统型分析，压缩元器件选用清单的条目数量，输出元器件选用清单压缩条目结果形成统型清单；

最后，根据可以统型的元器件清单，结合元器件选用清单，实施统型效果评价，量化评价指标包括元器件规格压缩比例、元器件厂家压缩比例、质量等级压缩比例和国产化提升比例四项，最终输出统型效果评价结果。

统型数据流图如下所示：

![统型数据流图](/统型数据流图.png)

## **4 算法伪代码**
'''javascript
1.	初始化
result={ } 字典，记录每个元器件替代了哪些元器件，也就是统型结果
components_update=ID集合，在后续循环中使用，用于更新还没处理的元器件
count = 1，记录循环次数
'''

## **5 算法用户指南**
### 5.1 python安装包和依赖环境

### 5.2 算法输入输出
#### 算法输入：
元器件选用清单（ID.xlsx）

元器件替代关系（replacement.xlsx）

#### 算法输出：
统型结果（result）

评价指标（indicators)

### 5.3 运行步骤


### 5.4 结果示例
统型结果（result）

![统型结果（result）](/统型结果（result）.png)

评价指标（indicators)

![评价指标（indicators)](/评价指标（indicators).png)

## **6 与其他算法的比较**
精确解和近似解方法在用时上相差不大，精确解能够获得更好的结果。

<table>
   <tr>
      <td>统型前元器件种类</td>
      <td>方法</td>
      <td>用时（秒）</td>
      <td>统型后种类（减少比例）</td>
      <td>备注</td>
   </tr>
   <tr>
      <td rowspan="3">1000</td>
      <td rowspan="2">精确解</td>
      <td>3.81</td>
      <td>490（51%）</td>
      <td>使用Gurobi求解</td>
   </tr>
   <tr>
      <td>4.38</td>
      <td>490（51%）</td>
      <td>使用SCIP求解</td>
   </tr>
   <tr>
      <td>近似解</td>
      <td>2.73</td>
      <td>533（46.7%）</td>
      <td>参数p1=20, p2=100</td>
   </tr>
   <tr>
      <td rowspan="3">3000</td>
      <td rowspan="2">精确解</td>
      <td>16.87</td>
      <td>1451（51.63%）</td>
      <td>使用Gurobi求解</td>
   </tr>
   <tr>
      <td>18.88</td>
      <td>1451（51.63%）</td>
      <td>使用SCIP求解</td>
   </tr>
   <tr>
      <td>近似解</td>
      <td>12.65</td>
      <td>1579（47.37%）</td>
      <td>参数p1=50, p2=150</td>
   </tr>
   <tr>
      <td rowspan="3">5000</td>
      <td rowspan="2">精确解</td>
      <td>22.8</td>
      <td>2445（51.1%）</td>
      <td>使用Gurobi求解</td>
   </tr>
   <tr>
      <td>37.57</td>
      <td>2445（51.1%）</td>
      <td>使用SCIP求解</td>
   </tr>
   <tr>
      <td>近似解</td>
      <td>30.4</td>
      <td>2676（46.48%）</td>
      <td>参数p1=50, p2=150</td>
   </tr>
   <tr>
      <td rowspan="3">10000</td>
      <td rowspan="2">精确解</td>
      <td>89.11</td>
      <td>4456（55.44%）</td>
      <td>使用Gurobi求解</td>
   </tr>
   <tr>
      <td>189.75</td>
      <td>4456（55.44%）</td>
      <td>使用SCIP求解</td>
   </tr>
   <tr>
      <td>近似解</td>
      <td>214.67</td>
      <td>5021（49.79%）</td>
      <td>参数p1=50, p2=150</td>
   </tr>
</table>

## **7 相关开发信息**
<table>
   <tr>
      <td>名称</td>
      <td>人员</td>
      <td>时间</td>
      <td>版本</td>
      <td>状态</td>
   </tr>
   <tr>
      <td>gurobi</td>
      <td>翁欣</td>
      <td>2020年7月6日</td>
      <td>version 1</td>
      <td>已完成</td>
   </tr>
   <tr>
      <td>SCIP</td>
      <td>康至娟</td>
      <td>2020年7月6日</td>
      <td>version 1</td>
      <td>已完成</td>
   </tr>
</table>

## **参考文献**

