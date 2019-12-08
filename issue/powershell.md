# PowerShell

### 1. 此系统中禁止执行脚本

#### 产生环境

- 环境: Win10 19033.1
- 时间：2019/12/8

#### 解决方法

1. 使用管理员模式打开 PowerShell
2. 运行下面命令

```
set-executionpolicy remotesigned
```

#### 参考

<https://www.cnblogs.com/zhaozhan/archive/2012/06/01/2529384.html>
