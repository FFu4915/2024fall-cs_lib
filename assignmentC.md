# Assignment #C: 五味杂陈 

Updated 1148 GMT+8 Dec 10, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 1115. 取石子游戏

dfs, https://www.acwing.com/problem/content/description/1117/

思路：观察到当两堆数量达到2倍以上的时候有必胜策略即可



代码：

```python
def func(m,n):
    a=max(m,n)
    b=min(m,n)
    if a==b or a>=b*2:
        return True
    return not func(a-b,b)
while 1:
    a,b=map(int,input().split())
    if a==0 and b==0:
        break
    print('win' if func(a,b) else 'lose')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241217193950105](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241217193950105.png)



### 25570: 洋葱

Matrices, http://cs101.openjudge.cn/practice/25570

思路：损失了点时间复杂度但不多

但是代码简单易写

不用细想



代码：

```python
n=int(input())
onion=[]
maxsum=0
for _ in range(n):
    onion.append(list(map(int,input().split())))
for t in range(n):
    if t>n-t-1:
        break
    cengsum=0
    for i in range(n):
        cengsum+=onion[i][t]
        onion[i][t]=0
        cengsum+=onion[i][n-t-1]
        onion[i][n-t-1]=0
        cengsum+=onion[t][i]
        onion[t][i]=0
        cengsum+=onion[n-t-1][i]
        onion[n-t-1][i]=0
    maxsum=max(maxsum,cengsum)
print(maxsum)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241217195216563](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241217195216563.png)



### 1526C1. Potions(Easy Version)

greedy, dp, data structures, brute force, *1500, https://codeforces.com/problemset/problem/1526/C1

思路：我的思路直来直去

中间因为要依次改dp而把正向range改成反向，但是break忘记改成continue，出了问题，gpt给出了另一种思路，即维护负面药水，当生命值为负时考虑替换。这比我强多了

时间复杂度与代码复杂度都远小于我的呢



代码：

```python
n=int(input())
potions=list(map(int,input().split()))
dp=[0]*2005
m=0
for i in range(n):
    if potions[i]<0:
        for j in range(m+1,0,-1):
            t=dp[j-1]+potions[i]
            if t<0:
                continue
            else:
                if j==m+1:
                    m+=1
                    dp[j]=t
                    continue
                dp[j]=max(dp[j],t)
    else:
        m+=1
        for j in range(m,0,-1):
            dp[j]=max(dp[j],potions[i]+dp[j-1])
print(m)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241217205529955](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241217205529955.png)



### 22067: 快速堆猪

辅助栈，http://cs101.openjudge.cn/practice/22067/

思路：第一次忘记try了，被re吓了一跳



代码：

```python
n=0
m=[0]*100002
m[0]=float('inf')
while 1:
    try:
        msg=input()
    except EOFError:
        break
    if msg=='pop':
        if n==0:
            continue
        else:
            n-=1
            m[n+1]=0
    elif msg=='min':
        if n==0:
            continue
        else:
            print(m[n])
    else:
        a,b=msg.split()
        b=int(b)
        n+=1
        m[n]=min(m[n-1],b)

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>



![image-20241217210600730](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241217210600730.png)

### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/

思路：学了dijkstra和heapq（这个是gpt告诉我的）

比较怀旧，用deque用的顺，就尝试deque+bisect，WA。

将优先队列用heapq解决之后就AC



代码：

```python
import heapq

moves = [[0, 1], [0, -1], [1, 0], [-1, 0]]

def Dijkstra(s, e, m, n):
    # 优先队列
    q = []
    heapq.heappush(q, (0, s))  # (距离, 坐标)
    dist = [[float('inf')] * n for _ in range(m)]  # 距离数组
    dist[s[0]][s[1]] = 0
    visited = set()

    while q:
        d, front = heapq.heappop(q)
        if front == e:
            return d

        if front in visited:
            continue
        visited.add(front)

        u, v = front
        for move in moves:
            x = u + move[0]
            y = v + move[1]
            if 0 <= x < m and 0 <= y < n and (x, y) not in visited and matrix[x][y] != '#':
                # 计算新的距离
                new_dist = d + abs(int(matrix[u][v]) - int(matrix[x][y]))
                if new_dist < dist[x][y]:
                    dist[x][y] = new_dist
                    heapq.heappush(q, (new_dist, (x, y)))
    return 'NO'

# 输入部分
m, n, p = map(int, input().split())
matrix = [list(input().split()) for _ in range(m)]

for _ in range(p):
    a, b, c, d = map(int, input().split())
    s = (a, b)
    e = (c, d)

    # 检查起点和终点是否是墙
    if matrix[a][b] == '#' or matrix[c][d] == '#':
        print('NO')
        continue
    
    # 执行 Dijkstra 算法
    print(Dijkstra(s, e, m, n))

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241217222019165](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241217222019165.png)



### 04129: 变换的迷宫

bfs, http://cs101.openjudge.cn/practice/04129/

思路：实在没思路



代码：

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

还行

