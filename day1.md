````
# 今日学习：Obsidian + GitHub 搭建学习笔记仓库
## 一、目标
用 Obsidian 本地写计算机学习笔记（Linux命令、Java、实验报告），使用 Git 把笔记备份上传到 GitHub，实现云端存档、版本回溯。

## 二、操作步骤 & 踩坑记录
### 1. GitHub 创建仓库
1. GitHub网页新建仓库，仓库名：`obsidian-notes`
2. 复制仓库HTTPS链接，用于本地克隆

### 2. Git 克隆仓库（重点踩坑）
命令：
```bash
git clone https://github.com/guozhifan01/obsidian-notes.git
````
```
# 1. 将所有改动加入暂存
git add .
# 2. 本地提交，引号内写更新备注
git commit -m "备注文字，例如：添加.gitignore配置"
# 3. 推送到GitHub云端
git push
```
```
ss -tulnp | grep 8080
```
1. 创建目录

```
mkdir -p /opt/java_project
cd /opt/java_project
```

2. 模拟服务脚本

```
vim demo.sh
chmod +x demo.sh //给demo.sh脚本添加可执行的权限 让系统知道这是一个可以运行的程序
```

3. 前台运行（测试用，关闭终端程序停止）

```
./demo.sh
```

4. nohup 后台运行（传统部署方式）

```
nohup ./demo.sh > demo.log 2>&1 & //忽视ssh的断开 且把正确错误的信息都写入log里 最后&表示后台运行
tail -f demo.log //查看最后十行日志 -f表示实时监测日志
ps -ef | grep demo.sh
kill PID
```

5. systemd 托管服务（生产推荐，Java 项目主流方案）

```
vim /etc/systemd/system/demo.service
systemctl daemon-reload //重新加载systemd的配置
systemctl start demo
systemctl status demo
systemctl enable demo
systemctl stop demo
systemctl disable demo
journalctl -u demo -f // -u demo只看demo这个服务的日志 -f实时滚动输出日志
```

6. 端口查看

```
ss -tulpn
ss -tulpn | grep 8080 找到占用8080端口的进程
```

## 📌面试高频问答（你可以直接背）

问：SpringBoot 项目部署 Linux 有哪两种后台运行方式？ 答： ① nohup + &：简单，临时后台运行；关闭终端不停止，但服务器重启服务就没了，需要手动启动。 ② systemd：系统托管，可以配置开机自启，方便统一启停、查看日志，生产环境首选。

问：`nohup ./demo.jar > demo.log 2>&1 &` 各部分含义？

- nohup：脱离终端，不受 SIGHUP 信号影响
- `> demo.log`：标准输出写入日志文件
- `2>&1`：错误输出重定向到标准输出，一并写入日志
- `&`：放到后台执行

问：怎么查看服务实时日志？ 答：`tail -f xxx.log`；systemd 托管的服务用 `journalctl -u 服务名 -f`