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
## 使用者變數
```

```
# Shell Script
