# Shell 變數:系統變數、使用者變數、環境變數
## Shell 變數
```
● 在Shell中有三種變數：系統變數，環境變數，使用者變數。
● 使用者變數在程式設計過程中使用最多。
● 系統變數在對引數判斷和命令返回值判斷會使用。
● 環境變數主要是在程式執行的時候需要設定。
```
## 系統變數
```
>Shell常用的系統變數:
$n  $1 表示第一個引數，$2 表示第二個引數 … 
$#  命令列引數的個數 
$0  當前程式的名稱 
$?  前一個命令或函式的返回碼 
$*  以″引數1 引數2 … ″ 形式儲存所有引數 
$@  以″引數1″ ″引數2 ″ … 形式儲存所有引數 
$$  本程式的(程序ID號)PID 
$! 最後一個背景工作的PID 

>例子:example.sh
● 其中使用得比較多得是 $n $# $0 $? 
#!/bin/sh
#This file is used to explain the shell system variable.
echo "the number of parameter is $# ";
echo "the return code of last command is $? ";
echo "the script name is $0 ";
echo "the parameters are $* ";
echo "\$1 = $1 ; \$2 = $2 ";

>執行結果：
-bash-2.05b$ ./example1.sh winter stlchina
the number of parameter is 2
the return code of last command is 0
the script name is ./example1.sh
the parameters are winter stlchina
$1 = winter ; $2 = stlchina

>例子:exampl.2e.sh
#!/bin/sh
if [ $# -ne 2 ] ; then
echo "Usage: $0 string file";
exit 1;
fi
grep $1 $2 ;
if [ $? -ne 0 ] ; then
echo "Not Found \"$1\" in $2";
exit 1;
fi
echo "Found \"$1\" in $2";

1.判斷執行引數個數，如果不等於2，顯示使用”用法幫助”, 其中 $0 表示就是指令碼自己。
2.用grep 在$2 檔案中查詢$1 字串。
3.判斷前一個命令執行後的返回值(一般成功都會返回0, 失敗都會返回非0)。
4.如果沒有成功顯示沒找到相關資訊，否則顯示找到了。
5.其中\"表示轉義，在"" 裡面還需要顯示 " 號，則需要加上轉義符\" .

>執行結果:
$ ./example2.sh usage example2.sh
Not Found "usage" in example2.sh

$ ./example2.sh Usage example2.sh     
"Usage: $0 string file";
Found "Usage" in example2.sh
```
## Shell使用者變數
```
● 使用者定義的變數必須由字母數字及底線組成
● 變數名的第一個字元不能為數字
● 與其它UNIX名字一樣,變數名是大小寫敏感的
● 對於使用者變數,使用者可按如下方式賦值:
● name="Winter" 
● 引用變數時，需要在前面加上 $ 號。
  name="Winter"WINTERN=$nameecho "Hello $WINTERN!"
● 輸出結果：
  Hello Winter!
● 注意：變數和「=」之間不要有空格，「=」和賦值也不要有空格，否則shell不會認為變數被定義。

>使用者技巧
● 用變數和其他字元組成新的字
● 需要把變數用{}括起
  SAT=Saturecho Today is ${SAT}day輸出結果是： Today is Saturday
● 為了避免變數名和別的字元產生混淆，最好養成習慣把變數名用{}括起來。

>unset指令
● 對於未賦值的變數, Shell以空值對待。
● 使用者也可以用unset命令清除給變數賦的值。

>#!/bin/sh
echo "a=$a" ;
a=2
echo "a=$a" ;
unset a
echo "a=$a" ;

>結果是:
$ ./test.sh
a=
a=2
a=

>避免程式一不小心對變數進行修改
在shell中，對於使用者變數，可以使用修飾符 “readonly”

>#!/bin/sh
echo "a=$a" ;
#下面增加了readonly
readonly a=2   
echo "a=$a" ;
unset a
echo "a=$a" ;

>結果：
$ ./test.sh
a=
a=2
a=2
```
## shell中的陣列
```
● shell變數中還能設定陣列，但是不同的shell版本有不同陣列賦值方法，而bourne shell 中不支援陣列方式。
● shell有兩種賦值方式，第一種是直接用下標賦值：
name[0]="Tom"
name[1]="Tomy"
name[2]="John"
● 訪問陣列元素的方法使用${name[index]}的方式。
```
## bash中賦值
```
>#!/bin/bash
name=("Tom" "Tomy" "John")
for i in 0 1 2
do echo $i:${name[$i]} ;
done

>結果是：
$ ./test.sh   
0:Tom
1:Tomy
2:John
```
## shell環境變數
```
● shell 環境變數是所有shell 程式都會接受的引數。
● shell程式執行時，都會接收一組變數，這組變數就是環境變數。
```
## 常用的環境變數：

| 名稱 | 描述 |
| --- | --- |
| path |命令搜尋路徑，以冒號為分隔號，注意與DOS下不同是，當前目錄不再系統路徑 |
| home | 使用者home目錄的路徑名，是cd命令的預設引數 |
| columns | 定義了命令編輯模式下可使用命令列的長度 |
| editor | 預設的行編輯器 |
| visual | 預設的可是編輯器 |
| fcedit | 命令fc使用的編輯器 |
| histsize | 命令歷史檔案 |
| histfilesize | 命令歷史檔案中包含最大行數 |
| ifs | 定義shell使用的分隔號 |
| logname | 使用者登入名 |
| mail | 指向一個需要shell監視其修改時間的檔案，當該檔案修改後，shell將發訊息You have mail給使用者 |
| mailcheck | shell檢查mail檔案的週期，單位是秒 |
| mailpath | 功能與mail類似，但可以用一組檔案，以冒號分隔，每個檔案後可跟一個問號和一條發向使用者訊息 |
| shell | shell的路徑名 |
| term | 終端型別 |
| tmout | shell自動退出時間，單位為秒，若設為0則禁止shell自動退出 |
| prompt_command | 指定在主命令提示符前應執行命令 |
| ps1 | 主命令提示符 |
| ps2 | 二級命令提示符，命令執行過程中要求輸入資料時用 |
| ps3 | select的命令提示符 |
| ps4 | 除錯命令提示符 |
| manpath | 尋找手冊業的路徑，以冒號分隔 |
| ld_library_path | 尋找酷的路徑，以冒號分隔 |
# Shell Script
