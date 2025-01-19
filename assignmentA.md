# Assignment #A: dp & bfs

Updated 2 GMT+8 Nov 25, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### LuoguP1255 数楼梯

dp, bfs, https://www.luogu.com.cn/problem/P1255

思路：



代码：

```python
dp=[1,1]+[0]*5000
for i in range(2,5000):
    dp[i]=dp[i-1]+dp[i-2]

n=int(input())
print(dp[n])

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

网站出问题登不上去交不了。。。

题目是很简单的

不再浪费时间





### 27528: 跳台阶

dp, http://cs101.openjudge.cn/practice/27528/

思路：一眼看出是前面全部求和，很显然是二的幂次

狄贵同学真是神人



代码：

```python
n=int(input())
print(2**(n-1))
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241203151239810](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241203151239810.png)



### 474D. Flowers

dp, https://codeforces.com/problemset/problem/474/D

思路：爆时间了

用了线段树

优化了数据输入输出

但是再搞就超出我的能力范围了

干脆pypy了



代码：

```python
import sys
data=sys.stdin.readlines()

t,k=map(int,data[0].split())
dp=[1]*100001
for i in range(k,100001):
    dp[i]=(dp[i-1]+dp[i-k])%(10**9+7)
class segmenttree():
    def __init__(self,data):
        self.data=data
        self.n=len(data)
        self.tree=[0]*self.n*4
        self.build(0,0,self.n-1)
    def build(self,node,left,right):
        if left==right:
            self.tree[node]=self.data[left]
            return
        if left<right:
            mid=(left+right)//2
            leftchild=2*node+1
            rightchild=2*node+2
            self.build(leftchild,left,mid)
            self.build(rightchild,mid+1,right)
            self.tree[node]=self.tree[leftchild]+self.tree[rightchild]
    def query(self,node,left,right,start=0,end=None):
        if end==None:
            end=self.n-1
        if left>end or right<start:
            return 0
        if left<=start and right>=end:
            return self.tree[node]
        mid=(start+end)//2
        leftchild=2*node+1
        rightchild=2*node+2
        leftsum=self.query(leftchild,left,right,start,mid)
        rightsum=self.query(rightchild,left,right,mid+1,end)
        return leftsum+rightsum
dp=segmenttree(dp)
ans=[]
for _ in range(t):
    count = 0
    a,b=map(int,data[_+1].split())
    ans.append((dp.query(0,a,b))%(10**9+7))
for l in ans:
    print(l)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241203161126081](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241203161126081.png)



### LeetCode5.最长回文子串

dp, two pointers, string, https://leetcode.cn/problems/longest-palindromic-substring/

思路：一开始直接暴力搜索时间爆了。

后来想到这个方法，但是自己只写了回文长度为奇数的情况

回文长度为偶数时取i+0.5，j-0.5即可，但是我懒得写了，就让gpt顺便写了。



代码：

```python
s = 'bb'  # 输入字符串
maxc = 1  # 最大回文长度
a, b = 0, 1  # 初始化最长回文子串的起始和结束位置

# 奇数位回文中心
for i in range(len(s)):
    c = 1  # 回文长度
    m = min(i + 1, len(s) - i)  # 中心两侧可扩展的最大长度
    for j in range(1, m):
        if s[i + j] == s[i - j]:
            c += 2
        else:
            break
    if c > maxc:
        maxc = c
        a, b = i - c // 2, i + c // 2 + 1

# 偶数位回文中心
for i in range(len(s) - 1):
    if s[i] == s[i + 1]:  # 确保是偶数中心
        c = 2  # 初始回文长度为 2
        m = min(i + 1, len(s) - (i + 1))  # 中心两侧可扩展的最大长度
        for j in range(1, m):
            if s[i - j] == s[i + 1 + j]:
                c += 2
            else:
                break
        if c > maxc:
            maxc = c
            a, b = i - c // 2 + 1, i + c // 2 + 1

# 输出最长回文子串
print(s[a:b])

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241203210248082](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241203210248082.png)





### 12029: 水淹七军

bfs, dfs, http://cs101.openjudge.cn/practice/12029/

思路：绷不住了

oj只告诉我rte

我一直找不出来哪里有问题

chatgpt直接给我秒了

。。。。。。。。。。。。。。

唉



代码：

```python
from collections import deque
import sys

# 读取输入并过滤掉空行
data = [line for line in sys.stdin.read().splitlines() if line.strip()]

# BFS 搜索函数
def bfs(matrix, x, y, target_point, h, visited):
    q = deque([(x, y)])
    visited.add((x, y))
    while q:
        cur_x, cur_y = q.popleft()
        if (cur_x, cur_y) == target_point:
            return True
        for i in range(4):
            next_x = cur_x + dx[i]
            next_y = cur_y + dy[i]
            # 判断是否在范围内，且未访问，且满足高度条件
            if (0 <= next_x < len(matrix) and 0 <= next_y < len(matrix[0]) and
                matrix[next_x][next_y] <= h and (next_x, next_y) not in visited):
                visited.add((next_x, next_y))
                q.append((next_x, next_y))
    return False

# 主程序逻辑
cases = int(data[0])  # 读取案例数
line = 1
dx = [0, 0, 1, -1]
dy = [1, -1, 0, 0]

for _ in range(cases):
    m, n = map(int, data[line].split())
    line += 1
    # 构造带边界的矩阵
    matrix = [[float('inf')] * (n + 2)] + \
             [[float('inf')] + list(map(int, data[line + i].split())) + [float('inf')] for i in range(m)] + \
             [[float('inf')] * (n + 2)]
    line += m
    # 目标点和高度
    target_point = tuple(map(int, data[line].split()))
    line += 1
    target_height = matrix[target_point[0]][target_point[1]]
    t = int(data[line])
    line += 1
    # 读取所有待处理点
    candidates = []
    for _ in range(t):
        x, y = map(int, data[line].split())
        line += 1
        if matrix[x][y] > target_height:
            candidates.append((matrix[x][y], x, y))
    # 按高度降序排序
    candidates.sort(reverse=True)

    # 执行 BFS 查找路径
    visited = set()
    found = False
    for h, x, y in candidates:
        if bfs(matrix, x, y, target_point, h, visited):
            found = True
            break
    print("Yes" if found else "No")

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241203190812964](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241203190812964.png)



### 02802: 小游戏

bfs, http://cs101.openjudge.cn/practice/02802/

思路：死了。

dfs转bfs（看到群里的反例想到的）

一次代码要敲好长时间

还是不熟啊



代码：

```python
import sys
sys.setrecursionlimit(10000000)
from collections import deque
moves=[[1,0],[-1,0],[0,1],[0,-1]]
def bfs(x,y,e):
    q=deque([(x,y,1)])
    visited.add((x,y))
    while q:
        a,b,step=q.popleft()


        for i in range(len(moves)):
            nx=a+moves[i][0]
            ny=b+moves[i][1]
            while 0<=nx<=m+1 and 0<=ny<=n+1:
                if e==[nx,ny]:
                    return step
                if matrix[nx][ny]==1:
                    break
                if (nx,ny) not in visited:
                    q.append((nx,ny,step+1))
                    visited.add((nx,ny))
                nx+=moves[i][0]
                ny+=moves[i][1]
    return 0


count=0
while 1:
    count+=1
    pair=0
    n,m=map(int,input().split())
    if [m,n]==[0,0]:
        exit()
    print(f'Board #{count}:')
    matrix=[[0]* (n+2) for i in range(m+2)]
    for i in range(m):
        a=input()
        for j in range(n):
            if a[j]=='X':
                matrix[i+1][j+1]=1
    while 1:
        pair+=1
        b,a,d,c=map(int,input().split())
        if (a,b,c,d)==(0,0,0,0):
            break
        e=[c,d]
        visited=set()
        minseg=bfs(a,b,e)
        if not minseg:
            print(f'Pair {pair}: impossible.')
            continue
        print(f'Pair {pair}: {minseg} segments.')
    print()
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241203205856244](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241203205856244.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

我太菜了。

呜呜。



