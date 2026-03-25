# 42sh - POSIX Shell Implementation in C

> **Privacy Note:** The source code of this project is kept private to comply with EPITA's anti-plagiarism regulations. The code is structured, commented, and available upon request for recruiters during an interview. This repository serves as a technical showcase and provides a testable compiled version.

## 📖 Project Context

The **42sh** project is a core EPITA curriculum requirement. The goal is to recreate a complete command interpreter (shell) from scratch, complying with the POSIX standard. This project requires a deep understanding of UNIX system programming, language theory (Lexer/Parser), and software architecture.

**My Role:** I led the team development of this UNIX shell as **Project Manager and Git Administrator**. I managed the entire development cycle, coordinated the team, and personally designed the core of the interpreter: the Parser and the AST generation logic.

## ✨ Implemented Features

All of the following features were developed in C and are fully operational:

* **Command Execution:** `$PATH` search and binary execution (via `fork` and `execvp`) with error return code handling.
* **Built-ins:** Native implementation of `echo`, `cd`, `exit`, `export`, `unset`, `set`, `.`, `true`, `false`, as well as loop management with `break` and `continue`.
* **Control Structures:** * Conditions: `if / then / elif / else / fi`.
    * Loops: `while`, `until` and `for`.
* **Logical Operators:** Command chaining with `&&`, `||` and negation with `!`.
* **Pipelines and Redirections:** * Full management of pipes `|` to connect the output of one process to the input of another.
    * Single and multiple redirections: `>`, `<`, `>>`, `>&`, `<&`, `<>`.
* **Variables Management:** Assignment, variable expansion, and special variables handling like `$?` (return code of the last command).
* **Command Grouping:** Execution blocks `{ ... }` and subshells creation `( ... )`.
* **Quoting:** Support for weak (`"`) and strong (`'`) quoting for special characters escaping.

## 🏗️ Technical Architecture

The shell operates on a classic compilation/interpretation pipeline. As the core architect of the parsing phase, the structure is defined as follows:

1. **Lexer (Lexical Analysis):** Reads standard input (or script) character by character and generates a stream of "Tokens" (Words, Operators, Redirections).
2. **Parser (Syntax Analysis) [My Core Contribution]:** I implemented a syntax analyzer that transforms the token stream into a complex Abstract Syntax Tree (AST). This module strictly manages the nesting of control structures and enforces the rigid grammar of the Shell Command Language.
3. **Execution (AST Traversal):** The tree is traversed recursively. Redirections modify file descriptors (`dup2`), child processes are created (`fork`), and commands are executed.

## 🧠 Technical Challenges Solved

* **Memory Management:** Special attention to preventing memory leaks, particularly complex during AST destruction and syntax error handling.
* **Process Synchronization:** Precise use of `waitpid` to coordinate child processes execution in a pipeline without creating zombie processes.
* **File Descriptors Manipulation:** Restoring standard streams (STDIN/STDOUT/STDERR) after executing commands with complex redirections.

## 🛠️ Technologies Used

* **Language:** C (POSIX 2008 Standard)
* **Build System:** Makefile / Autotools (configure)
* **Version Control:** Git
* **Testing:** Custom Bash testsuite for non-regression validation.

## 🎯 How to test the project?

A pre-compiled version of the shell is available for testing.

1. Go to the **[Releases](../../releases)** section.
2. Download the archive containing the `42sh` executable.
3. Open a terminal in a Linux environment (or WSL on Windows) and run the executable:

```bash
tar -xvf 42sh_release.tar.gz
chmod +x 42sh
./42sh
```

### 👥 The Team
* **[Wael Akhdar](Ton_Lien_GitHub)**
* **[Youcef Zahra](https://github.com/youcefzahra)**
* **[Jessim Ziani](https://github.com/jessim-ziani)**
* **[Louis-Maximilien Chappuit](https://github.com/louischap31)**

