---
title: 'Mac 修改'
subtitle: ''
layout: post
date: 2024-03-31
header-img: "img/post-bg-halting.jpg"
catalog: true
tag: 
    - Mac
    - record
---

```python
"""去除iBooks摘抄引用"""
import sys
import re
content = ''
for t in sys.stdin:
	content += t
p = re.compile('“([\s\S]*)”[\n]*摘录来自')
if p.search(content) is not None:
	copy = p.search(content).group(1)
	if copy:
		print(copy)
else:
	print(content)
```



```python
import sys
import re
content = ''
#从stdin里读取内容
for t in sys.stdin:
   content += t
#利用正则表达式来查找原文并去除添加的引用信息
p = re.compile('“(.+)”\n\nExcerpt From')
copy = p.search(content).group(1)
#用print函数把结果传回Automator
if copy:
    print(copy)
```



## 2024-4-18

1. `brew install tree`

```bash
Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
```



2. `问题`：直接编译`keyrecovery4.cpp`文件，会报错如下：

```bash
  ld: Undefined symbols:
    partially_decrypt(unsigned char*, unsigned char*), referenced from:
        distinguisher_1(unsigned char*, unsigned char*, std::__1::set<int, std::__1::less<int>, std::__1::allocator<int>>&) in recover-bb342d.o
        distinguisher_1(unsigned char*, unsigned char*, std::__1::set<int, std::__1::less<int>, std::__1::allocator<int>>&) in recover-bb342d.o
  clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

  文件的tree如下：
```bash
$ tree -a
.
├── .vscode
│   └── settings.json
├── SmallAES.cpp
├── SmallAES.h
├── keyrecovery4
└── keyrecovery4.cpp

2 directories, 5 files
```



> 经过一些迷信的测试之后，可能是ld 缓存没有更新导致的。（下次出现这个问题的时候重新试试看。。。

```bash
update_dyld_shared_cache
```



> [vscode](https://blog.csdn.net/qq_45488242/article/details/128414756)
>
> [reference](https://blog.csdn.net/qq_33973359/article/details/105720511)



### 2024-4-10

1. 为vscode增加了copilot

### 2024-4-9

1. 创建符号链接将`/opt/homebrew/bin/python3`链接到`/usr/local/bin/python3`

​		`sudo ln -s /opt/homebrew/bin/python3 /usr/local/bin/python3`

2. 安装了rust，位置在?
3. 安装了mdbook，位置在`$HOME/.cargo/bin`
4. 增加了一个自动去掉ibooks copy时候的尾巴，存储在`/Users/bingwu/Library/Services/ibook去除摘抄引用.workflow`

   快捷键为`cmd+shift+L`

5. 收获[apple clean instructions](https://support.apple.com/zh-cn/103258)

6. 解决Mac合盖后hdmi连接显示器，显示器黑屏

> 1、在Mac电脑中打开**系统偏好设置**，
>
> 2、在系统偏好设置中点击“**节能**”
>
> 3、进入节能设置窗口后，点击“**电源适配器**”标签；
>
> 4、在电源适配器设置面板中，勾选上“**当显示器关闭时，防止电脑自动进入睡眠**”即可。