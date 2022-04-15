# 第一章 快速入門
簡單介紹 C++ 主要的基本元素:
+ 型別(types)
+ 變數(variables)
+ 運算式(statements)
+ 述句(expressions)
+ 函式(function)
## 1.1
主函式 `main()`: 執行 C++ 程式的切入點
最簡單的 main 函式
```cpp
int main() {

  return 0;
}
```
函式定義(function definition)四元素:
+ 回傳型別(return type)
+ 函式名稱(function name)
+ 包在括弧(parentheses)中(可為空)的參數列(parameter)
+ 函式主體(function body):由大括號包住

```cpp
回傳型別 函數名稱(參數列){

  return 0;
}
```
`return`: 終止函數的述句。會回傳一個值(value)給呼叫者(caller)。
分號(semicolon):C++ 大部分述句結尾。

main 函式回傳的值是一個狀態指示器(status indicator)，而回傳 0 代表執行成功。

### 1.1.1編譯&執行程式
終端機(terminal)編譯程式，以 GCC 為例:
```shell
g++ -o prog prog.cpp
```
會編譯出 `prog.exe`。`-o` 為編譯器的一個引數，後面加上執行檔的名稱，若省略則會產生一個名為 `a` 的執行檔案，以 windows 系統來說就是 `a.exe`。

執行檔案:
```shell
./a.exe
```

## 1.2 輸入/輸出
輸入:
```cpp
std::cin >> intput1 >> intput2;
```
輸出:
```cpp
std::cout << output1 << output2 << std::endl;
```
`std::endl`: 清除 buffer 並換行

## 1.3 註解
用 `/*`、`*/` 包可以換行註解，`//` 是單行註解
```cpp
#include <iostream>
/*
 * 簡單的 main 函式
 * 讀取兩數並取總和
 */
int main(){
  // 提示使用者輸入兩個數字
  std::cout << "Enter two numbers:" << std::endl;
  int v1=0,v2=0;  // 存放我們所讀取的輸入的變數
  std::cin >> v1 >>v2;  // 讀取輸入
  std::cout << "The sum of " << v1 <<" and " << v2
            << " is " << v1+v2 << std::endl;
  return 0;
}
```

## 1.4 流程控制
由上而下依序執行。
### while 述句
給的條件為 `true` 就會執行迴圈中的述句。
```cpp
while(條件) {
  述句;
}
```
### for 述句
迴圈執行 10 次:
```cpp
for(int i=0;i<10;i++) {
  述句;
}
```
### 讀取未知數量的輸入
aka EOF(end-of-file)
```cpp
while(cin >> 變數) {
  述句;
}
```

### if 述句
```cpp
if(條件) {
  述句;
} else if(條件) {
  述句;
} else {
  述句;
}
```

## 1.5 類別簡介
Sales_item :
+ 呼叫名為 isbn 函式從物件擷取 ISBN。
+ 用輸入( `<<` )、輸出( `>>` )運算子讀取或寫入物件。
+ 使用指定運算子( `=` )將一物件指定給另一個。
+ 用加法運算子( `+` )相加兩個物件。兩物件需涉及相同 ISBN。結果會是一新的物件，其 ISBN 就是其運算元的，而賣出本數即是其運算元中對應的值總和。
+ 使用複合運算子( `+=` )將一物件加到另一個。

```cpp
#include <iostream>
#include "Sales_item.h"

int main() {
    Sales_item total; // variable to hold data for the next transaction
    // read the first transaction and ensure that there are data to process
    if(std::cin >> total) {
		Sales_item trans; // variable to hold the running sum
        // read and process the remaining transactions
        while (std::cin >> trans) {
			// if we're still processing the same book
            if (total.isbn() == trans.isbn())
                total += trans; // update the running total
            else {              
		        // print results for the previous book
                std::cout << total << std::endl;  
                total = trans;  // total now refers to the next book
            }
		}
        std::cout << total << std::endl; // print the last transaction
    } else {
        // no input! warn the user
        std::cerr << "No data?!" << std::endl;
        return -1;  // indicate failure
    }

    return 0;
}
```
