---
title: 纯净配置Zsh
date: 2023-12-09T21:21:14+08:00
draft: true
keywords:
tags:
  - draft
categories:
  - draft
resources:
  - name: featured-image
    src: featured-image.png
---

网上许多 [Zsh]
的配置教程都是使用 [oh-my-zsh] 来进行配置，
优点是配置起来**简单**，对新手友好，
缺点是太过**臃肿**，拖慢 Zsh 的启动速度。
这篇文章记录了我不使用 oh-my-zsh 从零开始配置 Zsh 的过程。

<!--more-->

## 初始配置

使用 zsh 的新用户向导 `zsh-newuser-install` 进行初始配置。

{{< admonition tip >}}
如果是第一次安装 zsh，那么安装后在终端中运行 zsh 应该会自动启动新用户向导。
{{< /admonition >}}

{{< admonition note >}}
确保你的终端尺寸至少为 72×15 大小，否则新用户向导 `zsh-newuser-install` 将无法运行。
{{< /admonition >}}

```bash
autoload -Uz zsh-newuser-install
zsh-newuser-install -f
```

运行后出现如下提示，我们依次开始配置：

```text
               *** compinstall: main menu ***
Note that hitting `q' in menus does not abort the set of changes from
Please pick one of the following options:

(1)  Configure settings for history, i.e. command lines remembered
     and saved by the shell.  (Recommended.)

(2)  Configure the new completion system.  (Recommended.)

(3)  Configure how keys behave when editing command lines.  (Recommended.)

(4)  Pick some of the more common shell options.  These are simple "on"
     or "off" switches controlling the shell's features.

(0)  Exit, leaving the existing ~/.zshrc alone.

(a)  Abort all settings and start from scratch.  Note this will overwrite
     any settings from zsh-newuser-install already in the startup file.
     It will not alter any of your other settings, however.

(q)  Quit and do nothing else.
--- Type one of the keys in parentheses ---
```

### 配置历史记录

```text
History configuration
=====================

# (1) Number of lines of history kept within the shell.
HISTSIZE=1000                                   (not yet saved)
# (2) File where history is saved.
HISTFILE=~/.histfile                            (not yet saved)
# (3) Number of lines of history to save to $HISTFILE.
SAVEHIST=1000                                   (not yet saved)

# (0)  Remember edits and return to main menu (does not save file yet)
# (q)  Abandon edits and return to main menu

--- Type one of the keys in parentheses ---
```

{{< admonition tip "`HISTSIZE` 与 `SAVEHIST` 的区别" >}}
`HISTSIZE`：单次会话在内存中保存的最大历史记录（方向键 ⬆️ 查看）数量。  
`SAVEHIST`：会话结束时在文件中保存的最大历史记录（从内存中保存）数量。
{{< /admonition >}}

### 配置新的补全系统

```text
The new completion system (compsys) allows you to complete
commands, arguments and special shell syntax such as variables.  It provides
completions for a wide range of commonly used commands in most cases simply
by typing the TAB key.  Documentation is in the zshcompsys manual page.
If it is not turned on, only a few simple completions such as filenames
are available but the time to start the shell is slightly shorter.

You can:
  (1)  Turn on completion with the default options.

  (2)  Run the configuration tool (compinstall).  You can also run
       this from the command line with the following commands:
        autoload -Uz compinstall
        compinstall
       if you don't want to configure completion now.

  (0)  Don't turn on completion.

--- Type one of the keys in parentheses ---
```

新的补全系统（compsys）允许你补全命令、参数和特殊的 shell 语法，例如变量。
它提供了对大多数常用命令的补全，通常只需按 TAB 键即可。
文档在 [zshcompsys 手册页] 中。
如果没有打开，只有一些简单的补全，例如文件名是可用的，但启动 shell 的时间稍短。

### 配置编辑键盘行为

```text
Default editing configuration
=============================

The keys in the shell's line editor can be made to behave either
like Emacs or like Vi, two common Unix editors.  If you have no
experience of either, Emacs is recommended.  If you don't pick one,
the shell will try to guess based on the EDITOR environment variable.
Usually it's better to pick one explicitly.

# (1) Change default editing configuration
bindkey -e                                      (not yet saved)

# (0) or (q)  Return to main menu (no changes made yet)

--- Type one of the keys in parentheses ---
```

shell 的行编辑器中的键可以像 Emacs 或 Vi 一样运行。
如果你对任何一个都没有经验，那么推荐使用 Emacs。
如果你没有选择一个，shell 将尝试根据 EDITOR 环境变量来猜测。
通常最好明确地选择一个。

### 配置常用选项

```text
Common shell options
====================

The following are some of the shell options that are most often used.
The descriptions are very brief; if you would like more information,
read the zshoptions manual page (type "man zshoptions").

# (1) Change directory given just path.
unsetopt autocd                                 (not yet saved)
# (2) Use additional pattern matching features.
setopt extendedglob                             (not yet saved)
# (3) Unmatched patterns cause an error.
setopt nomatch                                  (not yet saved)
# (4) Beep on errors.
unsetopt beep                                   (not yet saved)
# (5) Immediately report changes in background job status.
setopt notify                                   (not yet saved)

# (0) or (q)  Return to main menu (no changes made yet)

--- Type one of the keys in parentheses ---
```

{{< admonition tip "常用的 shell 选项" >}}

- `autocd`：直接通过路径更改目录
- `extendedglob`：使用额外的模式匹配特性
- `nomatch`：未匹配的模式导致错误
- `beep`：错误时发出蜂鸣声
- `notify`：立即报台作业状态的变化

{{< /admonition >}}

更多信息请阅读 [zshoptions 手册页]

### 保存配置

{{< admonition tip "选择 0 保存配置" >}}
如果之前没有配置过 zsh，那么会自动创建 `~/.zshrc` 文件。  
如果之前已经配置过 zsh，那么会在 `~/.zshrc` 文件中追加新的配置。
{{< /admonition >}}

查看 `~/.zshrc` 文件，可以看到刚才的配置已经被保存了。

```zsh { title = ".zshrc" }
# Lines configured by zsh-newuser-install
HISTFILE=~/.zsh_history
HISTSIZE=10000
SAVEHIST=10000
setopt extendedglob nomatch notify
unsetopt autocd beep
bindkey -e
# End of lines configured by zsh-newuser-install
# The following lines were added by compinstall
zstyle :compinstall filename '/home/bingo/.zshrc'

autoload -Uz compinit
compinit
# End of lines added by compinstall
```

## 配置主题

使用 [Starship] 配置 prompt。

### 安装 Starship

```bash { title = "Arch Linux" }
sudo pacman -S starship
```

### 启用 Starship

```bash { title = "Arch Linux" }
echo 'eval "$(starship init zsh)"' >>~/.zshrc
```

### [配置 Starship]

[Zsh]: https://www.zsh.org/ "一款功能强大的命令行解释器（shell）"
[oh-my-zsh]: https://ohmyz.sh/ "a delightful, open source, community-driven framework for managing your Zsh configuration."
[zshcompsys 手册页]: https://linux.die.net/man/1/zshcompsys "zshcompsys - zsh completion system"
[zshoptions 手册页]: https://linux.die.net/man/1/zshoptions "zshoptions - zsh options"
[Starship]: https://starship.rs/ "The minimal, blazing-fast, and infinitely customizable prompt for any shell!"
[配置 Starship]: https://starship.rs/zh-CN/config/#配置
