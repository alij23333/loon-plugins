# 网易云音乐 Loon 去广告插件

基于网易云音乐 9.6.05（2026-10-19）实测抓包整理的 Loon 插件，纯本地规则，不依赖远程脚本。

## 插件

| 插件 | 适合 | 导入链接 |
| --- | --- | --- |
| **纯听歌版** `NeteaseMusicPure.plugin` | 只用来听歌，其他功能都不要 | `https://raw.githubusercontent.com/alij23333/netease-music-loon/main/NeteaseMusicPure.plugin` |
| 去广告版 `NeteaseMusicAdBlock.plugin` | 只去广告和推广位，保留云贝、动态等功能 | `https://raw.githubusercontent.com/alij23333/netease-music-loon/main/NeteaseMusicAdBlock.plugin` |

两个插件选一个启用即可，不要同时开。

### 纯听歌版拦截内容

- 开屏广告（包括实时下发和预下载）、信息流广告、广告监测
- 推广位、弹窗、气泡、红点、侧边栏推广
- 云贝、积分、商城、打榜助力
- 动态、笔记、直播、演出、一起听
- 会员营销页面（开通按钮、续费价格、优惠弹窗）
- 搜索热词、评论区推广
- 数据上报、升级提示

保留播放、歌单、搜索、每日推荐、歌词、评论和收藏，会员身份与音质不受影响。

## 导入方法

1. 打开 Loon，进入「配置」→「插件」，点「+」，粘贴上面的导入链接。
2. 在「配置」→「MITM」里开启 MITM，生成并安装证书。
3. 到 iPhone 的「设置」→「通用」→「关于本机」→「证书信任设置」，打开 Loon 证书的完全信任开关。

## 注意

- **开屏广告会预下载**：App 会在 WiFi 下提前缓存好几天的开屏广告。开启插件后，已缓存的广告可能还会出现几天，想立刻清空就删除网易云再重装。
- **QUIC 必须拦**：插件已内置这条规则。QUIC 流量无法被 MITM，不拦的话路径规则会全部失效。
- **有些推广拦不掉**：`/eapi/batch` 等接口把多个请求打包在加密请求体里，Loon 无法按内容区分。
- 规则来自安卓端抓包，iOS 端接口大体一致；如果遇到页面异常，可以提 Issue。

## 致谢

部分推广位规则参考了 [Thelongdarkorg/loon-plugins](https://github.com/Thelongdarkorg/loon-plugins)。
