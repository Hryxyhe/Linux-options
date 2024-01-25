# Linux-options
linux指令学习
---基本操作---
* 删除：rm -rf dir
* 复制：cp /path-to-your-source-dir /path-to-your-target-dir
* 移动：mv /path-to-your-source-dir /path-to-your-target-dir
* 创建文件夹： mkdir dir_name

--实时观察gpu--
* watch -n 1 nvidia-smi
* watch -n 1 gpustat
* nvitop

----多卡ddp训练-----
* CUDA_VISIBLE_DEVICES=0,1,2,3 python -m torch.distributed.launch --nproc_per_node=4 dist_train.py

---终止进程---
* ps -ef | grep dist_train.py | grep -v grep | awk '{print $2}' | xargs kill -9
* 该命令是用于在Linux或类Unix系统中通过进程名来终止进程的命令。以下是该命令的解释：
* ps -ef: 这个命令用于显示当前系统中所有正在运行的进程的详细信息。
* grep train.py: 通过grep命令过滤出包含"train.py"的进程信息，这样可以筛选出与"train.py"相关的进程。
* grep -v grep: 使用grep -v命令过滤掉包含"grep"的行，这样可以排除掉grep命令本身在进程列表中的信息。
* awk '{print $2}': 使用awk命令提取进程列表中的第二列，即进程ID（PID）。
* xargs kill -9: 使用xargs命令将之前提取的PID作为参数传递给kill -9命令，从而终止这些进程。

-------tmux指令-------
* 常用的tmux指令：
* tmux new-session -s mysession：启动tmux并给新会话窗口命名
* 按下 Ctrl + b 键，然后松开，然后按下 d 键：退出当前的tmux会话并将其后台运行
* tmux attach-session -t mysession：重新连接到这个会话
* tmux ls：查看所有后台运行的tmux会话
* tmux kill-session -t mysession：删除会话
* exit:永久关闭对话窗口
* Ctrl+A D：离开并会断开本地服务器连接

----screen命令启动会话窗口--------
* 使用screen命令：screen命令可以创建一个会话窗口，允许在其中运行多个终端命令，并在断开连接后保持会话状态。
* screen -S my_session：创建一个名为my_session的会话窗口
* Ctrl+A D：命令离开窗口。
* screen -r my_session：重新连接到会话窗口
* screen -list:列出所有窗口
* screen -r ip：进入某个窗口，ip为my_session前面的数字
* 配置screen的配置文件：在screen会话窗口下显示滚动条，并设置滚动缓冲区的大小为10000行：termcapinfo xterm* ti@:te@defscrollback 10000
  
 ---在tmux中启用滚动和鼠标支持---
* ①nano ~/.tmux.conf：使用nano编辑器在终端打开或创建~/.tmux.conf文件
* ②在~/.tmux.conf文件添加以下内容：
* 启用鼠标支持
* set -g mouse on
* 启用滚动支持
* set -g terminal-overrides 'xterm*:smcup@:rmcup@'
* ③依次按下ctrl+X  Y 保存并退出
* ④重新加载配置文件：tmux source-file ~/.tmux.conf

 ---软链接---
 * ln -s /path-to-your-source-dir /path-to-your-target-dir
 * Windows中完全不一样： mklink /d /path-to-your-target-dir /path-to-your-source-di



