# CS50 Week 1 影片內容整理與摘要 - C 語言基礎

### 1. C 語言簡介與語法規範
*   **進入文字代碼時代**：比起 Week 0 的 Scratch 積木，C 是一種更底層、需要手寫程式碼的語言。
*   **標準樣板**：每個 C 程式幾乎都以 `#include <stdio.h>` 開頭，這是在引進標準輸入輸出函式庫。主程式則放在 `int main(void) { ... }` 裡面。
*   **嚴謹語法**：
    *   每條指令結尾必須加上分號 `;`。
    *   字串必須用雙引號 `"` 包圍。

### 2. 編譯與執行 (Compilation)
*   **原始碼與機器碼**：電腦不懂我們寫的 C 代碼 (Source Code)，需要透過**編譯器 (Compiler)** 將其轉換為電腦看得懂的「0 與 1」(Machine Code)。
*   **編譯工具**：
    *   使用 `clang` 進行編譯。
    *   **make**：CS50 提供的一個簡化指令。輸入 `make hello`，系統會自動幫你執行複雜的編譯指令。
*   **執行程式**：編譯完成後，輸入 `./hello` 即可執行產生的二進位檔。

### 3. 資料型別與變數 (Data Types & Variables)
*   **常用型別**：
    *   `int`：整數 (Integer)。
    *   `long` : 位元數更多的整數 (儲存更大的數字)。
    *   `char`：單一字元 (例如 'A')。
    *   `float` / `double`：浮點數 (帶有小數點的數字)。
    *   `string`：字串 (需引進 `<cs50.h>` 才有)。
    *   `bool`：布林值 (`true` 或 `false`)。
*   **格式化輸出 (Format Specifiers)**：在 `printf` 中使用佔位符來顯示變數值：
    *   `%i` 代表整數，`%s` 代表字串，`%f` 代表浮點數，`%li` 代表長整數。

### 4. 條件判斷與迴圈 (Conditionals & Loops)
*   **條件式**：`if`、`else if`、`else`。邏輯運算子包含 `&&` (且)、`||` (或)、`!` (非)。
*   **迴圈**：
    *   `while (condition) { ... }`：只要條件成立就重複。
    *   `for (int i = 0; i < n; i++) { ... }`：精確控制次數的計數型迴圈。
    *   `do { ... } while (condition)`：保證內容至少執行一次。

### 5. CS50 函式庫與輸入
為了降低初學者學習門檻，哈佛團隊開發了 `<cs50.h>`，提供了方便獲取使用者輸入的函式：
*   `get_string("Name: ")`
*   `get_int("Number: ")`
*   `get_float("Price: ")`

### 6. 課堂重點實作範例
*   **hello.c**：印出 "hello, world" 或使用者名字的初階程式。
*   **meow.c**：展示如何用迴圈讓電腦印出多次 "meow"，並將其封裝成自定義函式 (Function)。
*   **mario.c**：練習巢狀迴圈 (Nested Loops)，在螢幕上印出像瑪利歐遊戲中的磚塊矩陣。
*   **calculator.c**：基本的算術運算與資料溢位 (Overflow) / 精準度 (Precision) 的概念初步探討。

### 7. 抽象化 (Abstraction)
*   將複雜的邏輯包裝成一個簡單的函式名稱 (例如 `meow()`)，讓主程式碼更簡潔易讀。注意在 C 語言中，自定義函式若放在 `main` 之後，必須在程式頂部先寫下**函式原型 (Prototype)**。
