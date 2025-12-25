# Linux 常用指令速查

以下内容按功能分类，包含常用命令和典型示例，适合工程实践。

---

## 基本帮助与环境
- 查看帮助：`man <command>` 或 `command --help`  
  例：`man ls` / `ls --help`
- 查看环境变量：`env` / `printenv`
- 设置临时环境变量：`export VAR=value`
- 永久设置（bash）：编辑 `~/.bashrc` 并执行 `source ~/.bashrc`

---

## 文件与目录（导航）
- 列目录：`ls`，带详细信息和隐藏文件：`ls -la`
- 当前路径：`pwd`
- 切换目录：`cd <dir>`，上级目录：`cd ..`，家目录：`cd` 或 `cd ~`
- 创建目录：`mkdir <dir>`，递归创建：`mkdir -p a/b/c`
- 删除文件/目录：`rm file`，强制递归目录：`rm -rf dir`（小心使用）

---

## 文件操作（读写复制移动）
- 复制：`cp src dest`，保留属性：`cp -a src dest`
- 移动/重命名：`mv old new`
- 创建空文件：`touch file`
- 查看文件内容：`cat file`，分页查看：`less file` / `more file`
- 查看文件前/后若干行：`head -n 20 file` / `tail -n 50 file`
- 实时查看追加内容：`tail -f file`

---

## 权限与属主
- 改变权限：`chmod 755 file` 或 `chmod u+rwx,g+rx,o+rx file`
- 改变属主/属组：`chown user:group file`
- 查看权限：`ls -l`

---

## 查找文件 / 内容
- 按名字查找文件：`find /path -name "pattern"`  
  例：`find . -name "*.py"`
- 快速查找文件：`locate filename`（需先 `sudo updatedb`）
- 在文件中查找文本：`grep -R "pattern" .`  
  高亮：`grep --color=auto`
- 组合示例：`grep -R "TODO" --include="*.py" ./src`

---

## 文本处理
- 统计行数/单词：`wc -l file` / `wc -w file`
- awk（字段处理）：`awk '{print $2}' file`
- sed（替换）：`sed 's/old/new/g' file`，写回文件：`sed -i 's/old/new/g' file`
- cut（按列截取）：`cut -d',' -f1 file`

---

## 打包与压缩
- tar 打包 gzip 压缩：`tar -czvf archive.tar.gz folder/`
- 解压 tar.gz：`tar -xzvf archive.tar.gz`
- zip 压缩：`zip -r archive.zip folder/`  
- unzip 解压：`unzip archive.zip`

---

## 网络与远程
- 测试连通：`ping example.com`
- 查看端口监听：`ss -tuln` 或 `netstat -tuln`
- HTTP 下载：`curl -O URL` / `wget URL`
- SSH 登录远程：`ssh user@host`
- SCP 复制文件：`scp localfile user@host:/path/`
- rsync 同步：`rsync -avz localdir/ user@host:/path/`

---

## 进程与资源监控
- 查看实时进程：`top` / `htop`
- 查找进程：`ps aux | grep process_name`
- 杀进程：`kill <pid>` 或 `kill -9 <pid>`
- 查看磁盘使用：`df -h`
- 查看目录大小：`du -sh /path/*`

---

## 包管理（Debian/Ubuntu）
- 更新包索引：`sudo apt update`
- 安装包：`sudo apt install package`
- 升级包：`sudo apt upgrade`
- 搜索包信息：`apt search name`
- 清理缓存：`sudo apt autoremove`

---

## Python / 虚拟环境 / pip
- 创建虚拟环境：`python3 -m venv .venv`
- 激活：`source .venv/bin/activate`
- 退出虚拟环境：`deactivate`
- 安装依赖：`pip install -r requirements.txt`
- 查看已安装包：`pip list` 或 `pip freeze > requirements.txt`

---

## 服务管理（systemd）
- 启动服务：`sudo systemctl start servicename`
- 停止服务：`sudo systemctl stop servicename`
- 重启服务：`sudo systemctl restart servicename`
- 查看状态：`systemctl status servicename`
- 开机自启：`sudo systemctl enable servicename`
- 查看日志：`journalctl -u servicename -f`

---

## 容器（Docker）
- 查看容器：`docker ps`，所有容器：`docker ps -a`
- 启动容器：`docker run -it --rm imagename bash`
- 停止容器：`docker stop container_id`
- 查看镜像：`docker images`
- 构建镜像：`docker build -t name:tag .`

---

## 系统信息与诊断
- 查看内存：`free -h`
- 查看 CPU：`lscpu`
- 查看磁盘分区：`lsblk`
- 查看主机名/IP：`hostname` / `ip a`
- 查看环境变量：`env` / `printenv`

---

## 常用技巧与快捷
- 管道与重定向：`cmd1 | cmd2`，`cmd > out.txt`，追加：`>>`
- 后台运行：`command &`，查看任务：`jobs`，前台：`fg`
- 使用 sudo：`sudo <command>`
- 历史搜索：`Ctrl+R`
- 快速切换目录：`cd -`
- 复制到剪贴板（Ubuntu）：`cat file | xclip -selection clipboard`（需安装 xclip）

---

## 安全与注意事项
- `rm -rf` 非常危险，务必确认路径
- 避免在系统 Python 上随意 pip 安装，使用虚拟环境
- 小心提交敏感信息（`.env`、密钥等）
