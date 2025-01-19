# Assignment #2: 语法练习

Updated 0126 GMT+8 Sep 24, 2024

2024 fall, Complied by ==同学的姓名、院系==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 263A. Beautiful Matrix

https://codeforces.com/problemset/problem/263/A



思路：



##### 代码

```python
# for i in range(0, 5):
    r=input().split()
    for j in range(0, 5):
        if r[j] == '1':
            print(abs(i-2)+abs(j-2))

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240924152819598](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20240924152819598.png)



### 1328A. Divisibility Problem

https://codeforces.com/problemset/problem/1328/A



思路：



##### 代码

```python
# for i in range(int(input())):
    a,b=map(int,input().split())
    if a%b==0:
        print(0)
    else:
        print(b-a%b)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240924152753552](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20240924152753552.png)



### 427A. Police Recruits

https://codeforces.com/problemset/problem/427/A



思路：



##### 代码

```python
# a=input()
b=list(map(int,input().split()))
crime=0
police=0
for i in b:
    police+=i
    if police==-1:
        police=0
        crime+=1
print(crime)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240924153741752](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20240924153741752.png)





### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/



思路：



##### 代码

```python
# [length,number]=[int(a) for a in input().split()]
interval=set()
for i in range(0,number):
    [start,end]=[int(a) for a in input().split()]
    for j in range(start,end+1):
        interval.add(j)
print(length+1-len(interval))


```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240924154024770](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20240924154024770.png)

### sy60: 水仙花数II

https://sunnywhy.com/sfbj/3/1/60



思路：



##### 代码

```python
# a,b=map(int,input().split())
list1=[]
for i in range(a,b+1):
    k=0
    for j in str(i):
        k+=int(j)**3
    if k==i:
        list1.append(i)
if len(list1)==0:
    print('NO')
else:
    for i in range(0,len(list1)-1):
        print(list1[i],end=' ')
    print(list1[len(list1)-1])

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240924160114601](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20240924160114601.png)



### 01922: Ride to School

http://cs101.openjudge.cn/practice/01922/



思路：



##### 代码

```python
# 这是我的代码，又长又臭，而且跑出来不知道为什么WA，已经修过好几遍了，这真的不知道哪里还能出问题。这里我的误区是：顺着题意，把思路局限在charley身上，希望通过复现他运动过程来正向解决问题
import math
def crosspoint(a,b):
    v1,v2=a
    t1,t2=b
    return ((v1*t1-v2*t2)/(v1-v2),v1/3.6*((v1*t1-v2*t2)/(v1-v2)-t1))
while 1:
    n=int(input())
    list=[]
    tlist=[]
    if n==0:
        break
    for i in range(1,n+1):
        list.append(tuple(map(int,input().split())))
    for i in list:
        if i[1]>=0:
            tlist.append(i)
    char=min(tlist,key=lambda x:x[1])
    list.remove(char)
    blist=list
    point=crosspoint(char,(0,0))
    while list:
        for i in list:
            if i[0]<=char[0]:
                blist.remove(i)
        list=blist
        xlist=[]
        for i in list:
            if crosspoint(char,i)[0]>point[0]:
                xlist.append((i,crosspoint(char,i)[0]))
        if not xlist:
            break
        char1=min(xlist,key=lambda x:x[1])[0]
        if crosspoint(char1,char)[1]<4500:
            char=char1
            point = crosspoint(char, char1)
        else:
            break
    print(math.ceil(16200/char[0]+char[1]))
```



```python
#这是chatgpt微调的大佬的代码@24-物院-王成睿，从终点看，出发时间晚于charley，到的最早的一个人肯定与charley相遇，那么charley会跟随他，而出发更早且到达更早者不会与charley相遇。由此大大简化问题
import math
import sys

while True:
    n = int(input())
    if n == 0:
        break
    
    ans = float('inf')  # Initialize with infinity

    for _ in range(n):
        a, b = map(int, input().split())
        if b >= 0:  # Only consider riders with non-negative set off times
            # Calculate arrival time
            arrival_time = b + (4500 / (a * (1000 / 3600)))  # Convert speed to m/s
            ans = min(ans, math.ceil(arrival_time))

    print(ans)
```

代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240924222857848](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20240924222857848.png)

![屏幕截图 2024-09-24 222841](d:\Users\m1885\Pictures\Screenshots\屏幕截图 2024-09-24 222841.png)

## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。==

通过这次的作业，我再次学习了一些新的函数的用法，并开始使用def函数来简化过程

同时，我也看出，一个好的思路往往比过程更重要。按照麻烦的思路写一个小时也比不上一个高级的思路。





