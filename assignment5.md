# Assignment #5: Greedy穷举Implementation

Updated 1939 GMT+8 Oct 21, 2024

2024 fall, Complied by <mark>同学的姓名、院系</mark>



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### 04148: 生理周期

brute force, http://cs101.openjudge.cn/practice/04148

思路：



代码：

```python
number=0
while 1:
    number+=1
    x,y,z,d=map(int,input().split())
    if (x,y,z,d)==(-1,-1,-1,-1):
        exit()
    i=0
    found=0
    while not found:
        if (23*i+x-y)%28==0:
            if (23*i+x-z)%33==0:
                if d>=23*i+x:
                    ans=23*i+x+23*28*33-d
                    found=1
                else:
                    ans=23*i+x-d
                    found=1
        i+=1
    print(f'Case {number}: the next triple peak occurs in {ans} days.')
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>![image-20241028225403095](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241028225403095.png)





### 18211: 军备竞赛

greedy, two pointers, http://cs101.openjudge.cn/practice/18211

思路：



代码：

```python
money=int(input())
lst=list(map(int,input().split()))
lst.sort()
i=0
j=0
ans=0
max_ans=0
while i+j<len(lst):
    if money>=lst[i]:
        money-=lst[i]
        i+=1
        ans+=1
        max_ans=max(max_ans,ans)
        continue
    if ans>0:
        j+=1
        ans-=1
        money+=lst[-j]
        continue
    break
print(max_ans)
```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20241028225442731](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241028225442731.png)



### 21554: 排队做实验

greedy, http://cs101.openjudge.cn/practice/21554

思路：



代码：

```python
n=int(input())
a=list(map(int,input().split()))
b=[]
for i in range(n):
    b.append((a[i],i+1))
b.sort(key=lambda x:x[0])
c=[]
waitingtime=0
for j in range(n):
    waitingtime+=(n-1-j)*b[j][0]
    c.append(str(b[j][1]))
print(' '.join(c))
print(f"{waitingtime/n:.2f}")

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241028231058435](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241028231058435.png)



### 01008: Maya Calendar

implementation, http://cs101.openjudge.cn/practice/01008/

思路：



代码：

```python
months = ['pop', 'no', 'zip', 'zotz', 'tzec', 'xul', 'yoxkin', 'mol', 'chen', 'yax', 'zac',
          'ceh', 'mac', 'kankin', 'muan', 'pax', 'koyab', 'cumhu', 'uayet']
weeks = ['imix', 'ik', 'akbal', 'kan', 'chicchan', 'cimi', 'manik', 'lamat', 'muluk', 'ok',
         'chuen', 'eb', 'ben', 'ix', 'mem', 'cib', 'caban', 'eznab', 'canac', 'ahau']
n = int(input())
print(n)
for _ in range(n):
    tmp = input().split()
    day, month, year = tmp[0][:-1], tmp[1], tmp[2]
    d = int(day)+1+months.index(month)*20+365*int(year)
    nd, y = d % 260, d // 260
    x, m = nd % 13, nd % 20
    if x == 0:
        x = 13
        if m == 0:
            y -= 1
    print(x, weeks[m-1], y)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241028233737197](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241028233737197.png)





### 545C. Woodcutters

dp, greedy, 1500, https://codeforces.com/problemset/problem/545/C

思路：



代码：

```python
n=int(input())
x=[]
h=[]
for _ in range(n):
    _x,_y=map(int,input().split())
    x.append(_x)
    h.append(_y)
if n<=2:
    print(n)
else:
    num=2
    q=x[0]
    for i in range(1,n-1):
        if x[i]-q>h[i]:
            num+=1
            q=x[i]
            continue
        elif x[i+1]-x[i]>h[i]:
            num += 1
            q=x[i]+h[i]
            continue
        q=x[i]
    print(num)
```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>

![image-20241028231245368](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241028231245368.png)



### 01328: Radar Installation

greedy, http://cs101.openjudge.cn/practice/01328/

思路：

思路是对于每个点找数轴上需要雷达的线段打标签，然后按照标签数量从大到小排序放雷达，并删去对应点所打的标签，然而这是一个无论从想法上还是执行上都非常困难的思路，甚至存在反例。所以我在写了一个多小时然后一直不知道为什么报错WA之后放弃了。

但是不亏，起码又跟chatgpt学了点代码，又知道了一些报错原因

代码：

```python

```



代码运行截图 <mark>（至少包含有"Accepted"）</mark>





## 2. 学习总结和收获

<mark>如果作业题目简单，有否额外练习题目，比如：OJ“计概2024fall每日选做”、CF、LeetCode、洛谷等网站题目。</mark>

唉有的时候自己就是想不出来，思路好的时候一下就秒，没感觉就卡死了



