---
layout: default
title: Research
permalink: /study/
description: 
---

<div class="research-articles">
  <h2>Study</h2>
  <ul class="study-list">
    {%- assign sorted_papers = site.study | sort: "date" | reverse -%}
    {%- for paper in sorted_papers -%}
      <li>
        <a href="{%- if paper.redirect -%}{{ paper.redirect }}{%- elsif paper.url -%}{{ paper.url | relative_url }}{%- else -%}#{%- endif -%}">
          <span class="study-title">{{ paper.title }}</span>
          <span class="study-date">{{ paper.date | date: "%Y.%m.%d" }}</span>
        </a>
      </li>
    {%- endfor -%}
  </ul>


<style>
.research-articles {
  max-width: 800px;
  margin: 0 auto;
  font-family: 'Georgia', serif;
}

.study-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.study-list li {
  margin-bottom: 0.8em;
  border-bottom: 1px solid #eee;
  padding-bottom: 0.8em;
}

.study-list li:last-child {
  border-bottom: none;
}

.study-list a {
  text-decoration: none;
  color: inherit;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5em 0;
}

.study-list a:hover {
  color: #666;
}

.study-title {
  font-size: 1.1em;
  font-weight: 500;
  color: #333;
}

.study-date {
  font-size: 0.9em;
  color: #888;
  font-family: monospace;
}
</style>
  