---
title: Safari上更好的Bilibili-Old
tags: [Bilibili]
poster:
  topic: a better experience for bilibili
  headline: Bilibili-Old-Better for Safari
date: 2024-02-18 19:46:52
description: 恢复旧版Bilibili页面，为了那些念旧的人。
cover: https://f005.backblazeb2.com/file/img-forWeb/uPic/eJzL7c.png
banner: https://f005.backblazeb2.com/file/img-forWeb/uPic/sdbcqjkkjq.png
---
#### Preview


{% image https://f005.backblazeb2.com/file/img-forWeb/uPic/Screenshot2312231.png bg:white %}

#### 前置要求


##### [bilibili 页面净化大师](https://github.com/festoney8/bilibili-cleaner)

- 开启「BV号转AV号」功能


##### [Bilibili-Old (v9.1.8)](https://greasyfork.org/zh-CN/scripts/394296-bilibili-旧播放页?version=1111478) 

- 注释掉脚本内这段代码

- {% image https://f005.backblazeb2.com/file/img-forWeb/uPic/Screenshotashkjakjsnakjxnkj.png %}

- 目的是舍弃旧版本的AV转换算法，使用页面净化大师的AV转换算法。视频页面加载时会先跳出新版播放器页面，需要重新刷新页面进入旧版播放页面。

#### 脚本

```javascript
// ==UserScript==
// @name         Bilibili-Old-Better
// @namespace    http://tampermonkey.net/
// @version      2024-03-11
// @description  try to take over the world!
// @author       Paris
// @match        *://*.bilibili.com/**
// @run-at       document-start
// @icon         https://cdn.jsdelivr.net/gh/the1812/Bilibili-Evolved@preview/images/logo-small.png
// @grant        none
// ==/UserScript==

(function() {
    'use strict';

    var selectors = [

        'div.blur-bg', // 顶部导航背景
        'div.nav-menu',
        '#banner_link', // banner
        '#primary_menu', // 菜单栏
        'input.search-keyword',
        'input.nav-search-keyword', // 搜索框
        '.gif-menu .random-p img', //首页gif
        '.video-info-m h1', // 视频标题
        '.video-info-module h1', // 稍后再看页标题
        'div.carousel-box', // 首页活动大图
        '#home_popularize', // 首页推荐
        'a.head-logo', // 首页logo

        'div.number', // 点赞投币收藏
        'a.message.icon', // 发消息按钮
        'div.btn.followed', // 关注按钮
        'div.btn.followe', // 未关注按钮
        'button.bi-btn.text-only', // 展开按钮
        'span.title', //UP主列表
        'div.player-box', // 播放器
        'div.video-box-module', // 稍后再看播放器
        'div[name="widescreen"]',// 宽屏按钮
        '#arc_toolbar_report', //播放器工具栏
        'div.video-toolbar-module', // 稍后再看播放器工具栏
        '#v_tag', // tag
        'div.video-tag.video-tag-box.s_tag', // 稍后再看页tag
        'div.inside-wrp', //视频参与活动信息

        'div.footer.bili-footer.report-wrap-module', // 页脚备案信息
        'div.footer.bili-footer',
        '#special_recommend', // 首页底部推荐

        'body',

    ]

    // 应用样式函数
    function applyStyles(selector, element) {
        var currentHour = new Date().getHours();

        if (window.location.href === 'https://www.bilibili.com/') {
        // 在匹配到特定网址时执行操作
            if (selector === '#banner_link') {
                if (currentHour >= 9 && currentHour <= 14) {
                    element.style.backgroundImage = "url('https://i0.hdslb.com/bfs/album/198baa642414cb79b6338faf2c6bfd6f1c5f5b72.png')" // 白天
                } else if (currentHour > 14 && currentHour <= 16) {
                    element.style.backgroundImage = "url('https://i0.hdslb.com/bfs/album/784eb0b42070bb22a50dfae9baca3c09c79afb96.png')" // 下午
                } else if (currentHour > 16 && currentHour <= 19) {
                    element.style.backgroundImage = "url('https://i0.hdslb.com/bfs/album/988da1865b723ecfb1592fcd47e1d3952337c8ba.png')" // 黄昏
                } else if (currentHour > 19 && currentHour <= 22) {
                    element.style.backgroundImage = "url('https://i0.hdslb.com/bfs/album/c835b1e3895a1e77e9c4aa3ed052cfb5e7fd64bb.png')" // 晚上
                } else {
                    element.style.backgroundImage = "url('https://i0.hdslb.com/bfs/album/b6e2cb6e4fb30e515928511c4b28e40d0eab74c3.png')" // 深夜
                }
            } else if (selector === '.gif-menu .random-p img') {
                element.src = '//i0.hdslb.com/bfs/archive/c8fd97a40bf79f03e7b76cbc87236f612caef7b2.png';
            } else if (selector === '#primary_menu') {
                element.style.borderBottomColor = 'rgba(255,255,255,0)';
            } else if (selector === 'div.carousel-box'
                || selector === '#home_popularize'
                || selector === 'div.footer.bili-footer.report-wrap-module'
                || selector === '#special_recommend'
                || selector === 'a.head-logo') {
                element.remove();
            }
        }

        if (selector === 'div.blur-bg') {
            element.style.backgroundImage = '';
        } else if (selector === 'div.nav-menu') {
            element.style.fontWeight = 'bold';
            element.style.fontSize = '14px';
        } else if (selector === 'body') {
            element.style.fontWeight = '580';
        } else if (selector === 'input.nav-search-keyword' || selector === 'input.search-keyword') {
            element.placeholder = "请输入你想要搜索的内容";
        } else if (selector === 'div.player-box' || selector === 'div.video-box-module') {
            element.style.backgroundColor = 'rgba(255,255,255,0)';
            element.style.borderTop = '0';
            element.style.borderBottom = '0';
            element.style.padding = '0'
        } else if (selector === 'div[name="widescreen"]') {
            element.click();
        } else if (selector === '.video-info-m h1' || selector === '.video-info-module h1') {
            element.style.fontWeight = 'bold';
            if (currentHour <= 18 && currentHour >= 7) {
                element.style.color = '#000000';
            } else {
                element.style.color = '#ffffff';
            }
        } else if (window.location.href === 'https://www.bilibili.com/') {
            return;
        } else {
            if (element) {
                element.remove();
            }
        }
    }

    // 应用样式到元素函数
    function applyStylesToElements() {
        for (var i = 0; i < selectors.length; i++) {
            (function(index) {
                var elements = document.querySelectorAll(selectors[index]);
                elements.forEach(function(element) {
                    applyStyles(selectors[index], element);
                });
            })(i);
        }
    }

    function handleKeyPress(event) {

        var wide = document.querySelector('div[name="widescreen"]');
        var web = document.querySelector('div[name="web_fullscreen"]');
        var wide_n = document.querySelector('div.bpx-player-ctrl-btn.bpx-player-ctrl-wide');
        var web_n = document.querySelector('div.bpx-player-ctrl-btn.bpx-player-ctrl-web');

        if (document.activeElement.tagName !== 'INPUT') {
            if (event.keyCode === 87) { //W 宽屏
                if (wide) {
                    wide.click();
                } else if (wide_n) {
                    wide_n.click();
                }
            } else if (event.keyCode === 84) { //T 网页全屏
                if (web) {
                    web.click();
                } else if (web_n) {
                    web_n.click();
                }
            }
        }
    }

    // 设置定时器
    setTimeout(applyStylesToElements,800);

    // 监听按键按下事件
    document.addEventListener('keydown', handleKeyPress);
})();
```
#### 特别鸣谢：[Bilibili-Old](Bilibili-Old](https://github.com/MotooriKashin/Bilibili-Old) 

