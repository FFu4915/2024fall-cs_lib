# Assignment #B: Dec Mock Exam大雪前一天

Updated 1649 GMT+8 Dec 5, 2024

2024 fall, Complied by <mark>数院付麟瑞</mark>



**说明：**

1）⽉考： AC6<mark>（请改为同学的通过数）</mark> 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E22548: 机智的股民老张

http://cs101.openjudge.cn/practice/22548/

思路：



代码：

```python
a=list(map(int,input().split()))
xiao=a.copy()
da=a.copy()
n=len(a)
for i in range(1,n):
    xiao[i]=min(xiao[i],xiao[i-1])
for i in range(n-2,-1,-1):
    da[i]=max(da[i],da[i+1])
c=0
for i in range(n):
    c=max(c,da[i]-xiao[i])
print(c)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241205193805119](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241205193805119.png)



### M28701: 炸鸡排

greedy, http://cs101.openjudge.cn/practice/28701/

思路：乍一看不简单，但是看到greedy以后会心一笑（）

：。3f是问的gpt



代码：

```python
n,m=map(int,input().split())
a=list(map(int,input().split()))
a.sort()
s=sum(a)
while 1:
    t=a.pop()
    if t*m>s:
        m-=1
        s-=t
    else:
        print(f'{s/m:.3f}')
        break
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241205195423577](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241205195423577.png)



### M20744: 土豪购物

dp, http://cs101.openjudge.cn/practice/20744/

思路：一开始甚至在考场中手搓线段树。。。。

其实线段树感觉也要n^3左右的时间复杂度了

然后也试过好多方法，过于复杂

后来在纸上一画才发现原来这么简单



代码：

```python
a=list(map(int,input().split(',')))
n=len(a)
maxcount=0
maxqian=[a[0]]+[-float('inf')]*(n-1)
for i in range(1,n):
    maxqian[i]=max(maxqian[i-1]+a[i],a[i])
maxhou=[-float('inf')]*(n-1)+[max(0,a[-1])]
for i in range(n-2,-1,-1):
    maxhou[i]=max(maxhou[i+1]+a[i],a[i],0)
for i in range(n-2):
    maxcount=max(maxcount,maxqian[i],maxhou[i+2]+maxqian[i])
maxcount=max(maxcount,maxqian[n-1],maxqian[n-2])
print(maxcount)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241205193544165](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241205193544165.png)



### T25561: 2022决战双十一

brute force, dfs, http://cs101.openjudge.cn/practice/25561/

思路：就是麻烦，不难，但是真的麻烦，出点问题要花半天解决



代码：

```python
n,m=map(int,input().split())
juan=[[]for i in range(m)]
prices=[[float('inf')]*m for _ in range(n)]
shops=[0]*m
final=0
final_prices=[]
for i in range(n):
    info=list(input().split())
    for j in range(len(info)):
        shop,price=map(int,info[j].split(':'))
        prices[i][shop-1]=price
for i in range(m):
    info=list(input().split())
    for j in range(len(info)):
        x,y=map(int,info[j].split('-'))
        juan[i].append((x,y))
def dfs(n,m,i=0,total=0):
    if i == n:
        final=total-50*(total//300)
        for j in range(m):
            jian=0
            for k in juan[j]:
                if shops[j]>=k[0]:
                    jian=max(jian,k[1])
            final-=jian
        final_prices.append(final)
        return
    for j in range(m):
        if prices[i][j]==float('inf'):
            continue
        shops[j]+=prices[i][j]
        dfs(n,m,i+1,total+int(prices[i][j]))
        shops[j]-=prices[i][j]


dfs(n,m,0)
print(min(final_prices))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241205193435053](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241205193435053.png)



### T20741: 两座孤岛最短距离

dfs, bfs, http://cs101.openjudge.cn/practice/20741/

思路：相同的思路，我的代码跑不出来，chatgpt的代码随便ac

唉，可能这就是天赋罢

What can I say?

啊啊啊受不了了chatgpt你快给我开个共享文档帮我考期末吧呜呜呜呜



代码：

```python
from collections import deque

# 定义四个方向
moves = [[0, 1], [0, -1], [1, 0], [-1, 0]]

# 输入
n = int(input())
matrix = [list(map(int, input())) for _ in range(n)]

# 标记第一个孤岛，并返回边界点
def mark_island(x, y):
    queue = deque()
    boundary = deque()
    queue.append((x, y))
    matrix[x][y] = 2  # 标记第一个孤岛
    while queue:
        cx, cy = queue.popleft()
        for dx, dy in moves:
            nx, ny = cx + dx, cy + dy
            if 0 <= nx < n and 0 <= ny < n:
                if matrix[nx][ny] == 1:  # 孤岛内部
                    matrix[nx][ny] = 2
                    queue.append((nx, ny))
                elif matrix[nx][ny] == 0:  # 边界点
                    boundary.append((cx, cy))
    return boundary

# 从边界点开始 BFS 搜索最短桥
def bfs(boundary):
    step = 0
    while boundary:
        for _ in range(len(boundary)):
            x, y = boundary.popleft()
            for dx, dy in moves:
                nx, ny = x + dx, y + dy
                if 0 <= nx < n and 0 <= ny < n:
                    if matrix[nx][ny] == 1:  # 找到第二个孤岛
                        return step
                    elif matrix[nx][ny] == 0:  # 水域，扩展搜索
                        matrix[nx][ny] = 2
                        boundary.append((nx, ny))
        step += 1
    return -1

# 主程序
boundary = None
for i in range(n):
    for j in range(n):
        if matrix[i][j] == 1:  # 找到第一个孤岛
            boundary = mark_island(i, j)
            break
    if boundary:
        break

# 输出结果
print(bfs(boundary))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241205205458572](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241205205458572.png)



### T28776: 国王游戏

greedy, http://cs101.openjudge.cn/practice/28776

思路：考虑交换两人位置，要把左右手乘积大者放在后面（容易证明这样不影响其他人而且最后结果更小）



代码：

```python
n=int(input())
p,q=map(int,input().split())
a=[]
for i in range(n):
    x,y=map(int,input().split())
    a.append((x*y,x,y))
a.sort()
ji=p
m=p//a[0][2]
for i in range(1,n):
    ji*=a[i-1][1]
    m=max(m,ji//a[i][2])
print(m)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241205193219537](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241205193219537.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>





