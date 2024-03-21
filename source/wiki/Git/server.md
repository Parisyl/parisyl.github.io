---
wiki: Git
title: 搭建 Git 服务器
---

## 横向对比
表格中的符号含义:

- ✓ - 支持
- ⁄ - 部分支持
- ✘ - 不支持
- ? - 不确定

{% tabs align:center %}
<!-- tab 主要特性 -->
|特性|Gitea|Gogs|GitHub EE|GitLab CE|GitLab EE|BitBucket|RhodeCode CE|
|---|---|---|---|---|---|---|---|
|开源免费|✓|✓|✘|✓|✘|✘|✓|
|低资源开销 (RAM/CPU)|✓|✓|✘|✘|✘|✘|✘|
|支持多种数据库|✓|✓|✘|⁄|⁄|✓|✓|
|支持多种操作系统|✓|✓|✘|✘|✘|✘|✓|
|升级简便|✓|✓|✘|✓|✓|✘|✓|
|支持 Markdown|✓|✓|✓|✓|✓|✓|✓|
|支持 Orgmode|✓|✘|✓|✘|✘|✘|?|
|支持 CSV|✓|✘|✓|✘|✘|✓|?|
|支持第三方渲染工具|✓|✘|✘|✘|✘|✓|?|
|Git 驱动的静态 pages|✘|✘|✓|✓|✓|✘|✘|
|Git 驱动的集成化 wiki|✓|✓|✓|✓|✓|✓ (cloud only)|✘|
|部署令牌|✓|✓|✓|✓|✓|✓|✓|
|仓库写权限令牌|✓|✘|✓|✓|✓|✓|✓|
|内置容器 Registry|✓|✘|✓|✓|✓|✘|✘|
|外部 Git 镜像|✓|✓|✘|✘|✓|✓|✓|
|WebAuthn (2FA)|✓|✘|✓|✓|✓|✓|?|
|内置 CI/CD|✘|✘|✓|✓|✓|✘|✘|
|子组织：组织内的组织|✘|✘|✘|✓|✓|✘|✓|
<!-- tab 代码管理 -->
|特性|Gitea|Gogs|GitHub EE|GitLab CE|GitLab EE|BitBucket|RhodeCode CE|
|---|---|---|---|---|---|---|---|
|仓库主题描述|✓|✘|✓|✓|✓|✘|✘|
|仓库内代码搜索|✓|✘|✓|✓|✓|✓|✓|
|全局代码搜索|✓|✘|✓|✘|✓|✓|✓|
|Git LFS 2.0|✓|✘|✓|✓|✓|✓|✓|
|组织里程碑|✘|✘|✘|✓|✓|✘|✘|
|细粒度用户角色 (例如 Code, Issues, Wiki)|✓|✘|✘|✓|✓|✘|✘|✘|
|提交人的身份验证|⁄|✘|?|✓|✓|✓|✘|
|GPG 签名的提交|✓|✘|✓|✓|✓|✓|✓|
|SSH 签名的提交|✓|✘|✘|✘|✘|?|?|
|拒绝未用通过验证的提交|✓|✘|✓|✓|✓|✓|✓|
|仓库活跃度页面|✓|✘|✓|✓|✓|✓|✓|
|分支管理|✓|✘|✓|✓|✓|✓|✓|
|建立新分支|✓|✘|✓|✓|✓|✘|✘|
|在线代码编辑|✓|✓|✓|✓|✓|✓|✓|
|提交的统计图表|✓|✘|✓|✓|✓|✓|✓|
|模板仓库|✓|✘|✓|✘|✓|✓|✘|
<!-- tab Issues -->
|特性|Gitea|Gogs|GitHub EE|GitLab CE|GitLab EE|BitBucket|RhodeCode CE|
|---|---|---|---|---|---|---|---|
<!-- tab Pull/PR -->
|特性|Gitea|Gogs|GitHub EE|GitLab CE|GitLab EE|BitBucket|RhodeCode CE|
|---|---|---|---|---|---|---|---|

<!-- tab 第三方集成 -->
|特性|Gitea|Gogs|GitHub EE|GitLab CE|GitLab EE|BitBucket|RhodeCode CE|
|---|---|---|---|---|---|---|---| 

{% endtabs %}

## Gitea
{% note 👍&nbsp;推荐 color:green [Gitea](https://about.gitea.com) 是一个开源社区驱动的轻量级代码托管解决方案，后端采用 Go 编写，采用 MIT 许可证。我现在使用的就是它。相较于 gitlab 更轻量级，内存占用更小，适合个人或小型团队使用。%}

{% tabs %}
<!-- tab 使用Docker安装 -->
{% link https://docs.gitea.cn/installation/install-with-docker/ %}

<!-- tab 使用包管理安装 -->
{% link https://docs.gitea.cn/installation/install-from-package/ %}

以{% mark macOS %}为例，输入这两行代码就可以完成本地安装：
{% code %}
brew tap gitea/tap https://gitea.com/gitea/homebrew-gitea
brew install gitea
{% endcode %}
{% endtabs %}

## Gitblit
{% note 🚫&nbsp;不推荐 color:yellow 相较于前面提到的几款而言不是很推荐使用这个 %}

{% timeline %}
<!-- node 安装 JDK -->
下载并安装 JDK：[javase-downloads](https://www.oracle.com/java/technologies/downloads/)
<!-- node 安装并配置 Gitblit -->
- 下载 [gitblit](https://github.com/gitblit-org/gitblit)
- 解压 Gitblit，进入目录 `~/gitblit-1.8.0/data/defaults.properties`
- 用编辑器打开 `defaults.properties`
{% code %}
git.repositoriesFolder = /Users/用户名/gitserver/gitRepository
server.httpPort = 7070
{% endcode %}

<!-- node 启动服务 -->
在终端中执行 `gitblit.sh` 脚本即可启动服务：
```sh
./gitblit.sh,
```
**建议设置开机自启动**
通过 Mac 的自动化工具，将启动指令写成脚本，系统启动后自动运行脚本即可。
Windows 平台可以添加到启动计划任务中。

<!-- node 客户端访问 -->
用服务器 IP + 端口号来访问。例如我的电脑的 IP 是 `10.8.12.200`，那么在局域网内另外一台电脑访问 `http://10.8.12.200:7070` 就可以看到管理页面了：
![](https://f005.backblazeb2.com/file/img-forWeb/uPic/6v6vWV.jpg)

网页操作和使用 GitHub、Coding 等平台相似，非常简单。

{% endtimeline %}

