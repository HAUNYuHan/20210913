# 3.1迴圈與串列
## 3.1.1 串列(list)
```
>串列名稱 = [元素1,元素2, ...]

list1 = [1, 2, 3, 4, 5] # 元素皆為整數
list2 = ["香蕉", "蘋果", "橘子"] # 元素皆為字串
list3 = [1, "香蕉",True] #包含不同資料型態元素

list4 = ["香蕉", "蘋果", "橘子"]
print(list4[1]) # 蘋果
print(list4[3]) # 錯誤,索引值超過範圍

print(list4[-1]) # 橘子
print(list4[-4]) # 錯誤,索引值超過範圍

list5= [["joe", "1234"], ["mary", "abcd"], ["david","5678"]]
print(list5[1]) # ["mary", "abcd"], 元素為串列
print(list5[1][1]) # abcd
```
### list1.py
```
score = [85, 79, 93]
print("國文成績 : %d 分" % score[0])
print("數學成績 : %d 分" % score[1])
print("英文成績 : %d 分" % score[2])
```
## 3.1.2 rang函式
```
>串列變數 = range(整數值)

r1 = range(5)
print(list(r1)) #[0,1,2,3,4]

>串列變數 = range(起始值, 終止值)

r2 = range(3, 8) #list(r2)=[3,4,5,6,7]
r3 = range(-6, -2) #list(r3)=[-6,-5,-4,-3]

>串列變數 = range(起始值, 終止值, 間隔值)

r4 = range(3, 8, 1) #list(r4)=[3,4,5,6,7]
r5 = range(3, 8, 2) #list(r5)=[3,5,7] , 元素值每次增加2

r6 = range(8, 3, -1) #list(r6)=[8,7,6,5,4]
```
## 3.1.3 for迴圈
```
>for 變數 in 串列:
    程式區塊
    
list1 = ["香蕉", "蘋果", "橘子"]
for s in list1:         #執行結果為:香蕉, 蘋果, 橘子        
    print(s, end=",")
    
for i in range(1,31):
    列印程式碼
```
### numtotal.py
```
sum = 0
n = int(input("請輸入正整數："))
for i in range(1, n+1):
    sum += i
print("1 到 %d 的整數和為 %d" % (n, sum))
```
## 3.1.4 巢狀for迴圈
```
>使用巢狀for迴圈時須特別注意執行次數問題，其執行次數是各層迴圈的乘積，
若執行次數太多會耗費相當長時間，可能讓使用者以為電腦當機，例如:
n = 0
for i in range (1,10001):
    for j in range (1,10001):
        n += 1
print(n)
外層迴圈及內層迴圈都是一萬次，則「n+=1」會執行一億次(10000*10000)，
執行時間視CPU速度約需十餘秒到數十秒
```
### ninenine.py
```
for i in range(1,10):
    for j in range(1,10):
        product = i * j
        print("%d*%d=%-2d   " % (i, j, product), end="")    /*列印乘法算式:格式「-2d」表示列印佔2個字元的整數，並靠左對齊；「end=""」表示不換行，在同一列列印*/
    print()
```
## 3.1.5break及coutinue
```
迴圈執行時，如果要中途結束執行，可使用break命令強制離開迴圈，

## 3.1.6
## 3.1.7
# 3.2進階串列與元組
## 3.2.1
## 3.2.2
