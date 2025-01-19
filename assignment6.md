# Assignment #6: Recursion and DP

Updated 2201 GMT+8 Oct 29, 2024

2024 fall, Complied by <mark>数院 付麟瑞 2400010844</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### sy119: 汉诺塔

recursion, https://sunnywhy.com/sfbj/4/3/119  

思路：



代码：

```python
n=int(input())
print(2**n-1)
def move(n,A,B,C):
    if n>1:
        move(n-1,A,C,B)
        print(f'{A}->{C}')
        move(n-1,B,A,C)
    elif n==1:
        print(f'{A}->{C}')
move(n,'A','B','C')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241103221440080](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241103221440080.png)



### sy132: 全排列I

recursion, https://sunnywhy.com/sfbj/4/3/132

思路：



代码：

```python
import itertools
a=list(range(1,int(input())+1))
aa=itertools.permutations(a)
for i in aa:
    print(*i)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241103222517806](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241103222517806.png)



### 02945: 拦截导弹 

dp, http://cs101.openjudge.cn/2024fallroutine/02945

思路：



代码：

```python
n=int(input())
ceng=[1]*(n+1)
a=list(map(int,input().split()))
for i in range(n):
    for j in range(i):
        if a[i]<=a[j]:
            ceng[i]=max(ceng[i],ceng[j]+1)
print(max(ceng))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241103223124428](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241103223124428.png)



### 23421: 小偷背包 

dp, http://cs101.openjudge.cn/practice/23421

思路：



代码：

```python
n,b=map(int,input().split())
prices=list(map(int,input().split()))
weights=list(map(int,input().split()))
dp=[[0]*(b+1)for k in range(n+1)]
for i in range(n):
    for j in range(b):
        if weights[i]<=j+1:
            dp[i+1][j+1]=max(dp[i][j+1],dp[i][j+1-weights[i]]+prices[i])
        else:
            dp[i + 1][j + 1] = dp[i][j + 1]
print(dp[n][b])

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241103231135963](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241103231135963.png)



### 02754: 八皇后

dfs and similar, http://cs101.openjudge.cn/practice/02754

思路：



代码：

```python
import itertools
n=int(input())
a=itertools.permutations(range(1,9))
queens=[]
for k in a:
    b=set()
    c=set()
    for i in range(8):
        b.add(k[i]+i)
        c.add(k[i]-i)
    if len(b)==8 and len(c)==8:
        queens.append(''.join(map(str,k)))
for _ in range(n):
    print(queens[int(input())-1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241103233416076](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241103233416076.png)



### 189A. Cut Ribbon 

brute force, dp 1300 https://codeforces.com/problemset/problem/189/A

思路：



代码：

```python
n,a,b,c=map(int,input().split())
t=min(a,b,c)
dic={t:1}
d=sorted([a,b,c])
if d[1]%d[0]==0:
    dic[d[1]]=d[1]//d[0]
else:
    dic[d[1]]=1
for i in range(d[2]):
    m=d[2]-i*d[1]
    if m %d[0]==0:
        dic[d[2]]=i+m//d[0]
        break
    if m<0:
        dic[d[2]]=1
        break
for i in range(-4000,t):
    dic[i]=0
def func(l,a,b,c):
    if l in dic:
        return dic.get(l)
    else:
        m=max(func(l-a,a,b,c),func(l-b,a,b,c),func(l-c,a,b,c))+1
        if m==1:
            dic[l]=0
            return 0
        else:
            dic[l]=m
            return m
for i in range(n+1):
    func(i,a,b,c)
print(dic[n])

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>![image-20241104003612690](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241104003612690.png)





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

最近不定时学习，属于是看心情学了。有的知识点，一长串代码看起来就让人头疼，但是尝试理解其思路或者是在问题中使用它的过程却很有意思。在反复优化代码的过程中收获颇丰。不断想办法应对递归次数过多报错，超时等挑战很令人兴奋。目前状态不错，也找到了适合自己的学习方法，打算加快进度了



