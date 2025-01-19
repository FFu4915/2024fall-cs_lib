# Assignment #D: 十全十美 

Updated 1254 GMT+8 Dec 17, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 02692: 假币问题

brute force, http://cs101.openjudge.cn/practice/02692

思路：



代码：

```python

n=int(input())
for _ in range (n):
    zhen = [0] * 12
    lighter=[1]*12
    heavier=[1]*12
    for __ in range(3):
        lhs,rhs,fuhao=input().split()
        if fuhao=='even':
            for i in lhs:
                zhen[ord(i)-65]=1
            for i in rhs:
                zhen[ord(i) - 65] = 1
        if fuhao=='down':
            for i in rhs:
                lighter[ord(i)-65]=0
            for i in lhs:
                heavier[ord(i)-65]=0
            for i in range(12):
                if (chr(i+65) not in lhs) and (chr(i+65) not in rhs):
                    zhen[i] = 1
        if fuhao=='up':
            for i in lhs:
                lighter[ord(i)-65]=0
            for i in rhs:
                heavier[ord(i)-65]=0
            for i in range(12):
                if (chr(i+65) not in lhs )and( chr(i+65) not in rhs):
                    zhen[i] = 1
    for i in range(12):
        if not zhen[i]:
            if lighter[i]:
                print(f'{chr(i+65)} is the counterfeit coin and it is light.')
                break
            if heavier[i]:
                print(f'{chr(i+65)} is the counterfeit coin and it is heavy.')
                break

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241224152101260](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241224152101260.png)



### 01088: 滑雪

dp, dfs similar, http://cs101.openjudge.cn/practice/01088

思路：



代码：

```python
m,n=map(int,input().split())
matrix=[list(map(int,input().split())) for i in range(m)]
matrix2=[[0]*n for i in range(m)]
moves=[[0,1],[0,-1],[1,0],[-1,0]]
def dfs(x,y,m,n):
    if matrix2[x][y]!=0:
        return matrix2[x][y]
    t=1
    for i in moves:
        nx=x+i[0]
        ny=y+i[1]
        if 0<=nx<m and 0<=ny<n and matrix[x][y]>matrix[nx][ny]:
            t=max(t,dfs(nx,ny,m,n)+1)
    matrix2[x][y]=t
    return t
c=1
for i in range(m):
    for j in range(n):
        c=max(c,dfs(i,j,m,n))
print(c)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241224153847065](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241224153847065.png)



### 25572: 螃蟹采蘑菇

bfs, dfs, http://cs101.openjudge.cn/practice/25572/

思路：



代码：

```python
from collections import deque
n=int(input())
maze=[list(map(int,input().split())) for i in range(n)]
moves=[[0,1],[0,-1],[1,0],[-1,0]]
def bfs(s1,s2,e,n):
    q=deque([(s1,s2)])
    inq_set=set([(s1,s2)])
    while q:
        p1,p2=q.popleft()
        if p1 ==e or p2 ==e:
            return 'yes'
        for i in moves:
            x1=p1[0]+i[0]
            y1=p1[1]+i[1]
            x2=p2[0]+i[0]
            y2=p2[1]+i[1]
            if 0<=x1<n and 0<=y1<n and 0<=x2<n and 0<=y2<n and maze[x1][y1]!=1 and maze[x2][y2]!=1 and((x1,y1),(x2,y2))not in inq_set:
                inq_set.add(((x1,y1),(x2,y2)))
                q.append(((x1,y1),(x2,y2)))
    return 'no'
start=[]
for i in range(n):
    for j in range(n):
        if maze[i][j]==9:
            e=(i,j)
        elif maze[i][j]==5:
            start.append((i,j))
s1=start[0]
s2=start[1]
print(bfs(s1,s2,e,n))
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241224160229138](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241224160229138.png)



### 27373: 最大整数

dp, http://cs101.openjudge.cn/practice/27373/

思路：



代码：

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





### 02811: 熄灯问题

brute force, http://cs101.openjudge.cn/practice/02811

思路：花了点时间理解了这个问题。先穷举第一行所有按灯情况，随后下面的每一行只能由上面一行决定，这样得到的结果是唯一的。

对每个穷举结果，接下来如果最后可以全部熄灭，则得到解，否则continue

代码完成部分较为重复，给ai完成



代码：

```python
import copy

def toggle(matrix, r, c):
    """按下(r, c)处的按钮，改变灯的状态"""
    if 0 <= r < 5 and 0 <= c < 6:
        matrix[r][c] ^= 1  # 当前按钮位置
    if 0 <= r - 1 < 5:  # 上方
        matrix[r - 1][c] ^= 1
    if 0 <= r + 1 < 5:  # 下方
        matrix[r + 1][c] ^= 1
    if 0 <= c - 1 < 6:  # 左边
        matrix[r][c - 1] ^= 1
    if 0 <= c + 1 < 6:  # 右边
        matrix[r][c + 1] ^= 1

def solve_lights_out(matrix):
    best_press = None  # 用于保存最终的按按钮方案

    # 穷举第一行的按法（2^6 种情况）
    for first_row_press in range(1 << 6):  # 0 到 63
        # 按钮记录矩阵，用于保存按下的按钮
        press = [[0] * 6 for _ in range(5)]
        # 当前灯状态，深拷贝初始状态
        current_matrix = copy.deepcopy(matrix)
        
        # 应用第一行的按法
        for j in range(6):
            if (first_row_press >> j) & 1:  # 如果第 j 个按钮被按下
                press[0][j] = 1
                toggle(current_matrix, 0, j)
        
        # 按第二行到第五行
        for i in range(1, 5):
            for j in range(6):
                if current_matrix[i - 1][j] == 1:  # 如果上一行第 j 个灯亮
                    press[i][j] = 1
                    toggle(current_matrix, i, j)

        # 检查最后一行是否全部熄灭
        if all(current_matrix[4][j] == 0 for j in range(6)):
            best_press = press  # 找到解
            break

    return best_press

# 输入部分
matrix = []
for _ in range(5):
    matrix.append(list(map(int, input().split())))

# 解决问题
result = solve_lights_out(matrix)

# 输出结果
for row in result:
    print(" ".join(map(str, row)))

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241224164813800](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241224164813800.png)



### 08210: 河中跳房子

binary search, greedy, http://cs101.openjudge.cn/practice/08210/

思路：谢谢gpt！又学了一道。

我的思路是先将所有距离排序，再不断删除最小的，但是这样一些边界条件难以处理

于是WA

gpt思路清奇，又给我上了一课



代码：

```python
def can_remove_rocks(rocks, L, M, d):
    """判断是否能通过移除 M 个岩石使最短跳跃距离 >= d"""
    removed = 0
    last_position = 0  # 从起点开始跳跃
    for rock in rocks:
        if rock - last_position < d:
            removed += 1  # 移除当前岩石
            if removed > M:  # 超过可移除的最大数量
                return False
        else:
            last_position = rock  # 更新最后跳跃点
    return True

def max_min_jump(L, N, M, rocks):
    rocks.append(L)  # 终点
    
    # 二分搜索跳跃距离
    low, high = 1, L
    answer = 0
    while low <= high:
        mid = (low + high) // 2
        if can_remove_rocks(rocks, L, M, mid):
            answer = mid  # 当前跳跃距离是可行的，尝试更大的跳跃距离
            low = mid + 1
        else:
            high = mid - 1  # 当前跳跃距离不可行，尝试更小的跳跃距离
    return answer

# 输入部分
L, N, M = map(int, input().split())
rocks = [int(input()) for _ in range(N)]

# 输出结果
print(max_min_jump(L, N, M, rocks))

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241224173534411](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241224173534411.png)



## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>



我宣布，gpt是神，请求考试让它给我开共享文档

