# 拼音课表录音

`src/public/audio/pinyin/*.mp3`：拼音卡片（学习流里的 `pinyin:<课 id>` 条目）的发音录音，92 条。

文件名是 **ASCII 音频 id**（`a1`、`zh`、`yi`），不是带调字形——macOS 的 NFD 分解会让
「ā.mp3」在真机上取不到。id ↔ 字形的映射在 `src/pinyin/content.ts`，
URL 由 `src/utils/pinyinAudio.ts` 拼（H5 同源相对路径，weapp 走 `CLOUD_HOST`）。

## 来源与许可

- 原始录音：[davinfifield/mp3-chinese-pinyin-sound](https://github.com/davinfifield/mp3-chinese-pinyin-sound)，
  **Unlicense（公有领域）**，可商用、可修改、无需署名。本目录 `LICENSE.txt` 为原仓库许可原文。
- 生成命令（可复现）：
  ```bash
  git clone --depth 1 https://github.com/davinfifield/mp3-chinese-pinyin-sound /tmp/dav
  npm run build:pinyin-audio -- --src /tmp/dav
  ```
- 取法（都是为了同一个录音者，避免音色跳）：
  - **声母**：呼读音音节（`b`←`bo`、`zh`←`zhi`），只取第一声；
  - **韵母**：零声母音节（`i`←`yi`、`ui`←`wei`、`ie`←`ye`），四声各取一条；
  - **仓库没有的三个**：`o`←`wo`、`eng`←`weng`、`ong`←`yong`，剪掉开头 35ms 滑音后取元音段。
- 统一处理：`loudnorm=I=-16:TP=-1.5:LRA=7`、单声道 44.1kHz、96kbps、首尾各 15ms 淡入淡出。

## 已知局限

- 源录音首尾被切齐，声母辅音偏轻；练习是「看字母自己读、家长判会/不会」，不考辨音差异。
- `o`/`eng`/`ong` 由滑音音节剪出，起点比自然发音略硬，真机上需要人耳复核（换真人录音时保持 id 不变即可）。
- 不做轻声音（产品决定）。
