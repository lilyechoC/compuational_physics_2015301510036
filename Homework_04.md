## 第四次作业

### 一、摘要
   T1.1、地球表面自由落体的问题\
    自由落体运动（Free falling movement）,运用Euler Method求出1.1题的近似解，并与其精确解对照。

### 二、背景介绍
- 自由落体运动是初速度为零、加速度为重力加速度的匀加速直线运动。
- 在只考虑重力而忽略其他影响的情况下，由牛顿第二定律可得其运动规律。

### 三、正文
* Euler Method的近似解
>v(t+dt)=v(t)+gdt\
直接求得的解析解\
>v=-gt

* 以下是Python程序：
```python
import numpy as np
import matplotlib.pyplot as plt

def draw_pic(g,v0):
    v0 = float(v0)
    g = float(g)
    v=[]
    v.append(v0)
        
    t = np.linspace(0,0.2,1000)
    #Euler method 数值解
    for i in range(999):
        v_new = v[i]-g*t[1]
        v.append(v_new)
    #exact solution 解析解
    V = v0-g*t          
    #绘图
    plt.figure(figsize=(10,6))
    plt.plot(t,V,label="exact solution",color="red",linewidth=1)
    plt.plot(t,v,label="Euler method",color="green",linewidth=3,linestyle='--')        
    plt.xlabel("Time(t)")
    plt.ylabel("velocity(v)")
    plt.title("Free falling problems")
    plt.legend(loc='best')
    plt.savefig(str(g+v0)+'.png')
    plt.show()

print ('Now you can draw your curve')
g = input('input g:')
v0 = input('input v0:')
draw_pic(g,v0)
```
得到\
Now you can draw your curve\
input g:9.8\
input v0:0


* 结果分析：
近似解与解析解满足相同的线性关系
![image](https://github.com/lilyechoC/compuational_physics_2015301510036/blob/master/04-1.png)


### 四、总结
    验证了Euler method在自由落体运动中给出的近似解即为正确的答案。
    
### 五、致谢
    感谢方勃的指导。


---

   >PS.\
   做完第一题之后觉得有些简单了，于是开始思考蔡老师在课堂上提到的第五题，\
   然而程序老是报错TAT，和同学讨论他们也解决不了。\
   还是贴出错误的程序和图来吧，证明我到此一游TAT
   
```python
# -*- coding: utf-8 -*-
"""
Created on Sat Sep 29 20:10:42 2017

@author: qmcqi
"""

import numpy as np
import pylab as pl
Number_A=[]    
Number_B=[]
t=[]
print("the number of A atoms ->")
number_a=input()
Number_A.append(number_a)
print("the number of B atoms ->")
number_b=input()
Number_B.append(number_b)
print("the time of decay ->")
t_decay=input()
print("the time step ->")
dt=input()
def Bigger(a,b):
  if a>b:
      return a
  else:
      return b
def Smaller(a,b):
  if a>b:
      return b
  else:
      return a
big=Bigger(Number_A[0],Number_B[0])
small=Smaller(Number_A[0],Number_B[0])
t.append(0.0)
for i in range(100):
  NA=Number_A[i]+int((float(Number_B[i])-float(Number_A[i]))/float(t_decay))*dt
  NB=Number_B[i]+int((float(Number_A[i])-float(Number_B[i]))/float(t_decay))*dt
  tadd=int(float(t[i])+float(dt))
  Number_A.append(NA)
  Number_B.append(NB)
  t.append(tadd)
t_max=t[-1]
pl.plot(t,Number_A,'r')
pl.plot(t,Number_B,'g')
pl.title('the decay between A and B')
pl.xlabel('the time of decaying')
pl.ylabel('number of atoms')
pl.xlim(0.0,t_max)
pl.ylim(small,big)
pl.show()

```
   
![image](https://github.com/lilyechoC/compuational_physics_2015301510036/blob/master/04-2.png)   
谢谢老师ORZ
