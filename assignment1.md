**\# Assignment #1: 自主学习**
**Updated 0110 GMT+8 Sep 10, 2024**
**2024 fall, Complied by ==付麟瑞 数院==**

## 1. 题目



### 02733: 判断闰年



http://cs101.openjudge.cn/practice/02733/

思路：

##### 代码



```
# a=int(input())
if a % 4==0 :
    if a % 100==0:
        if a %400==0 :
            if a % 3200==0  :
                print('N')
            else:
                print('Y')
        else:
            print("N")
    else:
        print('Y')
else :
    print('N')
```



代码运行截图 ==（至少包含有"Accepted"）==

![](d:\Users\m1885\Pictures\Screenshots\屏幕截图 2024-09-19 225414.png)

### 02750: 鸡兔同笼



http://cs101.openjudge.cn/practice/02750/

思路：

##### 代码



```
# a=int(input())
if a%2==0:
    max=a//2
    if a%4==0:
        min=a//4
    else:
        min=a//4+1
else:
    print('0 0')
    exit()
print(min,max)

```



代码运行截图 ==（至少包含有"Accepted"）==

![image-20240919225741478](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20240919225741478.png)

### 50A. Domino piling



greedy, math, 800, http://codeforces.com/problemset/problem/50/A

思路：

##### 代码



```
# m,n = map(int,input().split())
print(m*n//2)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240919230121020](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20240919230121020.png)

### 1A. Theatre Square



math, 1000, https://codeforces.com/problemset/problem/1/A

思路：

##### 代码



```
# [n,m,a]=[int(i) for i in input().split()]
print(-n//a*(-m//a))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==、

![image-20240919230335886](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20240919230335886.png)

### 112A. Petya and Strings



implementation, strings, 1000, http://codeforces.com/problemset/problem/112/A

思路：

##### 代码



```
# a=input().lower()
b=input().lower()
if a<b:
    print(-1)
elif a>b:
    print(1)
else:
    print(0)    
    
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240919230806734](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20240919230806734.png)

### 231A. Team



bruteforce, greedy, 800, http://codeforces.com/problemset/problem/231/A

思路：

##### 代码



```
# n=int(input())
count=0
for i in range(n):
    a,b,c=map(int,input().split())
    if a and b or a and c or b and c:
        count+=1
print(count)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![image-20240919231202603](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20240919231202603.png)

## 2. 学习总结和收获

通过这一周的学习，我学会了使用chatgpt获取一些简单操作的实现方法、检查代码错误，熟悉了一些简单函数的应用，并且学会了使用AI等工具提升工作效率。