# Assignment #7: Nov Mock Exam立冬

Updated 1646 GMT+8 Nov 7, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>付麟瑞 数学学院



**说明：**

1）⽉考： AC4<mark>（请改为同学的通过数）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E07618: 病人排队

sorttings, http://cs101.openjudge.cn/practice/07618/

思路：月考时心态爆炸的开始。一开始不知道bisect——insert不能用key函数，搞了然后报错。后面把key去掉，直接把（年龄，编号）排序，忽略了编号也会算入排序标准，所以WA了，事后一想只能这样



代码：

```python
import bisect
n=int(input())
wl=[]
yx=[]
yx1=[]
for _ in range(n):
    a,b=input().split()
    b=int(b)
    b=-b
    if b<=-60:
        t=bisect.bisect_right(yx,b)
        yx.insert(t,b)
        yx1.insert(t,a)
    else:
        wl.append(a)
for j in yx1:
    print(j)
for k in wl:
    print(k)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>![image-20241112152759478](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241112152759478.png)





### E23555: 节省存储的矩阵乘法

implementation, matrices, http://cs101.openjudge.cn/practice/23555/

思路：



代码：

```python
n,m1,m2=map(int,input().split())
a=[]
b=[]
for i in range(m1):
    x,y,t=map(int,input().split())
    a.append((x,y,t))
for j in range(m2):
    x,y,t=map(int,input().split())
    b.append((x,y,t))
c=[[0]*(n+1) for _ in range(n+1)]
for i in a:
    x,y,t=i
    for j in b:
        if j[0]==y:
            c[x][j[1]]+=t*j[2]
d=[]
for j in range(n):
    for i in range(n):
        if c[j][i]!=0:
            d.append([j,i,c[j][i]])
for i in d:
    print(*i)
```



代码运行截图 ==（至少包含有"Accepted"）==![image-20241112153257229](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241112153257229.png)





### M18182: 打怪兽 

implementation/sortings/data structures, http://cs101.openjudge.cn/practice/18182/

思路：呜呜最难受的一个题了

真的理解错题意了

按照自己以前的游戏经验，以为技能可以留到下一个时刻使用避免堵车，所以写了一个非常复杂的（应该在那个语境下是可以的但是不符合本次题意，硬生生把一个M的题目做成H了，气死人）

唉，为了实现A功能，在本来正确的代码上添加一句话，就会萌生出一些前面讨论不包含的情况，遂报错，然后由于之前的思路里面只是想实现A功能，没有考虑它新带来的影响，所以一个小时查不出来错

sigh



代码：

```python
import bisect
cases=int(input())
for _ in range(cases):
    n,m,b=map(int,input().split())
    time={}
    times=set()
    for qq in range(n):
        t,x=map(int,input().split())
        x=-x
        if t in times:
            bisect.insort_right(time[t], x)
        else:
            times.add(t)
            time[t]=[x]
    times=sorted(list(times))
    gg=1
    for i in times:
        if i>10**9:
            break
        else:
            if len(time[i])>m:
                b+=sum(time[i][:m])
            else:
                b+=sum(time[i])
            if b<=0:
                print(i)
                gg=0
                break
    else:
        if gg:
            print('alive')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241112162833174](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241112162833174.png)



### M28780: 零钱兑换3

dp, http://cs101.openjudge.cn/practice/28780/

思路：披着dp外套的递归（）

用字典爆内存，用经典dp超时，，遂折中，，，



代码：

```python
import sys
sys.setrecursionlimit(10**6)

n,m=map(int,input().split())
a=list(map(int,input().split()))
t=min(a)
dp=[-2]*(m+1)
dp[0]=0
for i in a:
    dp[i]=1
def func(m,a,t):
    if dp[m]!=-2:
        return dp[m]
    if m<t:
        dp[m]=-1
        return -1
    else:
        b=float('inf')
        for i in a:
            if m-i<0:
                l=-1
            else:
                l=func(m-i,a,t)
            if l>=0:
                b=min(b,l+1)
        if b ==float('inf'):
            b=-1
        dp[m]=b
        return b
for i in range(1,m+1):
    func(i,a,t)
print(dp[m])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241112172502870](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241112172502870.png)



### T12757: 阿尔法星人翻译官

implementation, http://cs101.openjudge.cn/practice/12757

思路：



代码：

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### T16528: 充实的寒假生活

greedy/dp, cs10117 Final Exam, http://cs101.openjudge.cn/practice/16528/

思路：



代码：

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

崩溃了。这次真崩溃了。

从想代码开始就把自己绕晕了

到后面优化更是摸不着头脑

太懒不想i敲代码导致的

我学东西真的好慢啊啊啊时间真的不够用





