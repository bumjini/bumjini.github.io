---
layout: default
title: Publications
permalink: /papers/
description: 
---

<div class="publications" style="margin-bottom: 150px;">
  <p style="margin-bottom: 20px;"></p>
  
  <div class="paper-grid">
    {%- assign sorted_papers = site.papers | sort: "date" | reverse -%}
    
    {%- for paper in sorted_papers -%}
      {% assign paper_gradient = paper.gradient | default: "linear-gradient(135deg, #f5f7fa 0%, #e4ebf5 100%)" %}
      {% assign paper_hover = paper.hover-gradient | default: "linear-gradient(135deg, #e0f7fa 0%, #b2ebf2 100%)" %}
      
      <div class="paper-item">
        {% if paper.redirect -%}
          <a href="{{ paper.redirect }}" class="paper-card-link">
        {%- else -%}
          <a href="{{ paper.url | relative_url }}" class="paper-card-link">
        {%- endif %}
          <div class="paper-card" style="background: {{ paper_gradient }};" data-hover-gradient="{{ paper_hover }}">
            {%- if paper.img -%}
              <div class="paper-image">
                <img src="{{ paper.img | relative_url }}" alt="{{ paper.title }}">
                <div class="paper-overlay">
                  <h2>{{ paper.title }}</h2>
                  {%- if paper.pdf or paper.code or paper.github -%}
                    <div class="paper-links">
                      {%- if paper.pdf -%}
                        <span class="paper-link pdf" onclick="window.open('{{ paper.pdf }}', '_blank'); event.stopPropagation();">PDF</span>
                      {%- endif -%}
                      
                      {%- if paper.code -%}
                        <span class="paper-link code" onclick="window.open('{{ paper.code }}', '_blank'); event.stopPropagation();">Code</span>
                      {%- endif -%}
                      
                      {%- if paper.github -%}
                        <span class="paper-link github" onclick="window.open('{{ paper.github }}', '_blank'); event.stopPropagation();">
                          <i class="fab fa-github"></i>
                        </span>
                      {%- endif -%}
                    </div>
                  {%- endif -%}
                </div>
              </div>
            {%- endif -%}
          </div>
        </a>
      </div>
    {%- endfor -%}
  </div>
</div>

<style>
  .paper-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-auto-rows: 250px;
    grid-auto-flow: dense;
    gap: 20px;
    margin-top: 40px;
    background-color:rgb(255, 255, 255);
    padding: 20px;
    border-radius: 10px;
  }
  
  /* Vertical spans pattern for 3-column layout */
  .paper-item:nth-child(9n) {
    grid-column: span 1;
    grid-row: span 2;
  }
  
  .paper-item:nth-child(9n+4) {
    grid-column: span 1;
    grid-row: span 2;
  }
  
  .paper-card {
    border-radius: 0;
    overflow: hidden;
    box-shadow: none;
    height: 100%;
    width: 100%;
    transition: transform 0.3s ease;
    position: relative;
  }
  
  .paper-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 20px rgba(0,0,0,0.15);
  }
  
  .paper-image {
    height: 100%;
    width: 100%;
    position: relative;
    overflow: hidden;
    mask-image: radial-gradient(circle, black 90%, transparent 100%);
    -webkit-mask-image: radial-gradient(circle, black 90%, transparent 100%);
  }
  
  .paper-image::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    box-shadow: inset 0 0 20px 10px #f9f9f9;
    pointer-events: none;
  }
  
  .paper-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.5s ease;
  }
  
  .paper-card:hover .paper-image img {
    transform: scale(1.05);
  }
  
  .paper-overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background: linear-gradient(to top, rgba(173, 216, 230, 0.8) 0%, rgba(173, 216, 230, 0) 100%);
    color: #333;
    padding: 20px;
    opacity: 0;
    transition: opacity 0.3s ease;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    height: 100%;
  }
  
  .paper-card:hover .paper-overlay {
    opacity: 1;
  }
  
  .paper-overlay h2 {
    margin: 0 0 10px 0;
    font-size: 1.2rem;
    text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
  }
  
  .paper-links {
    display: flex;
    gap: 10px;
    margin-top: 10px;
  }
  
  .paper-link {
    background: rgba(41, 128, 185, 0.2);
    color: #333;
    padding: 5px 10px;
    border-radius: 20px;
    font-size: 0.8rem;
    backdrop-filter: blur(5px);
    transition: background 0.3s;
    cursor: pointer;
  }
  
  .paper-link:hover {
    background: rgba(41, 128, 185, 0.4);
  }
</style>

<script>
  document.addEventListener('DOMContentLoaded', function() {
    // Randomize the order of paper items to create visual interest
    const container = document.querySelector('.paper-grid');
    const items = Array.from(container.querySelectorAll('.paper-item'));
    
    // Randomize the sizes a bit to create more visual interest
    items.forEach((item, index) => {
      // Apply different rotation angles for a scattered look
      const randomAngle = (Math.random() * 4 - 2) + 'deg';
      item.querySelector('.paper-card').style.transform = `rotate(${randomAngle})`;
      
      // On hover, straighten the card
      item.querySelector('.paper-card').addEventListener('mouseenter', () => {
        item.querySelector('.paper-card').style.transform = 'translateY(-5px) rotate(0deg)';
      });
      
      // On mouse leave, return to original rotation
      item.querySelector('.paper-card').addEventListener('mouseleave', () => {
        item.querySelector('.paper-card').style.transform = `rotate(${randomAngle})`;
      });
    });
  });
</script>
  