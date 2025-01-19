# Assignment #4: T-primes + 贪心

Updated 0337 GMT+8 Oct 15, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）课程网站是Canvas平台, https://pku.instructure.com, 学校通知9月19日导入选课名单后启用。**作业写好后，保留在自己手中，待9月20日提交。**

提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 34B. Sale

greedy, sorting, 900, https://codeforces.com/problemset/problem/34/B



思路：



代码

```python
# 
n,m=map(int,input().split())
a=list(map(int,input().split()))
a.sort()
sum=0
for i in range(m):
    if a[i]<0:
        sum+=a[i]
    else:
        break
print(-sum)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>![image-20241020170244965](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241020170244965.png)





### 160A. Twins

greedy, sortings, 900, https://codeforces.com/problemset/problem/160/A

思路：



代码

```python


a=input()
b=sorted(list(map(int,input().split())),reverse=True)
s=sum(b)
mine=0
for i in range(len(b)):
    mine+=b[i]
    if mine*2>s:
        ans=i+1
        break
else:
    print(len(b))
print(ans)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241020170655395](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241020170655395.png)



### 1879B. Chips on the Board

constructive algorithms, greedy, 900, https://codeforces.com/problemset/problem/1879/B

思路：



代码

```python
m=int(input())
for i in range(m):
    n=int(input())
    a=list(map(int,input().split()))
    b=list(map(int,input().split()))
    ans=min(sum(a)+n*min(b),sum(b)+n*min(a))
    print(ans)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241020174215823](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241020174215823.png)



### 158B. Taxi

*special problem, greedy, implementation, 1100, https://codeforces.com/problemset/problem/158/B

思路：



代码

```python

import math
a=input()
m=list(map(int,input().split()))
b=[0]*4
for i in m:
    b[i-1]+=1
count=b[3]+b[2]+math.ceil(b[1]/2)
kong=b[2]+2*(b[1]%2)
if kong<b[0]:
    count+=math.ceil((b[0]-kong)/4)
print(count)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241020175040243](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241020175040243.png)



### *230B. T-primes（选做）

binary search, implementation, math, number theory, 1300, http://codeforces.com/problemset/problem/230/B

思路：



代码

```python

origen=set(range(2,1000000))
primes=[]
not_primes=set()
for i in origen:
    if i not in not_primes:
        primes.append(i)
    for j in primes:
        if i*j > 1000000:
            break
        not_primes.add(i*j)
        if i%j==0:
            break
primes=set(primes)
def tprimes(n):
    m=n**0.5
    if m % 1 == 0:
        if m in primes:
            return 'YES'
        return "NO"
    else:
        return "NO"
a=int(input())
b=list(map(int,input().split()))
for k in b:
    print(tprimes(k))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>![image-20241020174413066](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241020174413066.png)





### *12559: 最大最小整数 （选做）

greedy, strings, sortings, http://cs101.openjudge.cn/practice/12559

思路：



代码

```python


```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

感觉最近还需要给自己上上强度，看线段树给自己看吐了，还是太逊



