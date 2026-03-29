# CS50 Week 2: Arrays (陣列) 課程重點整理

影片連結：[https://www.youtube.com/watch?v=h5Gc1n8ZuU8](https://www.youtube.com/watch?v=h5Gc1n8ZuU8)

本週課程探討了 C 語言中的更多基礎組件，並深入了解程式在底層是如何運作的，特別是記憶體與資料儲存的方式。

## 1. 編譯 (Compiling)
在之前的課程中，我們學到原始碼 (Source Code) 必須轉換成機器碼 (Machine Code) 才能被電腦執行，這個過程稱為**編譯 (Compiling)**。
- 當我們執行 `make [程式名稱]` 時，實際上在背後呼叫了 `clang` (C language compiler) 這樣一個編譯器程式。
- **編譯的四個步驟：**
  1. **預處理 (Preprocessing)**：處理以 `#` 開頭的指令（如 `#include <stdio.h>`），將函式庫的標頭檔的內容直接貼入程式碼中。
  2. **編譯 (Compiling)**：將 C 語言程式碼轉換為組合語言 (Assembly Code)。
  3. **組譯 (Assembling)**：將組合語言轉換成機器碼 (由 0 和 1 組成的二進位檔)。
  4. **連結 (Linking)**：將所有編譯好的機器碼（包含你自己寫的，以及函式庫的如 `stdio.h` 與 `cs50.h`）合併成最終的單一可執行檔。

---

## 2. 除錯 (Debugging)
寫程式一定會遇到 Bug。學習如何找出錯誤並修正，是程式設計師的必修課。
- **printf 除錯法**：在程式的各個地方加上 `printf` 觀察變數的狀態。例如，在迴圈中印出計數器 `i` 的值，來看迴圈究竟跑了幾次。
  ```c
  #include <stdio.h>

  int main(void)
  {
      for (int i = 0; i <= 3; i++) // 故意寫錯的 <= 3
      {
          printf("i is %i\n", i); // 透過 printf 觀察 i 的變化來找出邏輯錯誤
          printf("#\n");
      }
  }
  ```
- **除錯工具 (Debugger)**：使用 VS Code 內建的除錯工具，可以設定**中斷點 (Breakpoints)**，讓程式執行到該行時停下來，並允許我們一步一步 (Step Over, Step Into) 檢視記憶體中變數的變化。
- **duck debugging (小黃鴨除錯法)**：對著一小黃鴨 (或任何無生命的物品) 逐行解釋你的程式碼，這個過程往往能幫你發現哪裡邏輯不通。

---

## 3. 記憶體與資料型態 (Memory & Data Types)
電腦的記憶體資源是有限的。不同的資料型態在記憶體中佔用的空間不同：
- `bool`：1 byte
- `char`：1 byte
- `int`：4 bytes
- `float`：4 bytes
- `long`：8 bytes
- `double`：8 bytes

這意味著每宣告一個整數 (int)，就會佔用記憶體中 4 個連續位元組（32 個位元）來儲存資料。

---

## 4. 陣列 (Arrays)
當我們需要儲存很多相同型態的資料時（例如考試成績），如果宣告 `score1`, `score2`, `score3` 會非常缺乏彈性。
**陣列 (Arrays)** 是一種將相同資料型態的變數「背靠背」(連續) 儲存在記憶體中的資料結構。

- **靜態分數計算範例 vs 動態陣列分數計算範例**：
  不再宣告三個獨立的整數變數，我們宣告一個長度為 3 的陣列。
  ```c
  #include <stdio.h>

  int main(void)
  {
      int scores[3]; // 宣告一個名為 scores 的陣列，可容納 3 個整數
      scores[0] = 72; // 陣列的索引 (index) 從 0 開始
      scores[1] = 73;
      scores[2] = 33;

      printf("Average: %f\n", (scores[0] + scores[1] + scores[2]) / 3.0);
  }
  ```

---

## 5. 字串 (Strings) 揭密
回顧 Week 0，字串 (`string`) 其實不是 C 語言原本就有的基本資料型態，它是由 `cs50.h` 提供的。在底層，**字串就是一個字元陣列 (Array of characters)**。
- 字串中的每一個字元佔用 1 個位元組，整個字串在記憶體中也是連續儲存。
- 如何讓電腦知道字串在哪裡結束？C 語言使用一個特殊的字元 `\0`（也稱為 **NUL 字元**），ASCII 數值為 0。當電腦在記憶體中讀取字串時，讀到 `\0` 就知道字串結束了。
  
  例如字串 `"HI!"` 在記憶體中實際上佔滿 4 bytes：`'H'`, `'I'`, `'!'`, `'\0'`。

- **印出字元記憶體中的 ASCII 碼範例**：
  ```c
  #include <stdio.h>

  int main(void)
  {
      char c1 = 'H';
      char c2 = 'I';
      char c3 = '!';
      
      // %c 印出文字，%i 印出其整數 ASCII 值
      printf("%i %i %i\n", c1, c2, c3); // 結果為：72 73 33
  }
  ```

---

## 6. 指令列引數 (Command-Line Arguments)
除了在執行程式時讓使用者輸入資料外，我們也可以在程式一開始執行時「就直接傳入參數」，這稱作**指令列引數**。

- `int main(int argc, string argv[])` 就是用來在 C 語言中接收指令列參數的：
  - `argc`：代表參數的數量 (Argument Count)。至少為 1 (一定內含程式執行的名稱本身)。
  - `argv`：代表參數值的字串陣列 (Argument Vector)，儲存每個輸入的文字。
- **範例**：
  ```c
  #include <cs50.h>
  #include <stdio.h>

  int main(int argc, string argv[])
  {
      // 假設執行時輸入 ./greet David
      if (argc == 2)
      {
          printf("hello, %s\n", argv[1]); // argv[1] 為第一個被傳遞的參數 ("David")
      }
      else
      {
          printf("hello, world\n");
      }
  }
  ```

---

## 7. 離開狀態 (Exit Status)
當一個程式順利結束時，預設電腦會收到一個特殊的離開狀態碼 `0`。如果程式因為某種錯誤提前中斷，我們可以主動回傳非 `0` 的數字（通常是 `1`）用來表示出現了錯誤。
  ```c
  #include <cs50.h>
  #include <stdio.h>

  int main(int argc, string argv[])
  {
      if (argc != 2)
      {
          printf("Missing command-line argument\n");
          return 1; // 回傳 1 表示錯誤並強制結束程式
      }
      printf("hello, %s\n", argv[1]);
      return 0; // 回傳 0 表示程式順利執行結束
  }
  ```

---

## 8. 密碼學初探 (Cryptography)
課程最後介紹了如何應用前面學到的知識來進行簡單的文字加密與解密。
- **加密模型**：`明文 (Plaintext)` 加上一個 `金鑰 (Key)`，透過 `密碼演算法 (Cipher)` 計算後，轉變成我們看不懂的 `密文 (Ciphertext)`。
- 我們可以將字串中的字元當作整數 (剛剛學到的 ASCII 計算方式)，透過簡單的數學運算 (例如將字母整體位移一個數字) 就能把可讀文字轉換成亂碼字元。這不僅是 C 語言陣列與字元的綜合應用，也是本週作業的核心概念。
