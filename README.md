# Loon 去广告插件

基于实测抓包整理的 Loon 插件，纯本地规则，不依赖远程脚本。每条规则都在真机流量上回放验证过。

## 插件列表

| App | 插件 | 适合 | 导入链接 |
| --- | --- | --- | --- |
| 网易云音乐 | **纯听歌版** `NeteaseMusicPure.plugin` | 只用来听歌，其他功能都不要 | `https://raw.githubusercontent.com/alij23333/loon-plugins/main/NeteaseMusicPure.plugin` |
| 网易云音乐 | 去广告版 `NeteaseMusicAdBlock.plugin` | 只去广告和推广位，保留云贝、动态等功能 | `https://raw.githubusercontent.com/alij23333/loon-plugins/main/NeteaseMusicAdBlock.plugin` |
| 知乎 | `ZhihuAdBlock.plugin` | 去广告并精简界面 | `https://raw.githubusercontent.com/alij23333/loon-plugins/main/ZhihuAdBlock.plugin` |

网易云的两个插件选一个启用即可，不要同时开。

## 导入方法

1. 打开 Loon，进入「配置」→「插件」，点「+」，粘贴上面的导入链接。
2. 在「配置」→「MITM」里开启 MITM，生成并安装证书。
3. 到 iPhone 的「设置」→「通用」→「关于本机」→「证书信任设置」，打开 Loon 证书的完全信任开关。

## 网易云音乐

基于网易云音乐 9.6.05（2026-10-19）抓包。

**纯听歌版**拦截：开屏（实时 + 预下载）与信息流广告、推广位与弹窗、云贝 / 积分 / 商城 / 打榜、动态 / 笔记 / 直播 / 演出、会员营销页面、搜索热词、数据上报。保留播放、歌单、搜索、每日推荐、歌词、评论和收藏，会员身份与音质不受影响。

**去广告版**只拦广告接口和推广位，刻意不拦 `ad/listening`（云贝中心）和 `ad/power`（打榜助力）。

注意：
- 新版大量接口迁到了 `/xeapi/`，规则同时覆盖 `/eapi`、`/xeapi`、`/weapi`、`/api`。
- 第三方开屏素材改由阿里 CDN 和普通封面 CDN 下发，只靠域名屏蔽拦不住，必须拦接口。
- `/eapi/batch` 把多个接口打包在加密请求体里，Loon 无法按内容区分，这部分推广拦不掉。

## 知乎

基于知乎 11.10.0（2026-10-19）抓包。

拦截内容：
- 开屏（预下载 `launch_v2`、实时 `real_time_launch_v2`，以及兜底的穿山甲、优量汇 SDK）
- 首页顶部横幅、浮层视频、话题推广气泡、回答 / 文章底部广告、广告上报
- 点开回答后下滑出现的回答流（整体去掉）
- 关注动态、搜索「猜你想搜」、搜索框轮播词里的商业条目（只删广告条目）
- 首页顶部标签只留关注 / 推荐 / 热榜；搜索去掉小说、论文、知识标签
- 回答页悬浮搜索词、相关搜索、圈子卡片（保留热评预览）；评论区「大家在讨论」
- 我的页面盐选续费卡和会员入口；直答「看山」推荐气泡

## 通用注意事项

- **QUIC 必须拦**：插件已内置。QUIC 流量无法被 MITM，不拦的话路径规则会全部失效。
- **开屏广告会预下载**：App 会在 WiFi 下提前缓存好几天的开屏广告，开启插件后已缓存的可能还会出现几天。想立刻清空就删除 App 重装，重装后先确认 Loon 插件已开启再打开 App。
- 规则来自安卓端抓包，iOS 端接口大体一致；遇到页面异常可以提 Issue。

## 致谢

部分规则参考了 [Thelongdarkorg/loon-plugins](https://github.com/Thelongdarkorg/loon-plugins)。
