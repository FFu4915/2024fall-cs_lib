# Assignment #9: dfs, bfs, & dp

Updated 2107 GMT+8 Nov 19, 2024

2024 fall, Complied by <mark>付麟瑞 数院</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 18160: 最大连通域面积

dfs similar, http://cs101.openjudge.cn/practice/18160

思路：

前面一直re，查了递归深度和边界，甚至测过面积为0的情况

最后发现面积为0是会re的但是当时自己测没测出来

代码：

```python
import sys
sys.setrecursionlimit(1000000)
cases=int(input())
for _ in range(cases):

    m, n = map(int, input().split())
    pond = [[0] * (n + 2) for _ in range(m + 2)]
    for i in range(m):
        a = input()
        for j in range(n):
            if a[j] == 'W':
                pond[i + 1][j + 1] = 1
    t = [(0, 1), (0, -1), (1, 0), (1, 1), (1, -1), (-1, -1), (-1, 0), (-1, 1)]


    def dfs(x, y):
        pond[x][y] = 0
        mianji.append(1)
        for k in t:
            if pond[x + k[0]][y + k[1]] == 1:
                dfs(x + k[0], y + k[1])


    s = []

    count = 0
    for i in range(m):
        for j in range(n):
            if pond[i + 1][j + 1] == 1:
                mianji = []
                dfs(i + 1, j + 1)
                c = sum(mianji)
                s.append(c)
    if not s:
        print(0)
        continue
    print(max(s))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126213636496](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241126213636496.png)



### 19930: 寻宝

bfs, http://cs101.openjudge.cn/practice/19930

思路：



代码：

```python
m,n=map(int,input().split())
matrix=[]
dx=[1,0,-1,0]
dy=[0,1,0,-1]
for _ in range(m):
    a=list(map(int,input().split()))
    matrix.append(a)
matrix2=[[float('inf')]*n for i in range(m)]
steps=[]
step=[[0,0]]
matrix2[0][0]=0
found=0
c=0
if matrix[0][0]==2:
    print('NO')
    exit()
elif matrix[0][0]==1:
    print(0)
    exit()
def func(x,y,c):
    global found
    if matrix[x][y]==1:
        found=c
    matrix2[x][y]=c
    for i in range(4):
        p=x+dx[i]
        q=y+dy[i]
        if 0<=p<=m-1 and 0<=q<=n-1 and matrix[p][q]!=2 and matrix2[p][q]>c:
            steps.append([p,q])


while step and not found:
    for k in step:
        func(k[0],k[1],c)
    c+=1
    step=steps.copy()
    steps.clear()

if not found:
    print('NO')
else:
    print(found)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241126154528735](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241126154528735.png)





### 04123: 马走日

dfs, http://cs101.openjudge.cn/practice/04123

思路：



代码：

```python
moves=[(1,2),(1,-2),(2,1),(2,-1),(-1,2),(-1,-2),(-2,1),(-2,-1)]
cases=int(input())
for _ in range(cases):
    m,n,x,y=map(int,input().split())
    count=0
    board=[[0]*n for i in range(m)]
    def dfs(x,y,m,n,c):
        global count
        if c ==m*n:
            count+=1
            return
        board[x][y]=1
        for t in moves:
            mx=x+t[0]
            ny=y+t[1]
            if 0<=mx<=m-1 and 0<=ny<=n-1 and board[mx][ny]==0:
                dfs(mx,ny,m,n,c+1)
        board[x][y]=0

    dfs(x,y,m,n,1)
    print(count)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126215344045](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241126215344045.png)



### sy316: 矩阵最大权值路径

dfs, https://sunnywhy.com/sfbj/8/1/316

思路：



代码：

```python
movex=[0,0,1,-1]
movey=[1,-1,0,0]
m,n=map(int,input().split())
matrix=[[0]*n for i in range(m)]
count=0
matrix1=[]
for _ in range(m):
    a=list(map(int,input().split()))
    matrix1.append(a)
s=[]
def dfs(x,y,sum,prev):
    if x==m-1 and y==n-1:
        sum+=matrix1[x][y]
        s.append((sum,prev))
    matrix[x][y]=1
    for i in range(len(movex)):
        p=x+movex[i]
        q=y+movey[i]
        if 0<=p<=m-1 and 0<= q<=n-1 and matrix[p][q]==0:
            dfs(p,q,sum+matrix1[x][y],prev+[(p+1,q+1)])
    matrix[x][y]=0
dfs(0,0,matrix1[0][0],[(1,1)])
t=max(s)[1]
for i in t:
    print(i[0],i[1])
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126222431575](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241126222431575.png)





### LeetCode62.不同路径

dp, https://leetcode.cn/problems/unique-paths/

思路：

小学数学题，但是没搞懂这个网站输入怎么回事，一直出问题,索性不理会

代码：

```python
import math
m,n=map(int,input()
ans=math.factorial(m+n-2)/math.factorial(m-1)/math.factorial(n-1)
print(ans)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### sy358: 受到祝福的平方

dfs, dp, https://sunnywhy.com/sfbj/8/3/539

思路：



代码：

```python
n=input()
def dfs(n):
    if not n:
        return 1
    for i in range(len(n)):
        if (int(n[:i+1])**0.5)%1==0:
            if  n[i+1:]=='':
                return 1
            if n[i+1]=='0':
                continue
            if dfs(n[i+1:]):
                return 1
    return 0
if dfs(n):
    print('Yes')
else:
    print('No')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241126225527749](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241126225527749.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>



这次作业比较简单。今天刚结合讲义学习了bfs,dfs,刚好加深了一些理解。

流程比较固定，所以一次AC的多一点，基本没出问题。

