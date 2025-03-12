# BiliSearchPlugin 使用说明

<img src="https://github.com/user-attachments/assets/a2627960-69d8-400d-903c-309dbeadf125" width="400" height="600">
## 一、插件概述

BiliSearchPlugin 是一个用于搜索 B 站视频并提供播放链接的插件。用户可以通过关键词搜索 B 站视频，选择感兴趣的视频后查看剧集列表，并播放指定的剧集。该插件支持在聊天场景中与用户进行交互，为用户提供便捷的视频搜索和播放服务。

## 二、功能特性

- **🎬 视频搜索：** 用户输入关键词，插件会在 B 站搜索相关视频，并以列表形式展示搜索结果。
- **📚 剧集查看：** 用户选择视频后，插件会获取该视频的剧集列表，并展示给用户。
- **▶️ 视频播放：** 用户选择具体剧集后，插件会提供该剧集的播放链接，以卡片消息形式发送。
- **✨ 交互友好：** 使用 Emoji 美化输出信息，提供清晰的操作提示，增强用户体验。
- **💬 贴心提示：** 提供 "点开后用浏览器观看哦" 和 "温馨提示：需要等待5秒再点击哦" 等温馨提示。

## 三、安装与配置

1.  **安装依赖**

    确保你的 Python 环境中已经安装了以下依赖库：

    ```bash
    pip install aiohttp loguru filetype Pillow beautifulsoup4
    ```

2.  **配置文件**

    在 `plugins/BiliSearchPlugin` 目录下创建 `config.toml` 文件，并进行如下配置：

    ```toml
    [BiliSearchPlugin]
    enable = true
    commands = ["B站"]
    api_url = "https://www.hhlqilongzhu.cn/api/sp_jx/bilbil/api.php"
    play_command = "视频 "
    ```

    配置项说明：

    -   `enable`：是否启用该插件，`true` 为启用，`false` 为禁用。
    -   `commands`：触发视频搜索的命令列表，用户输入以该命令开头的消息时，插件会进行视频搜索。
    -   `api_url`：用于搜索视频的 API 地址，请替换为实际可用的 API 地址。
    -   `play_command`：选择视频的命令前缀，用户输入以该命令开头并跟上视频序号时，插件会处理该选择。

## 四、使用方法

1.  **搜索视频**

    在聊天中输入以 `commands` 配置项中的命令开头的消息，并跟上要搜索的关键词，例如：

    ```plaintext
    B站 网球王子
    ```

    插件会返回相关视频的列表，每个视频前会有对应的序号和 Emoji 标识，同时提供操作提示：

    ```plaintext
    🎬———B站视频———🎬
    1️⃣. 新网球王子 U-17世界杯半决赛🎾
    2️⃣. 新网球王子 U-17世界杯🎾
    ...
    _________________________
    🎵输入 “视频+序号” 选择视频🎵
    ```

2.  **选择视频**

    用户输入以 `play_command` 配置项中的命令开头并跟上视频序号的消息，例如：

    ```plaintext
    视频 1
    ```

    插件会获取该视频的剧集列表，并展示给用户：

    ```plaintext
    🎬———网球王子剧场版：英国式庭球城决战 ———🎬
    1️⃣. 第1集
    _________________________
    🎵输入 “序号 + 数字” 选择剧集🎵
    ```

3.  **选择剧集**

    用户输入以 “序号” 开头并跟上剧集序号的消息，例如：

    ```plaintext
    序号 1
    ```

    插件会提供该剧集的播放链接，并以美化后的卡片消息形式展示：

    ```
    [卡片消息示例]
    🎉网球王子剧场版：英国式庭球城决战 - 第1集🎉
    点开后用浏览器观看哦 🎥
    温馨提示：需要等待5秒再点击哦
    视频简介（如果有）
    [缩略图]
    ```

## 五、错误处理

-   如果未找到相关视频，插件会回复 “未找到相关视频。”
-   如果输入的视频编号或剧集编号无效，插件会回复相应的错误提示，如 “无效的视频编号。” 或 “无效的剧集编号。”
-   如果无法获取视频的剧集信息或播放链接，插件会回复相应的错误提示，如 “无法获取该视频的剧集信息。” 或 “无法获取该集视频链接或该视频没有播放资源。”

## 六、注意事项

-   请确保 `api_url` 配置项中的 API 地址是可用的，否则可能无法正常搜索视频。
-   该插件依赖于外部 API 提供视频搜索和播放链接，若 API 出现问题，可能会影响插件的正常使用。
-   插件的交互命令和提示信息可根据 `config.toml` 文件中的配置进行调整。
-   请确保已经安装了 `beautifulsoup4` 库，如果需要使用网页抓取功能。 （当前代码已移除此依赖，仅在需要抓取网页信息时才需要）

-   ![微信图片_20250223235609](https://github.com/user-attachments/assets/6cc415fd-05f3-4b1c-80fb-4796ea6391a2)

