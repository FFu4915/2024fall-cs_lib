Ascii表 chr(0),ord('A')

<img src="[d:\Users\m1885\Pictures\Screenshots\屏幕截图 2024-10-20 154950.png](https://github.com/FFu4915/2024fall-cs_lib/blob/cheetsheet/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-10-20%20154950.png)" alt="屏幕截图 2024-10-20 154950" style="zoom:75%;" />

![屏幕截图 2024-10-20 155002](d:\Users\m1885\Pictures\Screenshots\屏幕截图 2024-10-20 155002.png)

dijiaslkdj



    import heapq
    
    def dijkstra(s,mat,e):#s,e分别是起点和终点.起点s=(0,x0,y0),终点e=(xe,ye).
        MAXN=float('inf')
        weight=[[MAXN]*len(mat[0]) for _ in range(len(mat))]
        q=[s]
        weight[s[1]][s[2]]=0
        d=[(-1,0),(1,0),(0,-1),(0,1)]
    #开始bfs
    while q:
        w,x,y=heapq.heappop(q)
      
        #先处理到终点的情况
        if (x,y)==e:
            return weight[x][y]
      
        #然后探路
        for dx,dy in d:
            nx,ny=x+dx,y+dy
            if 0<=nx<len(mat) and 0<=ny<len(mat[0]):#不用not in visited
                new_w=weight[x][y]+______#这段填上点(x,y)到(nx,ny)的权重
                if new_w<weight[nx][ny]:
                    weight[nx][ny]=new_w
                    heapq.heappush(q,(new_w,nx,ny))
    
    return -1

欧拉筛



```
def euler(n):
    origen=set(range(2,n+1))
    primes=[]
    not_primes=[1]*(n+2)
    for i in origen:
        if not_primes[i]:
            primes.append(i)
        for j in primes:
            if i*j > n+1:
                break
            not_primes[i*j]=0
            if i%j==0:
                break
    return not_primes

not_primes=euler(1000000)
```


深拷贝

  from copy import deepcopy
a=[1,2,3]
b=a[:]
c=[[1,2],[2,3],[3,4]]
d=c[:]
e=deepcopy(c)

dfs

```
def dfs(x,y):
    d=[(-1,-1),(-1,0),(-1,1),(0,-1),(0,1),(1,-1),(1,0),(1,1)]
    for dx,dy in d:
        nx,ny=x+dx,y+dy
        if 0<=nx<len(mat) and 0<=ny<len(mat[0]):
            if mat[nx][ny]==1:
                mat[x][y]=0
                dfs(nx,ny)
                mat[x][y]=1
```



bfs

```
from collections import deque
def bfs(x0,y0,mat):
    q=deque([(x0,y0)])
    d=[(-1,0),(1,0),(0,1),(0,-1)]
    v=set()
    while q:#确定当前位置
        x,y=q.popleft()
        v.add((x,y))
        for dx,dy in d:#从当前位置开始探路
            nx,ny=x+dx,y+dy
            if 0<=nx<len(mat) and 0<=ny<len(mat[0]) and mat[nx][ny]==1:
                q.append((nx,ny))
```





二分

```
lo,hi=0,len(a)
while lo < hi:
	mid = (lo + hi) // 2
    if a[mid] < x:
        lo = mid + 1
    else:
        hi = mid
```



保留小数
"{:.2f}".format(number)






mergesort



```
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    # 分割
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])

    # 合并
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0

    # 合并两个有序数组
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    # 剩余元素
    result.extend(left[i:])
    result.extend(right[j:])
    return result

# 示例用法
data = [4, 2, 7, 1, 3]
sorted_data = merge_sort(data)
print("归并排序结果：", sorted_data)

```

