## Laboratory work XI

Данная лабораторная работа посвещена изучению инструментов отладки на примере **lldb**

```ShellSession
$ open https://lldb.llvm.org/tutorial.html
```

## Tasks

- [v] 1. Создать публичный репозиторий с названием **lab11** на сервисе **GitHub**
- [v] 2. Выполнить инструкцию учебного материала
- [v] 3. Ознакомиться со ссылками учебного материала
- [v] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_USERNAME=a346560
```

```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab10 lab11
$ cd lab11
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab11
```

```ShellSession
$ cmake -H. -B_build -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX=_install
cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
-- [hunter] Calculating Config-SHA1
-- [hunter] Calculating Toolchain-SHA1
-- [hunter] HUNTER_ROOT: /home/user/vershinin/lab11/hunter
-- [hunter] [ Hunter-ID: xxxxxxx | Config-ID: 75ced31 | Toolchain-ID: b8de188 ]
-- [hunter] PRINT_ROOT: /home/user/vershinin/lab11/hunter/_Base/xxxxxxx/75ced31/b8de188/Install (ver.: 0.1.0.0)
-- Configuring done
-- Generating done
-- Build files have been written to: /home/user/vershinin/lab11/_build
$ cmake --build _build --target install
Scanning dependencies of target DEMO
[ 50%] Building CXX object CMakeFiles/DEMO.dir/sources/demo.cpp.o
[100%] Linking CXX executable DEMO
[100%] Built target DEMO
Install the project...
-- Install configuration: ""
-- Installing: /home/user/vershinin/lab11/_install/bin/DEMO
$ cd _install/bin
```

```ShellSession
$ lldb demo
(lldb) target create "DEMO"
(lldb) process launch --stop-at-entry
(lldb) breakpoint list
(lldb) breakpoint set --name print
(lldb) breakpoint set --file demo.cpp --line 12
(lldb) breakpoint list
(lldb) process launch
(lldb) exit

Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "/usr/lib/python2.7/dist-packages/lldb/__init__.py", line 123, in <module>
    import six
ImportError: No module named six
(lldb) target create "DEMO"
Current executable set to 'DEMO' (i386).
(lldb) process launch --stop-at-entry
error: process launch failed: Lost debug server connection
(lldb) breakpoint list
No breakpoints currently set.
(lldb) breakpoint set --name print
Breakpoint 1: 2 locations.
(lldb) breakpoint set --file demo.cpp --line 12
Breakpoint 2: no locations (pending).
WARNING:  Unable to resolve breakpoint to any actual locations.
(lldb) breakpoint list
Current breakpoints:
1: name = 'print', locations = 2
  1.1: where = DEMO`print(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, std::ostream&) + 6 at print.cpp:4, address = DEMO[0x08048e73], unresolved, hit count = 0 
  1.2: where = DEMO`print(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, std::basic_ofstream<char, std::char_traits<char> >&) + 6 at print.cpp:8, address = DEMO[0x08048e8d], unresolved, hit count = 0 

2: file = 'demo.cpp', line = 12, exact_match = 0, locations = 0 (pending)

(lldb) process launch
error: process launch failed: Lost debug server connection
(lldb) exit

```

```ShellSession
$ demo
<Command>-T
$ ps
$ lldb
(lldb) process attach --pid <идентификатор_процесса> 
(lldb) process attach --name demo
(lldb) exit
```

```ShellSession
$ lldb demo
(lldb) process launch --stop-at-entry -- -program_arg "text1 text2 text3"
(lldb) thread list
(lldb) thread backtrace
(lldb) frame variable
(lldb) frame variable argv[0] 
```

```ShellSession
$ lldb demo
(lldb) process launch --stop-at-entry
(lldb) thread continue
(lldb) thread step-in
(lldb) thread step-over
(lldb) thread step-out
(lldb) thread step-inst
(lldb) thread step-over-inst
(lldb) exit
```
Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "/usr/lib/python2.7/dist-packages/lldb/__init__.py", line 123, in <module>
    import six
ImportError: No module named six
(lldb) target create "DEMO"
Current executable set to 'DEMO' (i386).
(lldb) process launch --stop-at-entry
error: process launch failed: Lost debug server connection
(lldb) breakpoint list
No breakpoints currently set.
(lldb) breakpoint set --name print
Breakpoint 1: 2 locations.
(lldb) breakpoint set --file demo.cpp --line 12
Breakpoint 2: no locations (pending).
WARNING:  Unable to resolve breakpoint to any actual locations.
(lldb) breakpoint list
Current breakpoints:
1: name = 'print', locations = 2
  1.1: where = DEMO`print(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, std::ostream&) + 6 at print.cpp:4, address = DEMO[0x08048e73], unresolved, hit count = 0 
  1.2: where = DEMO`print(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&, std::basic_ofstream<char, std::char_traits<char> >&) + 6 at print.cpp:8, address = DEMO[0x08048e8d], unresolved, hit count = 0 

2: file = 'demo.cpp', line = 12, exact_match = 0, locations = 0 (pending)

(lldb) process launch
error: process launch failed: Lost debug server connection
(lldb) process attach --pid <_>
error: invalid process ID '<_>'
(lldb) process attach --name DEMO
error: attach failed: could not find a process named DEMO
(lldb) process launch --stop-at-entry -- -program_arg "text1 text2 text3"
error: process launch failed: Lost debug server connection
(lldb) thread list
error: Process must be launched.
(lldb) thread backtrace
error: invalid thread
(lldb) frame variable
error: invalid thread
(lldb) frame variable argv[0] 
error: invalid thread
(lldb) process launch --stop-at-entry
error: process launch failed: Lost debug server connection
(lldb)  thread continue
error: invalid thread
(lldb) thread step-in
error: invalid thread
(lldb) thread step-over
error: invalid thread
(lldb) thread step-out
error: invalid thread
(lldb) thread step-inst
error: invalid thread
(lldb) thread step-over-inst
invalid command 'thread step-over-inst'.
(lldb) exit


```ShellSession
$ sed -i '' 's/lab10/lab11/g' README.md
```

```ShellSession
$ git add .
$ git commit -m"debugging"
$ git push origin master
```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=11
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [gdb](https://www.gnu.org/software/gdb/)
- [lldb](https://lldb.llvm.org)
- [windbg](https://msdn.microsoft.com/en-us/library/windows/hardware/dn745911(v=vs.85).aspx)

```
Copyright (c) 2017 Братья Вершинины
```
