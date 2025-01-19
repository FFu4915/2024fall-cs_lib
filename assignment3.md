# Assign #3: Oct Mock Exam暨选做题目满百

Updated 1537 GMT+8 Oct 10, 2024

2024 fall, Complied by Hongfei Yan==数院付麟瑞 AC5==



**说明：**

1）Oct⽉考： AC6==（请改为同学的通过数）== 。考试题⽬都在“题库（包括计概、数算题目）”⾥⾯，按照数字题号能找到，可以重新提交。作业中提交⾃⼰最满意版本的代码和截图。

2）请把每个题目解题思路（可选），源码Python, 或者C++/C（已经在Codeforces/Openjudge上AC），截图（包含Accepted, 学号），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、作业评论有md或者doc。

4）如果不能在截止前提交作业，请写明原因。



## 1. 题目

### E28674:《黑神话：悟空》之加密

http://cs101.openjudge.cn/practice/28674/



思路：



代码

```python

capital_letters = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
alphabets = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l','m', 'n', 'o', 'p', 'q', 'r','s', 't', 'u', 'v', 'w', 'x', 'y', 'z']
k=int(input())
str=''
a=input()
for i in a:
    try:
        str+=alphabets[(alphabets.index(i)-k)%26]
    except:
        str+=capital_letters[(capital_letters.index(i)-k)%26]
print(str)
```



代码运行截图 ==![image-20241012200833880](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241012200833880.png)==





### E28691: 字符串中的整数求和

http://cs101.openjudge.cn/practice/28691/



思路：



代码

```python

str1,str2=input().split()
str1=int(str1[0:2])
str2=int(str2[0:2])
print(str1+str2)
```



代码运行截图 ==![image-20241012200922873](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241012200922873.png)==





### M28664: 验证身份证号

http://cs101.openjudge.cn/practice/28664/



思路：



代码

```python

lst=[7,9,10,5,8,4,2,1,6,3,7,9,10,5,8,4,2]
m=int(input())
for j in range(m):
    n=input()
    k=0
    for i in range(0,17):
        k+=lst[i]*int(n[i])
    k=k%11
    lst2=[1,0,'X',9,8,7,6,5,4,3,2]
    a=str(lst2[k])
    if a == n[17]:
        print('YES')
    else:
        print('NO')
```



代码运行截图 ==![image-20241012200950932](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241012200950932.png)==





### M28678: 角谷猜想

http://cs101.openjudge.cn/practice/28678/



思路：



代码

```python

def func(a):
    if a == 1:
        print('End')
        exit()
    if a % 2 == 0:
        print(f'{a}/2={a//2}')
        func(a//2)
    else:
        print(f'{a}*3+1={a*3+1}')
        func(a*3+1)
func(int(input()))
```



代码运行截图 ==![image-20241012201033706](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241012201033706.png)==





### M28700: 罗马数字与整数的转换

http://cs101.openjudge.cn/practice/28700/



思路：



##### 代码

```python
# 
n=input()
qian=['','M','MM','MMM']
bai=['','C','CC','CCC','CD','D','DC','DCC','DCCC','CM']
shi=['','X','XX','XXX','XL','L','LX','LXX','LXXX','XC']
ge=['','I','II','III','IV','V','VI','VII','VIII','IX']
str=''
sum=0
try:
    n=int(n)
    a=n//1000
    str+=qian[a]
    b=(n%1000)//100
    str+=bai[b]
    c=(n%100)//10
    str+=shi[c]
    d=n%10
    str+=ge[d]
    print(str)
except:
    lst1=[1,5,10,50,100,500,1000]
    lst2=['I','V','X','L','C','D','M']
    lst=[]
    for i in n:
        lst.append(lst1[lst2.index(i)])
    lst.append(0)
    for j in range(len(lst)-1):
        if lst[j]<lst[j+1]:
            sum-=lst[j]
        else:
            sum+=lst[j]
    print(sum)
```



代码运行截图 ==![image-20241012201110110](C:\Users\m1885\AppData\Roaming\Typora\typora-user-images\image-20241012201110110.png)==





### *T25353: 排队 （选做）

http://cs101.openjudge.cn/practice/25353/



思路：



代码

```python


```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





## 2. 学习总结和收获

==这次的考试让我收获很多。周四下午因为我睡过头了没去机房，四点二十才开始做。电脑上pycharm里的AI插件帮我简化了很多工作，使我能够较快的使用枚举方法（1，5题）因为时间紧迫，我在读题不仔细这方面的毛病愈发凸显，荣获全场罚时最高（悲）。其实跑一遍报错以后再查倒不如提前仔细想想，着急也不会快很多。至于第六题，看到解析以后才明白。设计与优化算法解决复杂问题，并不是一开始就能把一个复杂的大问题解决，总是要从简单的小问题入手，从样本量较小的例子中总结归纳出一种规律再形成算法。而且，一些模型是需要积累的（例如线段树），这些方法可以帮我们达到想要的目的，缩短时间==











