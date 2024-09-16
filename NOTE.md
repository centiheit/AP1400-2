## 1

docker build -t ap1400-2:hw1 .
docker run -p 8080:8080 -d ap1400-2:hw1

## 2


这两个函数的主要区别在于随机数生成器和分布对象的生命周期和状态管理。

### 第一种实现
```cpp
size_t Client::generate_nonce() {
    static std::default_random_engine e;
    static std::uniform_int_distribution<int> u(0, INT_MAX);
    return u(e);
}
```

#### 特点：
1. **静态变量**：[`e`](command:_github.copilot.openSymbolFromReferences?%5B%22e%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Csrc%5C%5Cclient.cpp%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A36%2C%22character%22%3A38%7D%7D%5D%5D "Go to definition") 和 [`u`](command:_github.copilot.openSymbolFromReferences?%5B%22u%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Csrc%5C%5Cclient.cpp%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A37%2C%22character%22%3A46%7D%7D%5D%5D "Go to definition") 是静态变量，这意味着它们在第一次调用时初始化，并在整个程序的生命周期内保持其状态。
2. **状态保持**：由于 [`e`](command:_github.copilot.openSymbolFromReferences?%5B%22e%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Csrc%5C%5Cclient.cpp%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A36%2C%22character%22%3A38%7D%7D%5D%5D "Go to definition") 和 [`u`](command:_github.copilot.openSymbolFromReferences?%5B%22u%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Csrc%5C%5Cclient.cpp%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A37%2C%22character%22%3A46%7D%7D%5D%5D "Go to definition") 是静态的，每次调用 [`generate_nonce`](command:_github.copilot.openSymbolFromReferences?%5B%22generate_nonce%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Csrc%5C%5Cclient.cpp%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A35%2C%22character%22%3A15%7D%7D%5D%5D "Go to definition") 时，随机数生成器的状态都会延续上一次调用的状态。这意味着生成的随机数序列是连续的，不会重复。

### 第二种实现
```cpp
size_t Client::generate_nonce() {
    std::default_random_engine e;
    std::uniform_int_distribution<int> u(0, INT_MAX);
    return u(e);
}
```

#### 特点：
1. **局部变量**：[`e`](command:_github.copilot.openSymbolFromReferences?%5B%22e%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Csrc%5C%5Cclient.cpp%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A36%2C%22character%22%3A38%7D%7D%5D%5D "Go to definition") 和 [`u`](command:_github.copilot.openSymbolFromReferences?%5B%22u%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Csrc%5C%5Cclient.cpp%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A37%2C%22character%22%3A46%7D%7D%5D%5D "Go to definition") 是局部变量，每次调用 [`generate_nonce`](command:_github.copilot.openSymbolFromReferences?%5B%22generate_nonce%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Csrc%5C%5Cclient.cpp%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A35%2C%22character%22%3A15%7D%7D%5D%5D "Go to definition") 时都会重新创建和初始化。
2. **状态重置**：由于 [`e`](command:_github.copilot.openSymbolFromReferences?%5B%22e%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Csrc%5C%5Cclient.cpp%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A36%2C%22character%22%3A38%7D%7D%5D%5D "Go to definition") 和 [`u`](command:_github.copilot.openSymbolFromReferences?%5B%22u%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Csrc%5C%5Cclient.cpp%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A37%2C%22character%22%3A46%7D%7D%5D%5D "Go to definition") 是局部的，每次调用 [`generate_nonce`](command:_github.copilot.openSymbolFromReferences?%5B%22generate_nonce%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Csrc%5C%5Cclient.cpp%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2FAP1400-2%2FAP1400-2-HW2%2Fsrc%2Fclient.cpp%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A35%2C%22character%22%3A15%7D%7D%5D%5D "Go to definition") 时，随机数生成器的状态都会重置。这意味着每次调用都会生成相同的随机数序列，除非随机数生成器的种子发生变化。

### 总结
- **第一种实现**适用于需要生成连续且不重复的随机数序列的情况，因为静态变量保持了随机数生成器的状态。
- **第二种实现**适用于每次调用都需要独立的随机数生成的情况，但需要注意的是，如果不改变种子，每次调用生成的随机数序列可能是相同的。

通常情况下，为了确保随机数的质量和避免重复，推荐使用第一种实现。

## 3


在 C++ 中，`extern` 关键字用于声明一个变量或函数在其他文件中定义。它告诉编译器该变量或函数的定义在另一个翻译单元中，并且在当前文件中只进行声明而不进行定义。

### 作用

- **声明而不定义**：`extern` 关键字用于声明一个变量或函数，而不分配内存或生成代码。实际的定义和内存分配在另一个文件中进行。
- **跨文件访问**：允许在多个文件之间共享变量或函数。

### 示例

假设有两个文件：[`server.h`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "d:\PHD\CIM-SIM\cppLearning\ref\AP1400-2\AP1400-2-HW2\include\server.h") 和 `server.cpp`。

#### [`server.h`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "d:\PHD\CIM-SIM\cppLearning\ref\AP1400-2\AP1400-2-HW2\include\server.h")
```cpp
// 声明一个外部变量
extern std::vector<std::string> pending_trxs;
```

#### `server.cpp`
```cpp
#include "server.h"

// 定义外部变量
std::vector<std::string> pending_trxs;

int main() {
    // 使用外部变量
    pending_trxs.push_back("Transaction 1");
    pending_trxs.push_back("Transaction 2");

    for (const auto &trx : pending_trxs) {
        std::cout << trx << std::endl;
    }

    return 0;
}
```

### 解释

1. **声明**：
   - 在 [`server.h`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "d:\PHD\CIM-SIM\cppLearning\ref\AP1400-2\AP1400-2-HW2\include\server.h") 文件中，`extern std::vector<std::string> pending_trxs;` 声明了一个外部变量 [`pending_trxs`](command:_github.copilot.openSymbolFromReferences?%5B%22pending_trxs%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5Cref%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Cinclude%5C%5Cserver.h%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A12%2C%22character%22%3A32%7D%7D%5D%5D "Go to definition")，但没有分配内存或初始化。
   - 这告诉编译器 [`pending_trxs`](command:_github.copilot.openSymbolFromReferences?%5B%22pending_trxs%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5Cref%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Cinclude%5C%5Cserver.h%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A12%2C%22character%22%3A32%7D%7D%5D%5D "Go to definition") 在其他地方定义。

2. **定义**：
   - 在 `server.cpp` 文件中，`std::vector<std::string> pending_trxs;` 定义了 [`pending_trxs`](command:_github.copilot.openSymbolFromReferences?%5B%22pending_trxs%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5Cref%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Cinclude%5C%5Cserver.h%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A12%2C%22character%22%3A32%7D%7D%5D%5D "Go to definition") 并分配内存。
   - 这使得 [`pending_trxs`](command:_github.copilot.openSymbolFromReferences?%5B%22pending_trxs%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5Cref%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Cinclude%5C%5Cserver.h%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A12%2C%22character%22%3A32%7D%7D%5D%5D "Go to definition") 在整个程序的生命周期内都可以访问。

3. **使用**：
   - 在 `main` 函数中，可以使用 [`pending_trxs`](command:_github.copilot.openSymbolFromReferences?%5B%22pending_trxs%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22d%3A%5C%5CPHD%5C%5CCIM-SIM%5C%5CcppLearning%5C%5Cref%5C%5CAP1400-2%5C%5CAP1400-2-HW2%5C%5Cinclude%5C%5Cserver.h%22%2C%22_sep%22%3A1%2C%22external%22%3A%22file%3A%2F%2F%2Fd%253A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22path%22%3A%22%2Fd%3A%2FPHD%2FCIM-SIM%2FcppLearning%2Fref%2FAP1400-2%2FAP1400-2-HW2%2Finclude%2Fserver.h%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A12%2C%22character%22%3A32%7D%7D%5D%5D "Go to definition")，因为它在 `server.cpp` 中已经定义并分配了内存。

### 总结

`extern` 关键字用于在一个文件中声明一个变量或函数，而实际的定义在另一个文件中。这种机制允许在多个文件之间共享变量或函数，从而实现模块化编程。