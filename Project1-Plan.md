## Students

- Kaibo Ma
- Sami Hassan
- Tyler Zeng
- Fiona Cai

## Overview

| Week             | Date               | Objective                     |
| ---------------- | ------------------ | ----------------------------- |
| [Week 1](#week-1) | Term begins - 9/18 | Setup development environment |
| Week 2           | 9/21 - 9/25        |                               |
| Week 3           | 9/28 - 10/2        |                               |
| Week 4           | 10/5 - 10/9        |                               |
| Week 5           | 10/12 - 10/16      |                               |
| Week 6           | 10/19 - 10/23      |                               |
| Week 7           | 10/26 - 10/30      |                               |
| Week 8           | 11/2 - 11/6        |                               |
| Week 9           | 11/9 - 11/13       |                               |
| Week 10          | 11/16 - 11/20      |                               |

## Week 1

### Objective

1. Setup development environment
2. Get familiar with `patch_llvm.py`
    - You may want to read https://tree-sitter.github.io/tree-sitter/ first
3. Be able to debug Python and C++ code

### Tasks

#### Preliminary

> You can use any IDE that you like, but I will only demonstrate using VSCode. (You may have to figure out any issues you may encounter by yourself for other IDEs, but feel free to ask, and I'll try my best to help.)

- [ ] Install `uv`, `cmake`, `clang`, `ccache`
- [ ] Clone https://github.com/xuhongxu96/instcombine-instrumentor.git
- [ ] Clone llvm-project by running `clone_llvm.sh`
- [ ] Prepare Python environment by running `uv sync`
- [ ] Patch LLVM (`uv run patch_llvm.py`)

#### Build Native Version

- [ ] Build (`build_patched_llvm.sh`)
- [ ] Run smoke test (`smoke_test.sh`)

#### Build WASM Version

- [ ] Install emsdk (https://emscripten.org/docs/getting_started/downloads.html)
- [ ] Build WASM (`build_wasm.sh`)
- [ ] Run smoke test (`node wasm/test/smoke_wasm.mjs`)

#### Get Familiar with the Project

- [ ] Ensure you can debug Python code
    - [ ] VSCode Extensions: Python, Pylance, Python Debugger, Python Environments, Ruff
    - [ ] Configure `launch.json` in VSCode
    - [ ] Set a breakpoint in `patch_llvm.py` at Line 484 (`if body is None:`)
    - [ ] Print `get_function_name(func_node)`
    - [ ] What's the function name when the breakpoint is first hit?
- [ ] Ensure you can debug C++ code
    - [ ] VSCode Extensions: clangd, CMake Tools, LLDB DAP
    - [ ] Build native version in Debug mode
        - `BUILD_DIR=build/llvm-dbg BUILD_TYPE=Debug bash build_patched_llvm.sh`
    - [ ] Configure `launch.json` in VSCode
    - [ ] Set a breakpoint in `thirdparty/llvm-project/llvm/lib/IR/fuzz_runtime.cpp` at Line 365 (`record_stacktrace_internal(new_val)`)
    - [ ] What's the call stack now?
    - [ ] Switch to `visitAdd` frame
    - [ ] Print `(llvm::Value::ValueTy)I.getOperand(0)->SubclassID`
    - [ ] Print `(llvm::Value::ValueTy)I.getOperand(1)->SubclassID`
    - [ ] What are the value types of the two operands?

```json
{
    "configurations": [
        {
            "type": "lldb-dap",
            "request": "launch",
            "name": "opt",
            "program": "${workspaceFolder}/build/llvm-dbg/bin/opt",
            "args": [
                "-passes=instcombine",
                "test.ll"
            ],
            "env": [],
            "cwd": "${workspaceFolder}"
        },
        {
            "name": "patch_llvm.py",
            "type": "debugpy",
            "request": "launch",
            "program": "${workspaceFolder}/patch_llvm.py",
            "console": "integratedTerminal"
        },
    ]
}
```