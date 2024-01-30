# pica-cli

![NPM Version](https://img.shields.io/npm/v/pica-cli)

😉 哔咔漫画下载器

![演示](https://s2.loli.net/2024/01/29/rhcOo4GBD8kLEqv.gif)

- 交互式命令行
- 排行榜：下载当前排行榜的全部漫画
- 收藏夹：下载当前用户收藏夹的全部漫画
- 关键词搜索：支持多选
- 自动过滤已下载的章节和图片，不会重复下载
- 如果没有相关环境变量，则启动交互命令界面；若有则直接执行
- 通过 `pica-zip` 命令分章节批量压缩，配合支持 zip 包的漫画阅读软件使用，比如 [Perfect Viewer](https://play.google.com/store/apps/details?id=com.rookiestudio.perfectviewer)。
  不限于 `pica-cli` 下载的漫画使用，只要符合 [cmoics/漫画标题/漫画章节/漫画图片](#) 的目录结构即可。

如果用的开心，希望给个 star 支持一下，比心 ~ ❤️

## 用法

### 方式一：GitHub Actions（推荐）

利用 GitHub 的免费服务器下载，最关键的是不用科学上网，网速飞快，孩子用了都说好。

```bash
# 必填，固定值，不要修改
# ~d}$Q7$eIni=V)9\RK/P.RM4;9[7|@/CA}b~OW!3?EV`:<>M7pddUBL5n|0/*Cn
PICA_SECRET_KEY
# 必填，账号名
PICA_ACCOUNT
# 必填，账号密码
PICA_PASSWORD
```

fork 一份本仓库，将上面三个环境变量，设置为仓库密钥：

![action secret](https://s2.loli.net/2024/01/30/5FxU7olyWC3VAe1.png)

然后点击 Actions，再点击左侧的 `task` 工作流，再点击右侧的 `Run workflow`，输入相关的信息，点击运行即可。

![action run](https://s2.loli.net/2024/01/30/PmfublZKLFQrth9.png)

等执行完之后，进入执行详情，点击 Summary，在最下方有漫画的完整压缩包，下载即可。

![action summary](https://s2.loli.net/2024/01/30/eiRu2B9hovJxOzQ.png)

![artifact](https://s2.loli.net/2024/01/30/MJBxVe9UtszNmiv.png)

如果你想自定义过程，比如不想把每个章节打成压缩包，请自行修改 [.github/workflows/task.yaml](.github/workflows/task.yaml)。

### 方式二：直接安装

```bash
pnpm add pica-cli -g
```
在自己电脑上配置好环境变量，所需的环境变量如下所示：

```bash
# 必填，固定值，不要修改
PICA_SECRET_KEY=~d}$Q7$eIni=V)9\RK/P.RM4;9[7|@/CA}b~OW!3?EV`:<>M7pddUBL5n|0/*Cn
# 必填，账号名
PICA_ACCOUNT=
# 必填，账号密码
PICA_PASSWORD=
# 代理地址，示例：http://127.0.0.1:7890
PICA_PROXY=
# 下载图片的并发数，默认 5
PICA_DL_CONCURRENCY=5
# leaderboard | favorites | search
# 下载内容，分别表示：排行榜 | 收藏夹 | 搜索
PICA_DL_CONTENT=
# 搜索关键字，多个用 # 隔开
# 尽量输入完整漫画名，避免返回过多结果
PICA_DL_SEARCH_KEYWORDS=
```

```bash
# 运行
pica-cli

# 漫画下好后，生成 zip
pica-zip
```

## 开发

```bash
git clone https://github.com/justorez/pica-cli.git
```

拷贝一份 [.env.template](.env.template)，命名为 `.env.local`，填写好后就不用设置环境变量了，配置优先从 `.env.local` 里加载。

```bash
# 安装依赖
pnpm install

# 运行
pnpm dev

# 漫画打压缩包
pnpm dev:zip
```

[哔咔 API 文档（非官方）](https://www.apifox.cn/apidoc/shared-44da213e-98f7-4587-a75e-db998ed067ad/doc-1034189)。

## 更新日志

- 2024/01/30 提供 GitHub Actions 的下载方式
- 2024/01/29 下载完成后，提供命令把漫画按章节批量压缩
- 2024/01/28 完成基本功能

## 其他

代码参考了 [pica_crawler](https://github.com/lx1169732264/pica_crawler)，本来是想添加新功能，奈何 Python 早就忘光了，只好重写一个。
