# 建置py開發環境
## 1.1 建置Anaconda開發環境
### 1.1.1 安裝Anaconda
```
Anaconda 的特色
>內建眾多流行的科學、工程、數據分析的py模組
>完全免費及開源
>支援linux,Windows及Mac平台
>支援py2.x及3.x，且可自由切換
>內建Spyder編輯器
>包含Jupyter Notebook環境
```
### 1.1.2 Anaconda Prompt管理模組

### 啟動Anaconda Prompt
>安裝指令

| 功能 | pip指令 | conda指令 |
| --- | --- | --- |
| 查詢模組列表 | pip list | conda list |
| 更新模組 | pip install -U 模組名稱 | conda update 模組名稱 |
| 安裝模組 | pip install 模組名稱 | conda install 模組名稱 |
| 移除模組 | pip uninstall 模組名稱 | conda remove 模組名稱 |

### 1.1.3 Anaconda Prompt執行py程式檔案
```
python 檔案路徑

>sum.py

a = 12
b = 34
sum = a + b
print("總和 = " + str(sum))

```
## 虛擬環境的模組安裝是各自獨立
### 1.1.4 Anaconda Prompt建立虛擬環境
```
>建立虛擬環境
conda creat -n 虛擬環境名稱 python=版本 anaconda

>切換虛擬環境
activate 虛擬環境名稱

>關閉虛擬環境
conda deactivate

>複製目前環境
conda creat -n 虛擬環境名稱 --clone root

>命令查看目前所有虛擬環境名稱
conda info -e

>移除虛擬環境
conda remove -n 虛擬環境名稱 --all
```
## 1.2 Spyder編輯器
### 1.2.1 啟動Spyder編輯器及檔案管理
### 1.2.2 Spyder簡易智慧輸入
### 1.2.3 程式除錯
## 1.3 Jupyter Notebook編輯器
### 1.3.1 啟動Jupyter Notebook及建立檔案
### 1.3.2 Jupyter Notebook簡易智慧輸入
### 1.3.3 Jupyter Notebook執行程式
### 1.3.4 Jupyter Notebook常用編輯快速鍵
