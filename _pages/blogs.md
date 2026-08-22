---
layout: archive
title: "Blogs"
permalink: /blogs/
author_profile: true
---

<p class="blog-index-intro">Notes on building reliable networked systems and practical tools for research and engineering.</p>
<p class="blog-index-profiles">
  <span class="blog-index-profiles__label">Other writing profiles:</span>
  <a href="https://greenlv.medium.com/">Medium</a>
  <span aria-hidden="true">·</span>
  <a href="https://blog.csdn.net/LvGreat">CSDN</a>
  <span aria-hidden="true">·</span>
  <a href="https://juejin.cn/user/3999369124122387">Juejin</a>
</p>

{% assign blog_posts = site.categories.blogs %}
<div class="blog-list">
  {% for post in blog_posts %}
    <article class="blog-list__item">
      <a class="blog-list__cover" href="{{ post.url | relative_url }}" aria-label="Read {{ post.title | escape }}">
        <img src="{{ '/images/' | append: post.header.teaser | relative_url }}" alt="{{ post.header.teaser_alt | escape }}">
      </a>
      <div class="blog-list__heading">
        <p class="blog-list__meta">
          <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %-d, %Y" }}</time>
        </p>
        <h2 class="blog-list__title"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      </div>
      <div class="blog-list__summary">
        <div class="blog-list__excerpt">{{ post.excerpt | markdownify }}</div>
        <p class="blog-list__links">
          <a href="{{ post.url | relative_url }}">Read article</a>
          <span aria-hidden="true">&middot;</span>
          {% if post.chinese_url %}
            <a href="{{ post.chinese_url }}">Read the Chinese original</a>
          {% else %}
            <span class="blog-list__pending">Chinese edition pending</span>
          {% endif %}
        </p>
      </div>
    </article>
  {% endfor %}
</div>
