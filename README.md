# YouTube Thumbnail Preview — Immersive Player

A community-maintained derivative of [YouTube Thumbnail Preview — Clean Popup Player](https://github.com/Startanuki07/YouTube-Thumbnail-Preview-Clean-Popup-Player) by **Star_tanuki07**. This project retains upstream attribution and the MIT license; it does not claim the upstream work as wholly original.

> Unofficial community project. Not affiliated with or endorsed by YouTube or Google.

## Preview screenshots

Add your own screenshots to `docs/screenshots/` and replace these placeholders with Markdown image links.

<!-- SCREENSHOTS: replace the placeholders below when screenshots are ready -->

| Thumbnail controls | Immersive player |
|---|---|
| _Screenshot placeholder: `docs/screenshots/thumbnail-buttons.png`_ | _Screenshot placeholder: `docs/screenshots/immersive-player.png`_ |

| Player controls close-up | Comments and translation |
|---|---|
| _Screenshot placeholder: `docs/screenshots/player-controls.png`_ | _Screenshot placeholder: `docs/screenshots/comments-translation.png`_ |

## Features

- Adds convenient preview and comment controls to supported YouTube thumbnails.
- Opens a cleaner immersive popup player and attempts to prewarm the actual video silently while a thumbnail is hovered; the warmed iframe is reused when playback is opened.
- **Max quality shortcut:** the `Max` button in the popup player's upper-left controls automatically selects the highest quality currently available for the video.
- **Long-press speed control:** holding an arrow key activates 3× playback speed, rather than repeatedly seeking in 5-second increments. This is a script-specific behavior, not an official YouTube feature.
- **Exit the popup:** press `Esc`, or click the blank area between the video surface and the browser edge.
- Retains useful player interactions such as fullscreen, quality controls, and keyboard shortcuts.
- Provides comment browsing, filtering, paging, and optional translation. Comments require a user-supplied YouTube Data API v3 key.
- Uses SponsorBlock segment data where supported by the script.

### UI refinement in this derivative

In the immersive popup, **the four UI buttons originally positioned on the right side of the player have been moved to the upper-left corner**. Their styling is intentionally subtle and translucent where possible, helping them blend into the video background and reducing distraction from the content. The `Max` button automatically chooses the highest quality currently available for the video.

### Known issue: homepage thumbnail preview can restart

When the mouse remains over a recommended video thumbnail on the YouTube homepage, YouTube's own preview may restart from the beginning within roughly two seconds. The homepage preview and this script's hidden-player preloading can conflict. **The current build prioritizes preloading the actual player for faster popup playback**, so the brief/restarting native thumbnail preview is a known trade-off, not a claim that both behaviors work perfectly together. This behavior may vary with YouTube's page implementation.

## Installation

1. Install a compatible userscript manager, such as [Tampermonkey](https://www.tampermonkey.net/) or [Violentmonkey](https://violentmonkey.github.io/).
2. Open the userscript file in this repository.
3. Follow the manager's installation flow. Review the source and requested permissions before installing.
4. Visit YouTube and hover over a supported thumbnail to find the added controls.

## YouTube Data API key (comments)

The comment panel uses Google's official YouTube Data API v3. Enable the API in [Google Cloud Console](https://console.cloud.google.com/), create an API key, then enter it in the script's API-key prompt.

- The key is stored in your local userscript-manager profile using its value-storage API. The script does not upload it to this GitHub project.
- When comments are requested, the key is sent to Google's `youtube/v3/commentThreads` endpoint as part of the API request. Google receives the key and query parameters.
- Userscript-manager storage should not be considered an encrypted secrets vault. Software or extensions with sufficient access to the browser profile may potentially access stored values.
- Restrict the key in Google Cloud Console where practical, monitor quota/usage, and never post it in public issues, screenshots, commits, or logs.
- The script's API-key dialog can clear the locally stored key. If a key may have leaked, revoke or rotate it in Google Cloud Console too; deleting it locally does not revoke it remotely.
- The thumbnail/player features do not require a YouTube Data API key if you do not use comments.

## Privacy and network behavior

Based on inspection of the published source, relevant features may contact:

| Service | Purpose |
|---|---|
| YouTube and YouTube's embedded player/video hosts | Video playback and player resources |
| Google YouTube Data API v3 (`googleapis.com`) | Fetch comments when requested; the user's API key is included |
| Google Translate (`translate.googleapis.com`) | Translate comment text when a translation language is selected; comment text is sent for processing |
| SponsorBlock API (`sponsor.ajay.app`) | Retrieve segment data used by SponsorBlock-related behavior |

The script also adds resource hints for YouTube-related hosts. Actual requests depend on the page and features used.

**Limitations:** This table summarizes endpoints identified during source inspection; it is not a guarantee that the browser, userscript manager, YouTube, or future versions make no other network requests. No independent security audit or formal privacy certification is claimed. Review the source and browser network activity if you need a stricter audit.

## Attribution and license

- Upstream project and author: **Star_tanuki07**, [YouTube Thumbnail Preview — Clean Popup Player](https://github.com/Startanuki07/YouTube-Thumbnail-Preview-Clean-Popup-Player).
- The upstream code is used under the **MIT License**. Its copyright and license notice are retained in [LICENSE](./LICENSE).
- SponsorBlock segment data is identified in the script as licensed under **CC BY-NC-SA 4.0**. See the [SponsorBlock API documentation](https://wiki.sponsor.ajay.app/w/API_Docs) and [license text](https://creativecommons.org/licenses/by-nc-sa/4.0/).
- YouTube and Google are trademarks of their respective owners. This is an unofficial derivative and is not endorsed by them.

Open source means making provenance and changes visible. Please preserve attribution and license notices when redistributing.

## 简体中文

这是基于 **[Star_tanuki07 的 YouTube Thumbnail Preview — Clean Popup Player](https://github.com/Startanuki07/YouTube-Thumbnail-Preview-Clean-Popup-Player)** 二次开发的用户脚本。上游代码采用 MIT 许可证；本项目保留原作者署名和许可证，不会将上游工作冒称为原创。

### 功能

- 在 YouTube 视频缩略图上添加预览和评论入口。
- 打开更干净的沉浸式悬浮播放器；鼠标悬停缩略图时尝试静音预热实际视频，并在打开播放器时复用该 iframe，以减少等待。
- **Max 最高画质按钮**：点击悬浮播放器左上角的 `Max`，自动选择当前视频可用的最高画质。
- **长按方向键倍速**：按住方向键可启动 3 倍速播放，而不是反复按官方常见的 5 秒步进进行快进/快退。这是脚本提供的行为，并非 YouTube 官方功能。
- **退出悬浮播放器**：按 `Esc`，或点击视频画面与浏览器边框之间的留白区域。
- 保留全屏、画质控制及部分键盘快捷操作。
- 支持评论浏览、筛选、分页和可选翻译。评论功能需要用户自行提供 YouTube Data API v3 密钥。
- 在脚本支持的场景下使用 SponsorBlock 片段数据。

### 我们做的界面调整

在沉浸式悬浮播放器中，**原本位于播放器右侧的 4 个 UI 按钮被移动到了左上角**。按钮样式尽量克制、半透明，让它们尽可能融入视频背景，减少对画面内容的遮挡和干扰。左上角的 `Max` 按钮可以自动选择当前视频可用的最高画质。

### 已知问题：首页缩略图预览可能从头重播

鼠标悬停在 YouTube 首页推荐视频封面上时，YouTube 自带的预览视频可能在约 2 秒内从头重播。首页原生预览与脚本的隐藏播放器预加载存在冲突。**当前版本优先保证实际播放页的预加载与悬浮播放器快速起播**，因此暂时接受首页原生预览可能很短或重新开始这一取舍；这不是两个功能都已完美兼容的承诺。具体表现可能随 YouTube 页面实现变化。

### 安装方法

1. 安装兼容的用户脚本管理器，例如 [Tampermonkey](https://www.tampermonkey.net/) 或 [Violentmonkey](https://violentmonkey.github.io/)。
2. 打开仓库中的用户脚本文件。
3. 按脚本管理器提示安装。安装前建议查看源码和权限。
4. 打开 YouTube，将鼠标悬停在支持的缩略图上，查看新增控件。

### API 密钥、隐私与安全

- 评论功能使用 Google 官方 YouTube Data API v3。密钥通过用户脚本管理器的 `GM_setValue / GM_getValue` 存储在本机浏览器配置中；脚本不会把密钥上传到本 GitHub 项目。
- 请求评论时，密钥会发送给 Google 的 `youtube/v3/commentThreads` API。Google 会收到密钥和相应查询参数。
- 用户脚本管理器的本地存储不应被视为加密保险库；拥有足够权限的程序或扩展可能访问浏览器配置中的保存值。
- 建议在 Google Cloud Console 中尽可能限制 API 密钥、监控配额，并避免将密钥放进公开 issue、截图、提交记录或日志。
- 可以在脚本的 API 密钥对话框中清除本地密钥。若怀疑泄露，还应前往 Google Cloud Console 撤销或轮换；仅在本地删除不会让 Google 端的密钥失效。
- 评论翻译会将评论文本发送至 Google Translate 的 `translate.googleapis.com`；SponsorBlock 功能会请求 `sponsor.ajay.app`；视频播放本身会访问 YouTube 相关服务。

以上说明依据当前公开源码中识别到的请求端点整理，不构成“绝对安全”保证，也不代表经过独立安全审计。具体网络行为还会受到 YouTube、浏览器、脚本管理器及未来版本影响；如需严格确认，请自行审阅源码和浏览器网络记录。

### 致谢与开源

- 原始项目及作者：**Star_tanuki07** — [上游 GitHub 仓库](https://github.com/Startanuki07/YouTube-Thumbnail-Preview-Clean-Popup-Player)。
- 上游代码依据 **MIT License** 使用；本仓库保留原作者版权声明及许可证，详见 [LICENSE](./LICENSE)。
- SponsorBlock 数据依据 **CC BY-NC-SA 4.0** 许可，并在脚本中保留相应署名与说明，见 [SponsorBlock API 文档](https://wiki.sponsor.ajay.app/w/API_Docs)。
- 本项目为非官方衍生项目，与 YouTube / Google 无隶属或背书关系。

欢迎审阅、反馈和改进。转载或再分发时，请保留许可证、版权和来源说明。

## Contributing and security

Bug reports and reproducible improvements are welcome. Do not post API keys or private information in public issues. See [SECURITY.md](./SECURITY.md).
