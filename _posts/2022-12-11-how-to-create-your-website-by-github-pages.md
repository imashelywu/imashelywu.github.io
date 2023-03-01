---
toc: true
toc_label: "My Table of Contents"
toc_icon: "cog"
---

一直以來都想建立個人網站，一方面面試時方便呈現自己的能力，一方面也是因為自己記憶力太差，本來打算用wordpress，但對我來說門檻還是有高，後來才發現GitHub Page，建立相當簡單，而且看起來有自己的網域，因此記錄一下步驟供自己和有需要的人參考。

<!-- <aside> -->
💡 本篇對象為已有 git 基礎，但對架設 GitHub Page 網站一竅不通的人


<!-- </aside> -->


# 如何建立自己的網站?

1. 登入GitHub帳號並新增repository
    
    如下圖，Repository 命名規則為`{user_name}.github.io`，過一段時間應該就可以看到自己的 page了
    ![Example](/assets/images/2022-12-11/Untitled.png)
    <!-- <img src="{{site.baseurl | prepend: site.url}}_posts/Untitled.png" alt="zigzag" /> -->
    
2. 新增 index.html
    
    我自己是將GitHub的 repo clone 到本地端再新增檔案，index.html 最簡單可以新增下面的內容，可以參考 html 語法
    
    ```html
    <html>
      <head>
        <meta charset="utf-8">
        <title>Hello，GitHub</title>
      </head>
      <body>
        <h1>I'm new here!</h1>
      </body>
    </html>
    ```
    
3. 將檔案 push 至遠端並輸入 `https://{user_name}.github.io` 查看網站
    
    檔案 push 上去後查看該 repo 應該可以看到以下畫面，表示更新成功
    
    ![Page Build And Deployment](/assets/images/2022-12-11/Untitled%201.png)
    
    應可以看到之前新增的內容 index.html 
    
    ![Preview](/assets/images/2022-12-11/Untitled%202.png)
    


# 好醜, 可以變好看嗎?

雖然可以連到自己的網站了，但實在有點醜，然後我也不太了解前端要怎麼美化頁面，因此我們可以採用其他已經寫好的主題，既方便又好看。其中使用的就是 Jekyll ，除了有現成主題可以使用，還可以在本地端先預覽網站，確定符合預期後再 push 到 GitHub

Btw 以前 GitHub 有可以直接更改 theme 的選項，但後來為了安全性取消了，連結參考如下([https://www.notion.so/GitHub-Page-2342256795eb4056820853686b1d9c5f#3f15d20642a2457f90faf6edf4865779](https://www.notion.so/GitHub-Page-2342256795eb4056820853686b1d9c5f))

1. 安裝 Ruby
    
    因為 Jekyll 是用 Ruby 寫的，我是到 [https://rubyinstaller.org/](https://rubyinstaller.org/) 選擇最新版本 (Ruby+Devkit 3.1.X (x64))，一切按 default 安裝。安裝後會跳出下面的視窗，按 enter 就對了
    
    ![MSYS2 Installer](/assets/images/2022-12-11/Untitled%203.png)
    
    安裝完成可輸入 `ruby -v` 確定版本
    
2. 開啟 terminal 安裝 Jekyll 
    
    ```bash
    gem install jekyll
    ```
    
    安裝完成可輸入 `jekyll -v` 確定版本
    
3. 生成 Jekyll 相關檔案
    
    可以到你原本的 repo 生成，或是直接建立新的，我這邊是在原本的 repo 生成檔案，要記得把index.html刪 (否則首頁還是會吃原本的這個檔案)
    
    ```bash
    cd {your_github_repo} # 移到 local repo 的目錄
    jekyll new . --force # 生成 Jekyll 相關檔案
    ```
    
4. 可先在本地端check畫面
    
    執行 `jekyll serve`，就可以看到新增主題的畫面了，可先略過這步驟
     
5. 套用喜歡的主題
    
    基本上照官方文件([Quick-Start Guide - Minimal Mistakes (mmistakes.github.io)](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/))安裝 Minimal Tasks 就可以了，我採用的是 Remote Method，步驟如下
    
    - Create/replace the contents of your `Gemfile` with the following:
        
        ```bash
        source "https://rubygems.org"
        
        gem "github-pages", group: :jekyll_plugins
        gem "jekyll-include-cache", group: :jekyll_plugins
        ```
        
    - Add `jekyll-include-cache` to the `plugins` array of your `_config.yml`.
        
        ![Setting](/assets/images/2022-12-11/Untitled%204.png)
        
    - Run `bundle` in terminal
    - Add `remote_theme: "mmistakes/minimal-mistakes@4.24.0"` to your `_config.yml` file. Remove any other `theme:` or `remote_theme:` entry.
6. 確認主題是否套用成功
    
    因為前面下載過bundle，現在要在本地端預覽須執行 `bundle exec jekyll serve`
    若執行成功 terminal 應該會出現 Server address: `http://127.0.0.1:4000/`，在網址輸入連接到本機即可
    
    如果無法執行，可能是因為webrick ，只要執行`bundle add webrick`即可 ([https://talk.jekyllrb.com/t/load-error-cannot-load-such-file-webrick/5417/3](https://talk.jekyllrb.com/t/load-error-cannot-load-such-file-webrick/5417/3))
    


# 如何新增文章?

1. 新增markdown檔案
    
    我個人是都用 Notion 撰寫文章，然後再 export 成 .md 檔案
    
    檔案需要命名為以下格式 *`YYYY-MM-DD-NAME-OF-POST.md`*
    不過其實還是有許多地方要微調，例如圖片位置就需要修正，圖片不能放在 _folder 命名的資料夾裡面不然會被忽略掉，建議通常是在root創建asset資料夾，放在/asset/同層的 image 資料夾中的對應文章資料夾，圖片顯示格式如下

    `![Figure Description](/assets/images/2022-12-11/target-pic.png)`

    會ignore _folder 裡面非相關的資訊
    
2. 將檔案移至_posts
3. 再執行 `bundle exec jekyll serve` 就可以看到文章啦


# Summary

本篇記錄了如何從無到有建立 GitHub Pages 的網站，尚有許多項目還未完成，例如版面的 layout、文章category、images如何一起與文章管理、留言板等等，希望接下來能較系統化地整理這些資訊。以上如果有不對或值得補充的地方，請不吝指教！



# Reference

- https://www.casper.tw/jekyll/2014/01/13/windows-jekyll-server/
- https://github.com/mmistakes/minimal-mistakes
- https://mmistakes.github.io/minimal-mistakes/docs/configuration/


<!-- <script src="https://utteranc.es/client.js"
        repo="imwss-cyn/commentforimashely"
        issue-term="pathname"
        theme="github-dark"
        crossorigin="anonymous"
        async>
</script> -->

