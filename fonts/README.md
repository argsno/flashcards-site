# 拼音字体

SIL Andika 7.000（https://software.sil.org/andika/）的子集，SIL Open Font License 1.1，见 OFL.txt。

- 由 `npm run build:fonts -- --src <Andika 包解压目录>` 生成，**不要手工改**。
- 只保留拼音需要的码位（见 scripts/build-fonts.mjs 的 SUBSET_RANGES），每档约 22KB。
- 主名改为 MaimaiPinyin：OFL 1.1 第 3 条禁止修改版使用保留字体名（Andika / SIL），子集属修改版。
- H5 由 Vite publicDir 原样打进产物（`/fonts/…`）；weapp 不打包，走 `wx.loadFontFace` 取同一地址。
