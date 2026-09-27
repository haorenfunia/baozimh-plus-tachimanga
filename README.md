# baozimh-plus-tachimanga
包子漫画 Plus 的 Tachimanga 扩展仓库


## Mihon (Android) 使用

> 要求 **Mihon v0.20.0+**（对扩展 lib 1.6 的支持自该版本起）。

在 Mihon 中添加扩展仓库：`更多 → 设置 → 浏览 → 扩展存储 → 添加`，粘贴以下任一地址：

- **jsDelivr CDN（国内直连推荐）**
  ```
  https://cdn.jsdelivr.net/gh/haorenfunia/baozimh-plus-tachimanga@main/mihon-store/index.min.json
  ```
- **GitHub Raw（需代理）**
  ```
  https://raw.githubusercontent.com/haorenfunia/baozimh-plus-tachimanga/main/mihon-store/index.min.json
  ```

添加后到 `浏览 → 扩展` 刷新并安装「包子漫画 Plus」。扩展签名指纹已内置在
`mihon-store/repo.json`，安装后**自动信任**，无需手动确认。

### 目录说明（Mihon 相关）

```
mihon-store/
├── index.min.json   # legacy JSON 数组引导文件（Mihon 要求首字节为 '['）
├── repo.json        # meta + APK 签名指纹 + index_v2 指针（锁定 commit SHA）
├── index.v2.json    # tachiyomix 新格式仓库索引（绝对 APK/图标地址，走 jsDelivr）
└── icon/            # legacy 备用路径图标
```

根目录的 `index.json` / `index.min.json` / `index.pb` / `apk/` / `jar/` 仍归
Tachimanga (iOS) 使用，两套互不影响。

### 发布新版本时

1. 新 APK 放 `apk/`、jar 放 `jar/`（Tachimanga 用）
2. 更新根目录 `index.json` / `index.min.json` / `index.pb`
3. 同步更新 `mihon-store/index.min.json` 和 `mihon-store/index.v2.json`
   （code / version / apkUrl）
4. 提交后取该 commit SHA，更新 `mihon-store/repo.json` 里 `index_v2` 的
   `@<SHA>`（jsDelivr 对 SHA 路径即时生效，无缓存问题）
5. 如走 jsDelivr，可再手动刷一次 `@main` 引导文件缓存：
   `https://purge.jsdelivr.net/gh/haorenfunia/baozimh-plus-tachimanga@main/mihon-store/index.min.json`
