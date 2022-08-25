Linux入门

### 

# 文件夹操作 bash

- ls 列出目录下所有文件
- pwd 查看自己当前命令行所在目录
- cd 打开目录
  - tab 自动补全
- mkdir 创建目录
- touch 创建空文件
- cat 打印指定文件内容到屏幕上
- rm -rf  '文件夹名称或者文件名称'
  - rm -rf example

- 


# 文件编辑 vim

- 输入模式
  - 空输入模式,在任何场景下，按ESC
  - 在空输入模式下，按i，进入INSERT插入模式
    - 在空模式下，按o，进入下一个空行开始插入模式

- 命令模式
  - 在空输入模式下，按:，进入命令模式
    - 常用命令
      - w，保存文件
      - q，退出编辑

- 搜索模式
  - 在空输入模式下，按/，进入搜索模式
    - n，自动查找下一个

- 空模式下，光标移动技巧
  - G，到最后一行
  - g，到第一行
  - 上下左右
  - 通过搜索模式，快速将光标移动到想要编辑的位置
  - 通过命令模式+数字，快速将光标移动到报错的问题行

- 复杂的编辑技巧
  - 快速的剪切\删除\复制多行文字
    - Shift + V
    - Ctrl + V
    - G gg dd p
  - 还原 u 重新执行 Ctrl+R
  - d 删除选中 dd 删除整行（为了防止误删，存在剪贴板）

- vim中全选复制

  ​	**全选（高亮显示**）：按esc后，然后ggvG或者ggVG

  **全部复制：**按esc后，然后ggyG

  **全部删除：**按esc后，然后dG

  

  解析：

  **gg：**是让光标移到首行，在**vim**才有效，vi中无效 

  **v ：** 是进入Visual(可视）模式 

  **G ：**光标移到最后一行 

  **选**中内容以后就可以其他的操作了，比如： 
  **d** 删除**选**中内容 
  **y** 复制**选**中内容到0号寄存器 
  **"+y** 复制**选**中内容到＋寄存器，也就是系统的剪贴板，供其他程序用 



# 包管理以及服务管理

- Debian包管理：apt apt-get
  - /etc/apt/
  - /etc/apt/sources.list
- apt update
- apt search nginx
- apt install nginx

- 包管理器不但包含了当前Linux发行版的软件源清单，还包含了每一款软件的依赖关系

## 最常用的几个软件

- nginx WEB服务端
- haproxy 负载均衡服务端
- tmux 远程多人协作，多屏幕管理工具
  - 切换分屏
  - 切换会话
- postgresql 数据库
- nodejs 程序运行环境
- vim 编辑器


## 服务管理

- 针对一系列常用的软件进程的一套标准管理模式
- 非标管理模式
  - top 查询当前进程的CPU及内存情况
  - kill 结束当前进程
  - kill -9 最高级别的强制结束进程
  - killall 结束所有相关进程
- 标准管理模式：老 service 新 systemctl
  - service --help
    - start 开始服务
    - stop 停止服务
    - restart 重启服务
    - status 查看状态
    - enable 开机启动
  - systemctl --help

### linux 查看系统发行版本

- ​	cat /etc/issue
- 
