---
layout: landing
title: mceiba的个人博客
head_title: 晨旭园
description: |
  屌丝的技术生涯
---

<div class="row" style="margin-bottom:20px;">
  <div class="span7" style="width:95%">
    <h3 style="margin-bottom:5px; margin-left:20px">要么旅行,要么读书,身体和灵魂,必须有一个在路上</h3>
    <h6 align="right" style="font-size:12px; margin-right:8px">喜欢我或者我的博客，可以把它加入你的<a href="javascript:void(0)" onclick="window.external.AddFavorite(location.href, document.title)">收藏夹</a></h6>
  </div>
  <div class="span7 alert" style="width:575px;margin-right:10px;padding-right:20px;">
    <h1 id="start-now" style="margin-left: 0px; margin-right: 0px; font-size: 22px;">最新博文</h1>
    <div style="margin-left:-15px">
    {% assign posts_all = site.posts %}
    {% assign count = 10 %}
    {% include custom/posts_all %}
  </div>
  </div>
  
</div>

