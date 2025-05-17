---
layout: page
permalink: /repositories/
title: code
description:
nav: true
nav_order: 3
---

<!--
{% if site.data.repositories.github_users %}

## GitHub users

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for user in site.data.repositories.github_users %}
    {% include repository/repo_user.liquid username=user %}
  {% endfor %}
</div>

---
{% if site.repo_trophies.enabled %}
{% for user in site.data.repositories.github_users %}
{% if site.data.repositories.github_users.size > 1 %}

  <h4>{{ user }}</h4>
  {% endif %}
  <div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% include repository/repo_trophies.liquid username=user %}
  </div>

---

{% endfor %}
{% endif %}
{% endif %}
-->

{% if site.data.repositories.github_repos_pv %}

## Data science for PV

My traineeship at the European Commission's Joint Research Center kickstarted a project seeking a flexible, data-oriented approach for the definition of climatic zones with emphasis on PV applications. This repository contains the code for the reproduction of the results, featuring clustering and optimal transport embeddings for distribution-based classifications.

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.github_repos_pv %}
    {% include repository/repo.liquid repository=repo %}
  {% endfor %}
</div>
<br>
{% endif %}

{% if site.data.repositories.github_repos_ot %}

## Optimal Transport

My PhD code has mainly dealt with solving optimal transport problems efficiently on CPUs and GPUs. This has involved several areas in convex optimization including linear programming, graph optimization, fixed-point algorithms and primal-dual methods.

<div class="repositories d-flex flex-wrap flex-md-row flex-column justify-content-between align-items-center">
  {% for repo in site.data.repositories.github_repos_ot %}
    {% include repository/repo.liquid repository=repo %}
  {% endfor %}
</div>
<br>
{% endif %}
