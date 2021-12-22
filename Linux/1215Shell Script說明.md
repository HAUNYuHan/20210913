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
```
# Shell Script
