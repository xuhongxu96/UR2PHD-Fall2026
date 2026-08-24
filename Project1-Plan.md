## Students

- Kaibo Ma
- Sami Hassan
- Tyler Zeng
- Fiona Cai

## Overview

| Week              | Date               | Objective                                                   |
| ----------------- | ------------------ | ----------------------------------------------------------- |
| [Week 1](#week-1) | Term begins - 9/18 | Setup development environment                               |
| [Week 2](#week-2) | 9/21 - 9/25        | Learn the runtime; split the work                           |
| [Week 3](#week-3) | 9/28 - 10/2        | Share and discuss design docs (Task 1)                      |
| Week 4            | 10/5 - 10/9        | Develop the task 1                                          |
| Week 5            | 10/12 - 10/16      | Finish and demo the task 1                                  |
| Week 6            | 10/19 - 10/23      | Share and discuss design docs (Task 2)                      |
| Week 7            | 10/26 - 10/30      | Develop the task 2                                          |
| Week 8            | 11/2 - 11/6        | Continue the task 2                                         |
| Week 9            | 11/9 - 11/13       | Continue the task 2                                         |
| Week 10           | 11/16 - 11/20      | Finish the task 2; summarize and present the entire project |

## Week 1

### Objectives

1. Setup development environment
2. Get familiar with `patch_llvm.py`
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
- [ ] Read thru `patch_llvm.py`
    - [ ] Skim through https://tree-sitter.github.io/tree-sitter/
    - [ ] Which files in llvm-project are patched?
    - [ ] How does it locate a function to patch?
    - [ ] Categorize the types of patches in `patch_llvm.py` (Tips: find all occurrences of `edits`)
    - [ ] Use VSCode to open `thirdparty/llvm-project` and look at the git diffs in Source Control view.

## Week 2

### Objectives

1. Learn the runtime (`fuzz_runtime.cpp` and `fuzz_runtime.h`)
3. Split the work among team members

### Tasks

#### Get Familiar with the Runtime

- [ ] Read thru `runtime/fuzz_runtime.h` and `runtime/fuzz_runtime.cpp`
    - [ ] What is `CallScope`? How is it used?
    - [ ] Where (which variable) are trace data stored?
    - [ ] When will `start_iteration` and `dump_iteration_info` be called?

#### Split the Work

- [ ] Elect a team lead
- [ ] Work in pairs or solo?
- [ ] Split the work among team members
    - Complete instrumentation
      - Instrument `ConstantFolding` (Medium)
    - Track more information
      - Track `ValueTracking` information (Hard)
      - Track remaining instructions in the worklist (Easy)
      - Track activated conditions (Hard)
    - Support other peephole passes
      - `AggressiveInstCombine` (Easy)
      - `VectorCombine` (Medium)
    - Enhance user experience
      - Clean up useless fields in the trace data (Easy)
      - Output all newly added instructions instead of just the replacement instruction (Medium)

At least one medium or hard task should be assigned to each group.
I recommend that each group to take an easy task as well
to familiarize themselves with the codebase at the beginning.

## Week 3

### Objectives

1. Each subgroup presents their design doc
2. Discuss and finalize the design doc

### Tasks

- [ ] Prepare a design doc for your first assigned task
    - Slides are not necessary, but you can use them if you want to.
- [ ] Present your design doc to the team
- [ ] Discuss and finalize the design doc
    - The gathering lasts for 1 hour, so each subgroup has 10-15 minutes to present their design doc,
        and the rest of the time is for discussion.