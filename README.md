# BankSystem

A C++ object-oriented model of bank accounts with Normal and VIP tiers, credit borrowing and interest on overdue debt.

## Overview

BankSystem models a simple retail bank account in C++. A base `Account` class holds the shared behaviour (deposits, withdrawals, credit borrowing, repayment, debt status), and two derived classes, `Normal` and `Vip`, set the credit limit and repayment period for each account tier. A Qt Widgets main window exists as a starting point for a graphical front end, but it is currently an empty shell; the working part of the project is the console demo in `main.cpp`.

## Key features

- Account class hierarchy: `Account` (base), `Normal` and `Vip` (derived).
- Automatic account IDs, assigned from a static counter.
- Deposit and withdrawal with basic input checks.
- Credit borrowing against a tier-specific limit, with a repayment date computed from the borrow date.
- Repayment of borrowed credit and debt-status reporting.
- Overdue handling: `increament()` multiplies outstanding debt by 1.12 and pushes the payment date forward by 30 days (2,592,000 seconds) when the payment date has passed.
- Account tiers as defined in the constructors:

| Tier | Credit limit | Repayment period |
|--------|--------------|------------------|
| Normal | 10,000 | 60 days |
| VIP | 20,000 | 180 days |

## Tech stack

- C++ (the CMake project sets C++17)
- Qt Widgets (Qt 5 or Qt 6) for the placeholder GUI window
- CMake and Code::Blocks project files

## Repository structure

```
BankSystem/
├── include/
│   ├── Account.h        # Base account class
│   ├── Normal.h         # Normal tier
│   └── Vip.h            # VIP tier
├── src/
│   ├── Account.cpp
│   ├── Normal.cpp
│   └── Vip.cpp
├── main.cpp             # Console demo of the VIP account
├── mainwindow.cpp/.h/.ui  # Qt main window (empty shell)
├── CMakeLists.txt       # Qt/CMake project
├── BankSystem.cbp       # Code::Blocks project (console build)
└── .vscode/             # VS Code editor settings
```

## Installation

The Code::Blocks project (`BankSystem.cbp`) lists `main.cpp` and every file under `src/` and `include/`, and uses the GCC compiler with `include` as an include directory. Open it in Code::Blocks with a GCC toolchain (for example MinGW on Windows) and build.

The headers use `#include <String>` with a capital S. This resolves on case-insensitive file systems (Windows) but fails on case-sensitive ones (Linux), where it needs to be `<string>`. The sources have not been changed to fix this.

`CMakeLists.txt` is the Qt Creator-generated project. It compiles only `main.cpp`, `mainwindow.cpp`, `mainwindow.h` and `mainwindow.ui`, and does not include the `src/` files.

## Usage

Build and run from Code::Blocks, or compile directly with a GCC toolchain where `<String>` resolves:

```
g++ -Iinclude main.cpp src/*.cpp -o BankSystem
./BankSystem
```

`main.cpp` creates a `Vip` account, deposits 542, borrows 500, then prints the balance, remaining credit limit, payment date and days left to pay.

## Data

The project uses no external data and stores none; all values are created in code.

## Team / credits

- Ziyad ElFayoumy ([Ziyad-HF](https://github.com/Ziyad-HF))

## License

Released under the MIT License. See [LICENSE](LICENSE).

## Contact

Ziyad ElFayoumy, [LinkedIn](https://www.linkedin.com/in/ziyad-el-fayoumy)
