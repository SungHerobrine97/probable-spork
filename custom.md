# 自建世界观扩展

本内容仅限于某二游，并且**视为一个镜像世界**。

所有内容均应基于原版游戏正式版内容进行扩展，请勿用于任何违法用途。

## 目录

一般情况下，目录结构应该为这样子（但是**实际命名时不一定非得按照这样去做，建议你把目录结构做规范**）：

```
- 主页
- 自述
- 各个游戏世界观扩展
    - Limbus Company
        - E.G.O
            - E.G.O技能名字1
            - E.G.O技能名字2
        - 事务所
            - 事务所名字1
            - 事务所名字2
        - 其他大类
- 关于
- 合规性声明（如果涉及某些敏感内容）
- 许可和第三方通知
```

但是文件夹命名必须只有英文、破折号，**严禁带有空格和非英文字符**。以下为错误示范（此处为Docsify部署错误示例，本文的carlotta.montelli.org为虚构域名）：

```
https://carlotta.montelli.org/#/world/鸣潮
```

正确示范：

```
https://carlotta.montelli.org/#/world/wuwa
```

## 文件夹结构

如果您是Docsify用户，建议参考以下结构：

```
- docs/ 存放文档文件，仅支持markdown文档
- img/  存放图像文件
- modules/  如果你需要离线部署该文档，这个目录是必须的。
- files/    存放附加的文件，请勿部署超过650MB的文件（否则建议你使用网盘）
- css/  css样式表
- index.html    这是网页的HTML文件，如果没有这个文件你的Docsify文档将无法工作。
```

## Gitbook用户的一些说明

如果你是看到此处的内容想自己配置一个仓库，**请先不要在Github创建任何一个仓库**，先在Gitbook APP创建文档并发布网站之后再[设置Github Sync](https://gitbook.com/docs/documentation/zh/getting-started/git-sync/enabling-github-sync)，只有在配置Github Sync时没有可以操作的仓库再创建仓库。

发布网站时，请确保网络环境不在异常环境下（比如VPN、Tor路由、服务器环境下），否则容易吃封禁（[参考此处](/.gitbook/assets/eml.reply.txt)）。

Gitbook用户请参考[此处的说明](https://gitbook.com/docs/documentation/zh/getting-started/git-sync/content-configuration)配置你的仓库。

任何有关Gitbook仓库的问题请前往[此处](https://gitbook.com/docs/documentation/zh/getting-started/git-sync/troubleshooting)查看。