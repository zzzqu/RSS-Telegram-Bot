# 更新日志

## 频道远程管理、更多格式化选项和更多 (v2.2.0)

### 新特性

#### 亮点

- **频道/群组远程管理**: 现在你可以在和 bot 的私聊里管理你的频道/群组的订阅。支持使用大部分命令。只需以类似于 `/sub @username https://exmaple.com` 或 `/sub -10010000000000 https://exmaple.com` 的格式发送命令。(`@username` 是频道/群组的用户名, `@` 是不可缺少的; `-10010000000000` 是频道/群组的 ID, 必须以 `-100` 开头)
- **更多格式化选项**:
    - **媒体**: 你可以选择让 Telegram 消息不带任何媒体 (只有文字)。也可以选择让 Telegram 消息只带有媒体和元数据 (没有内容)；只有当有媒体附加到文章时才可如此，否则，它们仍会带有内容。
    - **链接预览**: 现在你可以强制关闭 Telegram 消息的链接预览。
    - **来源**: 更多来源格式化选项。阅读 [格式设置指南](formatting-settings.md) 以获取详细信息。
- **部署到 Heroku**: Bot 现在可以部署到 Heroku。阅读 [部署指南](deployment-guide.md) 以获取详细信息。
- **用户权限管理**: Bot 管理员现在可以使用 `/user_info` 命令来管理 bot 用户 (用户/频道/群组) 的权限。这样管理员就可以设置谁可以使用 bot，即使禁用了多用户模式。

#### 其他新特性

- **单列表格支持**: 先前，所有 HTML 表格都被丢弃。现在，只含有单列的表格将被渲染为多行文本。请注意，多列表格仍会被丢弃。
- **适用于 [lizhi.fm](https://www.lizhi.fm) 的音频回落**: 如果高音质音频超出了文件大小限制，自动回落到更低音质的音频。仅适用于 [lizhi.fm](https://www.lizhi.fm)。

### 增强

- **Telegraph 文章美化**: Telegraph 文章的格式美化。除此之外，所有图片和视频都使用媒体中继服务器来规避防盗链。
- **非 HTTP 超链接**: Telegram 不支持非 HTTP 超链接。Bot 会自动将它们转换为裸 URL。
- **Enclosure 清理**: 如果一个附件包含非 HTTP URL 且文章中的链接已包含它，它将被移除。
- **懒惰的媒体验证器**: 媒体验证器现在是懒惰的。它只有在一篇文章可能作为 Telegram 消息发送时才会运行。这将减少 CPU 使用量和网络流量。
- **增强的图片尺寸提取**: 图片尺寸提取现在更快速和灵活。如果提取失败，bot 会尝试使用 [images.weserv.nl](https://images.weserv.nl) 来提取。
- **本地化更新**: 土耳其语 (Türkçe) 本地化文件已更新。 (英语 / English 、简体中文 、繁体中文 / 正體中文 和 粤语 / 廣東話 永远是最新的。)
- **改进的 Docker 构建缓存**: 如果依赖未改变，无需再重新拉取完整的 Docker 镜像。只需使用缓存的依赖并拉取最新的源码。
- **从 Railway.app 的环境变量中提取 git 信息**: Railway.app 上的部署现在可以识别 git 信息。
- **次要的增强**

### Bug 修复

- **Python 3.7 兼容性**: 上一个版本破坏了与 Python 3.8 的兼容性，现在已经修复了。请注意，仅支持 x86 和 amd64 架构。对于 arm64，最小的 Python 版本要求是 3.8。
- **EntitiesTooLongError**: 含有大量文本超链接的文章可引起 Telegram API 抛出这个错误。现在 bot 会尝试通过更激进的文章分割来修复这个错误。
- `<div>`: Bot 现在会确保每个 `<div>` 标签都占据一整行。
- **不必要的图片回落**: 如果至少有一张图片需要作为文件发送，bot 不再会将所有图片都回落成文件。
- **网络重试**: 增加了一个需要进行重试的异常。
- **网页解码错误**: `cchardet` 并不足够健壮以处理所有源。现在 bot 会尝试从 XML 编码声明中探测网页编码。同时，如果 `cchardet` 返回了不支持的编码，bot 会尝试使用 UTF-8 来解码网页。任何无法被解码的字符都会被替换为 `�`。
- **从 Exif 缩略图中提取图片尺寸**: 一些图片在 Exif 数据中含有缩略图。Bot 现在会避免从缩略图中提取尺寸。
- **次要的 bug 修复**

## 自定义格式、新本地化、改进的媒体回落和更多 (v2.1.0)

官方的公开 bot [@RSStT_Bot](https://t.me/RSStT_Bot) 一直使用 `dev` 分支。如果你正在使用它，你可能已经注意到新功能了。由于添加了新的命令，请使用 `/lang` 命令再一次选择你的语言，让 bot 更新你的命令列表。

### 重大变更

- 由于加入了新的自定义设置，现在需要启用 inline 模式。请到 [@BotFather](https://t.me/BotFather) ，发送 `/setinline`，选择你的 bot，并回复一个你喜欢的 inline 占位符。例如，[@RSStT_Bot](https://t.me/RSStT_Bot) 使用的是 `Please input a command to continue...`。

### 新特性

#### 亮点

- **更多自定义格式化选项**: `/set` 命令可以发挥它的全部威力了。你可以控制媒体或者任何元数据是否显示，还可以添加自定义 hashtag 和设置自定义订阅标题。但这些都需要启用 inline 模式。请阅读 [格式设置指南](formatting-settings.md) 了解格式设置的详细信息。
- **用户默认格式化设置**: 使用 `/set_default` 命令来设置你的默认格式化设置。这将应用到你的所有新订阅，如果你喜欢，你也可以让现有订阅也使用它。如果你想给大多数你的订阅应用相似的设置，这是非常有用的。
  ![img.png](resources/formatting.png)
- **新本地化**: 意大利语 (Italiano)、土耳其语 (Türkçe)、加泰罗尼亚语 (Català) 和法语 (français)。想要添加你的语言吗？请在[这里](translation-guide.md)阅读翻译指南。
- **RSS 源嗅探器**: 如果你尝试订阅一个网页而不是 RSS 源，bot 将尝试从网页中提取 RSS 源。（注意：这仅在网页中包含 RSS 源链接时有效。）
- **Enclosure 支持**: Bot 现在可以从文章的 enclosure 中提取附件。来享受听音频节目，或者下载附件吧！
- **`<audio>` 支持**: Bot 现在可以从文章中提取音频。来享受听音频节目吧！
- **长图作为文件发送**: Bot 现在可以将长图作为文件发送，防止 Telegram 将它压缩得不可读。
- **导入含自定义标题的 OPML 文件**: 你现在可以从 OPML 文件导入订阅，而不会丢失你的自定义标题。Bot 将会询问你是否应该使用 OPML 文件中的自定义标题。
- **导出含自定义标题的 OPML 文件**: 你现在可以将你的订阅导出到 OPML 文件，而不会丢失你的自定义标题。

#### 其他新特性

- **合法化更多图片格式**: Bot 现在可以判断非 JPEG 图片的合法性，并在不合法时回落到替代图片 (如果有)。
- **图片回落 (`srcset`)**: Bot 现在可以在图片不合法时回落到替代图片 (`<img srcset="...">`，如果有)。
- **pixiv 图片回落**: Bot 现在可以在 pixiv 图片不合法时回落到其他尺寸 (如果有)。 (#41)
- **为所有图片设计的图片回落**: Bot 现在会使用 images.weserv.nl 来将不合法的图片回落成对于 Telegram API 合法的图片。
- **视频回落**: Bot 现在可以在视频不合法时回落到替代视频 (`<video><source>...</video>`，如果有) 或它的封面 (`<video poster="...">`，如果有)。
- **WEBP 和 SVG 支持**: Bot 现在会使用 images.weserv.nl 来将 WEBP 和 SVG 转换成 PNG，使它们兼容于 Telegram API。
- **媒体上传器**: Bot 现在使用基本的 MTProto API 调用来上传媒体，而不是使用 telethon 提供的便捷方法。这有助于避免不必要的媒体回落和提升性能。

### 增强

- **页码**: 当命令需要分页时，bot 会显示当前页码。
- **`/unsub_all` 确认**: 当你退订所有订阅时，bot 会向你确认并发送备份。
- **取消**: 一些命令可通过点击 `取消` 按钮取消。
- **自定义监视间隔**: 你现在有了更多的监视间隔可选。如果你想的话，也可以设置任何你喜欢的监视间隔 (需要启用 inline 模式，注意 bot 管理员可以禁止普通用户设置太短的监视间隔)
- **停用原因**: 当订阅由于出错太多次而被停用时，bot 会告知原因。
- **丢弃更多图标**: 一些文章有烦人的图标，bot 现在可以检测并丢弃更多。
- **监视任务顺序随机化**: 监视任务的顺序会被随机化。
- **发生 Telegram 内部错误时重试**: 当发生 Telegram 内部错误时，bot 会重试发送消息。
- **重写的文章解析器**: 文章解析器被重写，以使其更灵活，并获得支持自定义格式的能力。
- **重写的富文本分割器**: 富文本分割器被重写，以使其更灵活，并获得支持自定义格式的能力。这同样避免了它过早地分割文本。
- **命令加速**: 一些命令现在更快了。
- **`/test` 格式化**: `/test` 命令现在会使用用户的默认格式化设置或者订阅的格式化设置 (如果已被订阅)。 (注: 只有 bot 管理员可以使用这个命令。)
- **次要的增强**

### Bug 修复

- **RSS 源标题未更新**: 当 RSS 源更新了它的标题时，bot 现在会更新在数据库里的标题并在发送消息时使用新标题。
- **内容太长**: 可能包含太长的内容的命令现在会被缩减或分页。如果还是太长，bot 会提示你。
- **太多 entity**: Bot 现在会确保消息中格式化 entity 的数量不多于 100 个 (Telegram API 限制)，否则就进行分割。这有助于避免消息丢失格式化。
- **潜在的死锁**: 一个潜在的死锁问题被修复。
- **不正确的空格和换行策略**: Bot 现在会避免在消息中出现非预期的空格和换行，特别针对怪异的 RSS 源。这同样应用到 RSS 源/文章的标题和文章作者之上。
- **次要的 bug 修复**

## 多用户、国际化、改进的用户友好性和更多 (v2.0.0)

官方的公开 bot: [@RSStT_Bot](https://t.me/RSStT_Bot)

**这是一个重大的发布。它引入了一些重大变更，因此迁移至新版本需要手动完成。**  
**更新前请务必阅读[迁移指南](migration-guide-v2.zh.md)！**

### 重大变更

- 重写用户及订阅管理。Bot 现在可以被多个用户同时使用，且各个订阅都可以独立设置监视间隔。因此，环境变量 `CHATID` 和 `DELAY` 已经被弃用且不再有效。
    - 默认情况下，bot 将作为多用户机器人运行。如果你仍然希望限制 bot 仅为你服务，请按照[迁移指南](migration-guide-v2.zh.md)进行设置。
- 不再支持 Redis，仅支持 SQLite 和 PostgreSQL。

### 新特性

#### 亮点

- **多用户**: 任何用户都可以使用 bot，也可以在频道和群组中使用（除非环境变量 `MULTIUSER` 设置为 `0`）。
- **国际化**: Bot 现在支持多语言。目前，<ins>英语 (English, en)</ins>, <ins>简体中文 (zh-Hans)</ins> 和 <ins>粤语 (廣東話, yue)</ins> 已被支持。你可以参考 [翻译指南](translation-guide.md)，通过将 bot 翻译为你的语言，为项目作出贡献。
- **用户友好**: 你可以交互式地使用大部分命令，而不需要记住他们的语法。
- **HTTP 缓存**: Bot 已经实现了 [RFC7234](https://datatracker.ietf.org/doc/html/rfc7234) 中的必要部分，以“缓存”订阅源。这可以帮助 bot 所在的服务器和订阅源所在的服务器降低负载。

#### 其他新特性

- **自定义订阅**: 订阅可被自定义。目前，只有下面列出的设置可被自定义。其他设置正在开发中。
    - **暂停订阅**: 你可以暂停订阅。这样的话，你就可以让 bot 暂停发送订阅更新。
    - **静音订阅**: 你可以静音订阅。这样的话，当 bot 发送更新时，会发送静音消息。(你仍然会收到通知，但不会有声音)
    - **监视间隔**: 你可以更改订阅的监视间隔。
- **文档**: Bot 现在有了文档。请查阅 [docs]()。

### 增强

- **更好的订阅源历史管理**: 订阅源中的所有文章都会经过散列并储存，这样你就可以订阅几乎任何订阅源而不必担心遗漏文章。
- **更好的错误处理**: Bot 现在能更好地处理错误，它将会尝试恢复并重试。
- **更好的日志**: Bot 现在能更好地记录日志。
- **更佳的性能**: Bot 现在有着更佳的性能。
- **依赖更新**: 依赖已被更新至最新版本。潜在的漏洞已被修复。
- **代理绕过**: 如果设置了环境变量 `PROXY_BYPASS_PRIVATE` ，bot 会为私有网络绕过代理。在环境变量 `PROXY_BYPASS_DOMAINS` 中列出的域名也会被绕过。
- **Bug 修复**: 修复了一些 bug。

## 修复登录的仓促发布 (v1.6.1)

**这是一个仓促的发布。它将依赖 `telethon` 升级到了最新版本。请立即升级到这个版本以免由于依赖过时而无法登录。**

机器人正在 `multiuser` 分支上被活跃开发，但尚未被合并回来，以免过早引入重大变更。如果你想要尝试多用户版本，这里有一个公开的 demo [@RSStT_Bot](https://t.me/RSStT_Bot) 。

### 新特性

- `.env` 文件支持 (仅在手动执行时支持，不支持 docker)
- 反转义受到 HTML 转义的文章标题
- 当文章内容不含有文本时，将标题作为文章的内容

### 增强

- 一些小的错误修复
- 引入了一些变通解决方案以免频繁受到泛洪控制
- 引入了一些依赖以加速 HTTP 请求

## 切换到 MTProto、OPML 支持和更多 (v1.6.0)

### 重大变更

- 与 Telegram 交互的库由使用 HTTP Bot API 的同步库 `python-telegram-bot` 改为使用 MTProto Bot API 的异步库 `telethon`
    - 这引入了 API key 的需求，程序已经内置了 7 个公开的 API key，通常情况下不应无法登入。如果无法登入，可以自己申请 API key (详见 [docker-compose.yml.sample](https://github.com/Rongronggg9/RSS-to-Telegram-Bot/blob/53f11a4739/docker-compose.yml.sample#L43) 中的说明)

### 新特性

- 由于 Telegram bot 库的替换，bot 可以直接连接到 bot 所属的 DC，不需绕经 HTTP Bot API；也不需轮询获得消息更新，它在接收及发送消息方面都更为迅速，资源占用也更低； 即使 HTTP Bot API 宕机，bot 也可以正常工作 (详见 [Advantages of MTProto over Bot API](https://docs.telethon.dev/en/latest/concepts/botapi-vs-mtproto.html#advantages-of-mtproto-over-bot-api) 和 [MTProto vs HTTP Bot API](https://github.com/LonamiWebs/Telethon/wiki/MTProto-vs-HTTP-Bot-API))
- 支持更多元素的解析
    - `<iframe>`
    - `<video><source><source>...</video>`
    - `<code>`
    - `<pre>`
- 支持 OPML 导入导出
- 支持超长文章通过 Telegraph 发送 (必须先设置 `TELEGRAPH_TOKEN` 环境变量)
- 支持使用 redis 作为数据库
    - 注意：这是为了在 [railway.app]() 上部署而设计的变通解决方案，未来很可能丢弃
- 支持 arm64 (docker 构建)
- 支持在由于 Telegram 服务器不稳定或 Telegram 服务器与媒体服务器之间的网络连接不稳定而导致 Telegram 无法发出带有媒体的消息时，使用媒体反代服务器重新发送。
- 支持日志着色
- `docker-compose.yml.sample`
- 用于检查 bot 版本的 `/version` 命令
- 如果设置了全局代理 (环境变量 `SOCKS_PROXY`/`HTTP_PROXY`)，会使用它们

### 增强

- 将 feed 监视任务分配到每分钟，而不是每次 `DELAY` 一次性全部执行
    - 因此，环境变量 `DELAY` 将只能被设置为 60~3600
    - 注意：环境变量 `DELAY` 未来将被弃用
- 使用 `guid`/`id` 来辨识一个 post，而不是 `link`
- 简化了 `/list` 的输出
- 升级为 Python 3.9 (docker 构建)
- 次要的修复

## 完全重写的文章解码 (v1.5.0)

- **文章解码完全重写，更加稳定及更加忠实还原原有格式**
    - **针对大量短动态类 RSS 源进行了测试**
    - **即使是长文 RSS 源，也可以正确处理**
- **支持 GIF**
- **消息多于 10 张媒体时支持分条发送**
- **支持视频与图片任意混合于同一条消息**
- 超限媒体不再直接丢弃，而是作为链接附加到消息末尾
- 自动判断 RSS 源的标题是否为自动填充，并自动选择是否略去标题
- 自动显示作者名
- 自动替换 emoji shortcodes 为 emoji
- 自动替换满足某些特征的表情图片为 emoji 或其描述文本
- 因 telegram api 不稳定而无法发出图片时，自动更换图床服务器重发
    - 仅限微博图源，非微博图源自动将所有媒体转为链接附加到消息末尾
- 改进文本长度计数方式，不再因为链接 url 过长而导致消息被提前分割
- 更改 user-agent，规避某些网站屏蔽 requests UA 的问题
- 改进的日志记录

## 初始发布 (v1.0.0)

第一个公开发布