---
title: "使用 Hugo 自建部落格"
date: 2025-03-03T10:25:00+08:00
draft: false
tags: ["Hugo"]
keywords: ["Hugo"] #SEO用
categories: ["其他技術"]
summary: "此篇內容為 使用 Hugo 自建部落格的流程測試筆記" #文章總頁顯示用
description: "此篇內容為 使用 Hugo 自建部落格的流程測試筆記" #SEO用
toc: true
comments: true
thumbnail: "/images/logo.png" #文章總頁顯示圖片
shareImage: ""
---

## 香蕉在哪裡

> 有香蕉才有動力，有痛點或目標才會開始想做些甚麼。
>
> 阿猩期許自己今年能定期的做技術測試並寫下紀錄，起初是只想到開始思考要如何更方便的撰寫文章，且不要花太多時間維護。
> 後來找到 **Hugo** ，既可以自己架站，也可以不用花太多時間重頭造輪子。
>
> 測試完的心得，如果完全沒有程式背景，只是想要寫寫文章，**Hugo** 的門檻還是稍微高了一點。
> 從零開始建立部落格的過程，是一個蠻有趣的經驗，如果本身已有指令操作介面(如 cmd)、git、Markdown 等經驗，時做起來會順手很多。

## 開始使用 Hugo 建立部落格

1. 至 [Hugo Repo](https://github.com/gohugoio/hugo/releases) 下載 Windows 版本的 Hugo

   - 下載 hugo\_**extended**\_xxxx_windows-amd64.zip

2. 解壓縮後，進入該路徑並查詢版本，例如

   ```cmd
    cd D:\部落格專區\hugo_extended_0.145.0_windows-amd64
    hugo version
   ```

3. 將解壓縮的路徑，加入 Path 環境變數(使用者變數、系統變數都要加)。
4. 建立 Hugo 專案，並指定專案名稱，例如

   ```cmd
    cd D:\部落格專區
    hugo new site my-blog
   ```

5. 加入部落格樣式：至 [Hugo Themes](https://themes.gohugo.io/) 找到喜歡的格式，按下 Download 會進入該樣式 Repo，最後再 Clone 至 你的部落格專案/themes，例如：

   ```cmd
    cd D:\部落格專區\my-blog\themes
    git clone https://github.com/CaiJimmy/hugo-theme-stack.git
   ```

6. /在/content/post/helloworld 下新增 index.md 檔案，內容為:

   ```md
        ---
        title: "Hello World"
        date: 2023-03-25T17:00:00+08:00
        draft: false
        ---

        我的第一篇文章
   ```

## 參數設定測試

> 如果只是想寫網址，完全不想管樣式的話，做完上面步驟其實就可以了。
> 但阿猩想，既然 Hugo 都做成這樣的工具了，總會提供一些比較客製化的調整吧。
> 找了一下還真的有，這節就來測試一下參數吧。

[Hugo 樣式 Repo](https://themes.gohugo.io/themes/hugo-clarity/) 內會提供參數設定的項目概要，分為 Global 與 Page 參數，雖然沒說明細節設定，但有提供型別，以及說明 Page 設定，是否能覆蓋 Global 設定。
測試一下大致可行。全域設定要調整 **hugo.toml**，例如:

```md
    baseURL = "基本網址"
    languageCode = "zh-tw" #語系
    title = "瀏覽器分頁、Footer 顯示的名稱"
    theme = "部落格樣式 Repo"

    [params]

    # 畫面設定
    # introDescription = "網站介紹文字"
    logo = "logo 檔案路徑" #Ex: "/images/logo.png"
    iconsDir = "/images/" #預設會抓該目錄底下的 favicon-32x32.png
    footerLogo = "footerLogo 檔案路徑" #Ex: "/images/favicon.ico"
    dateFormat = "2006-01-02"

    # 網頁 SEO 用
    author = "作者"
    description = "網站描述"
    keywords = ["關鍵字1", "關鍵字2"....]

    # 網誌設定用
    numberOfTagsShown = 15       # 顯示 Tag 數
    mobileNavigation = "right"   # 手機 nav 顯示在哪側
    figurePositionShow = true
    figurePositionLabel = "圖"   # 圖片前贅字

    comments = true              # 是否啟用回應
    enableSearch = true          # 是否啟用全站搜尋
    showShare = true             # 是否啟用分享

    numberOfRecentPosts = 8      # 最新文章顯示筆數
```

如果要新增 nav 的選項，可在 **hugo.toml** 自行調整並加入下列內容:

```MD
    [[menu.main]]
    name = "首頁"
    url = "/"
    weight = 1

    [[menu.main]]
    name = "文章"
    url = "/posts/"
    weight = 2

    [[menu.main]]
    name = "關於我"
    url = "/about/"
    weight = 3
```

要設定 Page 的話，跟 Global 大同小異，大同小異，就自行研究啦。

## MarkDown 說明

> 阿猩之前已有做過 MarkDown 的研究了，想進一步練習的就自行研究吧 [阿猩的 MarkDown 測試](https://dotblogs.com.tw/supergary/Series?Qq=Markdown)

## 待測試

- 分享複製時，顯示的圖片
- 目前 MD 的排版有點太擠，日後再測看看，如何做到套用部分文章樣式
