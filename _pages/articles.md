---
layout: default
title: main_projects
permalink: /articles/
display_categories: ['Publication', 'Project', 'ETC']
---
<!-- pages/projects.md -->
<div class="projects">
  {%- if site.enable_project_categories and page.display_categories %}
    <!-- Display categorized projects -->
    {%- for category in page.display_categories %}
    <h2 class="category">{{ category }}</h2>
    {%- assign categorized_projects = site.articles | where: "category", category -%}
    {%- assign sorted_projects = categorized_projects | sort: "date" %}
    {%- assign sorted_projects = sorted_projects | reverse %}

    <!-- Generate cards for each project -->
    {% if page.horizontal -%}
    <div class="container">
      <div class="row row-cols-2">
      {%- for project in sorted_projects -%}
        {% include projects_horizontal.html %}
      {%- endfor %}
      </div>
    </div>
    {%- else -%}
    <div class="grid">
      {%- for project in sorted_projects -%}
        {% include projects.html %}
      {%- endfor %}
    </div>
    {%- endif -%}
    {% endfor %}
  
  {%- else -%}
  <!-- Display projects without categories -->
    {%- assign sorted_projects = site.articles | sort: "date" -%}
    {%- assign sorted_projects = sorted_projects | reverse %}

    <!-- Generate cards for each project -->
    {% if page.horizontal -%}
    <div class="container">
      <div class="row row-cols-2">
      {%- for project in sorted_projects -%}
        {% include projects_horizontal.html %}
      {%- endfor %}
      </div>
    </div>
    {%- else -%}
    <div class="grid">
      {%- for project in sorted_projects -%}
        {% include projects.html %}
      {%- endfor %}
    </div>
    {%- endif -%}
  {%- endif -%}
  </div>
  