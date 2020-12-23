---
layout: page
title: projects
permalink: /projects/
description: Code for other projects can be found on <a href="https://github.com/edmudo" target="\_blank">Github</a>.
nav: true
---
{% assign sorted_projects = site.projects | group_by: "category" | sort: "importance" %}
{% for projects in sorted_projects %}
{% if projects.name != '' %}
<h2 class='project-category post-title'>{{projects.name}}</h2>
{% endif %}
<div class="projects grid">
  {% for project in projects.items %}
    <div class="grid-item">
      {% if project.redirect %}
      <a href="{{ project.redirect }}" target="_blank">
      {% else %}
      <a href="{{ project.url | relative_url }}">
      {% endif %}
        <div class="card hoverable">
          {% if project.img %}
          <img src="{{ project.img | relative_url }}" alt="project thumbnail">
          {% endif %}
          <div class="card-body">
            <h2 class="card-title text-lowercase">{{ project.title }}</h2>
            <p class="card-text">{{ project.description }}</p>
            <div class="row ml-1 mr-1 p-0">
              {% if project.github %}
              <div class="github-icon">
                <div class="icon" data-toggle="tooltip" title="Code Repository">
                  <a href="{{ project.github }}" target="_blank"><i class="fab fa-github gh-icon"></i></a>
                </div>
                {% if project.github_stars %}
                <span class="stars" data-toggle="tooltip" title="GitHub Stars">
                  <i class="fas fa-star"></i>
                  <span id="{{ project.github_stars }}-stars"></span>
                </span>
                {% endif %}
              </div>
              {% endif %}
            </div>
          </div>
        </div>
      </a>
    </div>
  {% endfor %}
</div>
{% endfor %}