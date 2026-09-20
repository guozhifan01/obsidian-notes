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