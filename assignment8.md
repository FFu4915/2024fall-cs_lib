# Assignment #8: 田忌赛马来了

Updated 1021 GMT+8 Nov 12, 2024

2024 fall, Complied by <mark>付麟瑞 数院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 12558: 岛屿周⻓

matices, http://cs101.openjudge.cn/practice/12558/ 

思路：



代码：

```python
count=0
m,n=map(int,input().split())
matrix=[[0]*(n+4)for i in range(2)]
for i in range(m):
    row=list(map(int,input().split()))
    row.append(0)
    row.append(0)
    row.insert(0,0)
    row.insert(0, 0)
    matrix.append(row)
matrix.extend([[0]*(n+4)])
matrix.extend([[0]*(n+4)])
for i in range(1,m+3):
    for j in range(1,n+3):
        if matrix[i][j]==0:
            if matrix[i+1][j]==1:
                count+=1
            if matrix[i-1][j]==1:
                count+=1
            if matrix[i][j+1]==1:
                count+=1
            if matrix[i][j-1]==1:
                count+=1

print(count)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241116220640393](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241116220640393.png)



### LeetCode54.螺旋矩阵

matrice, https://leetcode.cn/problems/spiral-matrix/

与OJ这个题目一样的 18106: 螺旋矩阵，http://cs101.openjudge.cn/practice/18106

思路：这个好玩！

直接一步一步走了



代码：

```python
n=int(input())
matrix=[[0]*n for i in range(n)]
count=1
r=1
l=0
d=0
u=0
i=0
j=0
while 1:
    matrix[i][j]=count
    count+=1
    if count>n*n:
        break
    if r :
        if j==n-1:
            r=0
            d=1
            i+=1
        elif matrix[i][j+1]!=0:
            r = 0
            d = 1
            i += 1
        else:
            j+=1
    elif d:
        if i==n-1:
            d=0
            l=1
            j-=1
        elif matrix[i+1][j]!=0:
            d = 0
            l = 1
            j -= 1
        else:
            i+=1
    elif l:
        if j==0:
            l=0
            u=1
            i-=1
        elif matrix[i][j-1]!=0:
            l=0
            u=1
            i-=1
        else:
            j-=1
    elif u:
        if matrix[i-1][j]!=0:
            u=0
            r=1
            j+=1
        else:
            i-=1
for i in matrix:
    print(*i)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241116222313405](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241116222313405.png)



### 04133:垃圾炸弹

matrices, http://cs101.openjudge.cn/practice/04133/

思路：丢给chatgpt检查之后ac了仔细想了想才发现我之前的思路有问题

这题不能用缓冲带

或者说，最后数的时候不能把缓冲带数上（搞这么麻烦真就不如不用了）

原来缓冲带并没有那么通用，有的时候直接min,maax能解决的问题交给他们就好



代码：

```python
d = int(input())  # 输入偏移量
matrix = [[0] * 1025 for _ in range(1025)]  # 初始化矩阵
n = int(input())  # 输入数据点个数

for _ in range(n):
    x, y, t = map(int, input().split())  # 输入每个数据点的坐标和加值
    
    
    # 更新矩阵区域，添加边界检查
    for i in range(max(0, x - d), min(1024, x + d) + 1):
        for j in range(max(0, y - d), min(1024, y + d) + 1):
            matrix[i][j] += t

# 查找最大值并计算其出现次数
maxcount = 0
count = 1
for i in range(1025):
    for j in range(1025):
        if matrix[i][j] > maxcount:
            maxcount = matrix[i][j]
            count = 1
        elif matrix[i][j] == maxcount:
            count += 1

print(count, maxcount)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241116232623129](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241116232623129.png)





### LeetCode376.摆动序列

greedy, dp, https://leetcode.cn/problems/wiggle-subsequence/

与OJ这个题目一样的，26976:摆动序列, http://cs101.openjudge.cn/routine/26976/

思路：呜呜，丢给gpt检查被训了一顿然后给了一份正确代码

后来发现是检查常数数列的部分写错了=.=



代码：

```python
n=int(input())
a=list(map(int,input().split()))
t=a[0]
count=2
if n==1:
    print(1)
    exit()
elif n==2:
    if a[1]==a[0]:
        print(1)
        exit()
    else:
        print(2)
        exit()
for i in range(1,n-1):
    if t<a[i] and a[i]>a[i+1]:
        count+=1
        t=a[i]
    elif t>a[i] and a[i]<a[i+1]:
        count+=1
        t=a[i]
if count==2:
    count=1
    for i in range(1,n):
        if a[i]!=a[i-1]:
            count=2
            break
print(count)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241117012653424](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241117012653424.png)



### CF455A: Boredom

dp, 1500, https://codeforces.com/contest/455/problem/A

思路：CF上交题看了一遍错误数据就知道自己错哪了。

一开始思维定式了，以为奇数位加起来和偶数位加起来比较就是最优。

拜入dp神教了



代码：

```python
count=[0]*100001
n=input()
a=list(map(int,input().split()))
for i in a:
    count[i]+=i
dp=[0]*100001
for i in range(100001):
    dp[i]=max(dp[i-1],dp[i-2]+count[i])
print(dp[100000])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241119144924295](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241119144924295.png)



### 02287: Tian Ji -- The Horse Racing

greedy, dfs http://cs101.openjudge.cn/practice/02287

思路：很好玩的一个题！关键是讨论平局的情况，涉及到平局数和最小值的维护。

使用平局马的条件一开始没有搞清楚，所以有些地方讨论错了。

没有使用chatgpt自己做的，喜



代码：

```python
while 1:
    n=int(input())
    if n==0:
        break
    a=list(map(int,input().split()))
    b=list(map(int,input().split()))
    a.sort()
    b.sort(reverse=True)
    count=0
    ping=[0,0,0]
    for i in b:
        if a[-1]>i:
            count+=200
            a.pop()
        elif a[-1]<i:
            if ping[0]!=0 :
                if ping[1]>i:
                    ping[0]-=1
                elif ping[1]==i:
                    count-=200
            elif ping[0]==0:
                count-=200
        elif a[-1]==i:
            if ping[0]!=0:
                if ping[1]>i:
                    ping[0]-=1
                    continue   
            ping[0]+=1
            ping[1]=i
            a.pop()
    print(count)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241119003523103](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241119003523103.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

写完欠下的几次数分作业一定狂补计概



