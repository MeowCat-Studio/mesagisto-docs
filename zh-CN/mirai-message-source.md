# mirai消息源
**[Mesagisto信使项目](https://github.com/MeowCat-Studio/mesagisto)的一部分，消息转发客户端的mirai(Tencent-QQ)实现。**

## 需求
- Mirai 2.12.0+, MCL 2.1.0+
- 对于Windows, 需要安装 [Microsoft Visual C++ 2010 Redistributable运行时](https://www.microsoft.com/en-us/download/details.aspx?id=26999) 运行时位数应与JDK保持一致
## 安装
  1. 在[Releases页面](https://github.com/MeowCat-Studio/mirai-message-source/releases) 下载jar归档文件。
  2. 移动至mirai-console(或是mcl)同目录的plugins文件夹下。
## 简单入门
  1. 运行一次MCL并关闭
  2. MCL目录下 找到配置文件 config/org.meowcat.mesagisto/mesagisto.yml 并修改

  ```yaml
  # 是否启用插件
  enable: true
  # 中间转发服务器,消息的桥梁. 默认为我个人提供的[NATS](https://github.com/nats-io/nats-server)服务器
  nats:
    address: 'nats://itsusinn.site:4222'
  # 加密设置
  cipher:
    # 加密用使用的密钥
    key: your-key
  # 网络代理, 下载Telegram或Discord图片时所需
  # 注意, 如果tg-bot/dc-bot与mirai-bot在同一台主机
  # 仅设置tg-bot/dc-bot的代理即可
  proxy:
    # 是否启用代理
    enable: false
    # 代理服务器地址
    address: 'http://127.0.0.1:7890'
  # 实验性权限配置
  perm: 
    # 严格模式, 当启用时
    # 信使仅对下方users列表内用户所发命令作出响应
    strict: false
    # 用户列表, QQ号
    users: 
      - 123456
  # 存放信使频道与QQ群的对应关系,默认为空. 不推荐手动添加.
  bindings: {}
  ```

  3. 群主 (**除了BOT自身**) 可以执行以下指令 `/f` 或 `/信使` 将会得到
  ```
          未知指令
          ------  用法  ------
          /信使 绑定 [频道名]
          或 
          /f bind [频道名]
          例如
          /f bind 114514、/信使 绑定 114514 等
          ------  列表  ------
          /f help = /信使 帮助
          /f unbind = /信使 解绑
          /f about = /信使 关于
          /f status = /信使 状态
  ```
  任何管理员或群主可通过`/信使 设置频道 [频道名]`或`/f sc [频道名]`设置频道

  > 在 **QQ 群聊**(而不是 Mirai 控制台)中发送这些指令.
## 注意事项
  1. 现在信使**不再依赖**前置插件[chat-command]
