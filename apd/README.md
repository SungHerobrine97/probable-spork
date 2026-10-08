# A.P.D.脚本编写

因为是接触了cmd脚本，再者为了防止被带坏所以有了这个文章。

## 简述

我们不知道这是开了几个坑了。

不用多说，就是用来介绍某种安装盘自动播放脚本的。

## 前提

执行任何命令之前，一定要先定义一下变量。此处为cmd脚本片段示例。

```bat
set ANYTHING=Dirs
```

其中，`ANYTHING`可以被替换为任意值，`Dirs`只能为相对路径，开头**不能携带斜杠**。

然后，你只需确保你要构建的目录可以被普通用户读写，并且确定好你需要的目录之后再写脚本（**不要使用管理员权限**）。

```bat
set DOCS_DIR=docs
set DATA_DIR=data
set SETUP_DIR=setup
set RUNTIME_DIR=runtime
```

这些变量当中，如果后续引用两边有一边不带`%`符号，可能会让你的脚本无法工作。

## 菜单

建议在这里做个判断，如果不在根目录携带特殊标记，则必须先运行一次构建流程。

读取配置文件建议参考以下链接：[此处](https://www.cnblogs.com/SoaringLee/p/10532265.html)

相关脚本如下：
```bat
::此处为变量配置
::请勿模仿脚本内的操作，如果你试图读取ini文件可能会出现未验证的问题。
set CONFIG=config.txt
::此处为判断
if not exist "%CONFIG%" (
  exit 255
) else (
  set /p OEM=<config.txt
  goto another_stage
)
:another_stage
...
```

你可能会了解到检测到文件不存在时返回255的退出码，别笑，这是故意的，后文会直接改（下面也是一样）。

```bat
::此处为变量配置
::请勿模仿脚本内的操作，如果你试图读取ini文件可能会出现未验证的问题。
set CONFIG=config.txt
::此处为判断
if not exist "%CONFIG%" (
  goto another_stage
) else (
  echo Config exist, skip.
  exit 0
)
:another_stage
echo Welcome.
echo We will complete the process of A.P.D. Build.
echo So, what is your project name?
set /p TITLE=
echo Ok, anything else?
...
```

接下来就是没找到文件时先询问项目标题，再询问你的构建选项。

> 这个时候不会有任何生成式AI成分，如果你仍然认为这东西需要联网那就需要编写为程序并加壳（否则容易被看出来，有时候我们为了合规性不得不做出很多努力）。

然后是写一下配置文件没找到的逻辑，只要没找到直接问后面的创建过程，否则显示菜单：

```bat
if not exist "%CONFIG%" (
    goto build
)  else (
    set /P apd_title=<"%CONFIG%"
    goto menu
)
```

注意一下，这里的文件内容只能为一项目名字，实际编写脚本需要注意，更不要模仿。

然后就是一些构建选项，这里跳过，你都会设置变量了，新建文件夹这一类操作对你而言也就没难度了。

下面的一个命令可供你打开文件夹参考：
```bat
explorer.exe %cd%
```

完整脚本示例见下：
```bat
@echo off

set CONFIG=config.txt
set DOCS_DIR=docs
set DATA_DIR=data
set SETUP_DIR=setup
set RUNTIME_DIR=runtime

:check
if not exist "%CONFIG%" (
    goto build
)  else (
    set /P apd_title=<"%CONFIG%"
    goto menu
)
:build
echo Welcome!
echo We will complete the config file creation.
echo Input your project title.
:input_title
set /p TITLE=
if "%TITLE%"=="" (
    echo Are you serious?
    goto input_title
) else (
    goto build2
)
:build2
echo So, what do you do next?
echo.
echo [1] data,docs,setup
echo [2] docs only
choice /c 12 /n >nul
if %ERRORLEVEL%==1 (
    goto b1
)
if %ERRORLEVEL%==2 (
    goto b2
)
:b1
if not exist "%DOCS_DIR%" (
    mkdir "%DOCS_DIR%"
) else (
    echo docs dir exists, skip.
)
if not exist "%DATA_DIR%" (
    mkdir "%DATA_DIR%"
) else (
    echo data dir exists, skip.
)
if not exist "%SETUP_DIR%" (
    mkdir "%SETUP_DIR%"
) else (
    echo setup dir exists, skip.
)
echo %TITLE%>config.txt
if exist "%CONFIG%" (
    echo Done!
    pause
    exit 0
)
:b2
if not exist "%DOCS_DIR%" (
    mkdir "%DOCS_DIR%"
) else (
    echo docs dir exists, skip.
)
echo %TITLE%>config.txt
if exist "%CONFIG%" (
    echo Done!
    pause
    exit 0
)
:menu
::请勿照抄此处的代码，如果这是刚创建的空白文件夹则可以忽略这个注释。
::否则你应该根据实际情况修改脚本（你只管后面的choice和if语句然后比葫芦画瓢，然后后续的命令指向一个可执行文件即可）
echo %apd_title% Autoplay CLI
echo.
echo What do you do next?
echo.
:: That is your advanture.
echo [1] Project dir
echo [2] Exit
choice /c 12 /n >nul
if %ERRORLEVEL%==1 (
    explorer.exe %cd%
    exit 0
)
if %ERRORLEVEL%==2 (
    exit 0
)
::按实际需要修改代码并取消注释即可。
::if %ERRORLEVEL%==x (
::    example.exe
::)
```