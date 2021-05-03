---
layout: post
title: "筆記 | 一點小更新: Tag Page & RSS"
author: "Andrea Shih"
categories: journal
tags: [notes]
image: table.jpg
---

今天 (~~因為不想寫計算語言學作業~~) 更新了 blog 的 [tag page](https://andreashih.github.io/blog/menu/tags.html)，還有打開 [RSS](https://andreashih.github.io/blog/rss-feed.xml)，在此做些紀錄。

&nbsp;

### Tag Page
---
隨著文章越來越多，分類就更顯重要。我用的這個 jekyll 模板本來就可以在各篇文章加入 tags，但是沒有一個獨立的 tag page，所以打算自己幫它加一個。我參考的是[這篇文章](https://nk910216.github.io/2017/08/11/UsingTagsForJekyll/)的 code，只改了 css 讓按鈕變成我喜歡的顏色，顏色是在 [NIPPON COLORS](https://nipponcolors.com/) 挑的。

原本在本機一切順利，但是 push 上去卻發現我的 tags 按鈕不能顯示顏色。後來找到[解決方法](https://stackoverflow.com/questions/49743535/jekyll-static-page-css-not-rendering)才終於成功！

&nbsp;

### RSS Feed
---
其實我一直都知道這個模板可以用 RSS feed，但就是沒有把它打開，因為不知道可以幹嘛XD

直到最近才發現 RSS 其實蠻好用的。[RSS](https://zh.wikipedia.org/wiki/RSS) 的全名是 Really Simple Syndication，可以讓你訂閱喜歡的 blog、podcast，甚至是 YouTube 頻道。當訂閱的網站有更新，就可以獲得通知。再也不用一個一個加到我的最愛，最後因為懶得點開看有沒有更新而遺忘他們的存在。

> **要怎麼開始呢？**

很多 blog 的頁面上都找得到 RSS 的 icon (長得很像 wifi 圖示)，點進去之後會出現一堆亂七八糟的文字，請不要害怕，複製最上方的網址就對了。如果沒有 RSS 圖示的話，按右鍵然後點選 View page source 通常也找得到，只是要 ctrl+F 搜一下 RSS 網址在哪裡。

> **連結複製好了，然後呢？**

現在有許多管理 RSS 的平台，最多人使用的應該屬 [Feedly](https://feedly.com/)，操作簡單直覺，只要把複製好的網址貼上去就可以。除此之外還提供關鍵字搜尋以及群組功能，且在各作業系統都能使用。Mac 或 Linux 使用者可以試試 [Newsboat](https://newsboat.org/)，感覺也蠻方便的，但是 Windows 或 WSL 都不能用QQ

&nbsp;

以上就是這次 blog 的小更新，也歡迎大家用 RSS 訂閱這個 blog！雖然我更新很慢，草稿資料夾躺了一堆 md files 最後都沒繼續寫 (慚愧) 最近想寫讀書心得，但願我有空......

&nbsp;

Photo by <a href="https://unsplash.com/@krisatomic?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Kris Atomic</a> on <a href="https://unsplash.com/s/photos/cafe?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
  