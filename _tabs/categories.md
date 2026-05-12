---
layout: page
icon: fas fa-pen-nib
title: Posts
order: 1
---

<style>
/* ── Tree container ── */
.ptree {
  font-size: 0.91rem;
  line-height: 1.4;
  margin-top: 8px;
}

/* ── Category (folder) row ── */
.cat-row {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 8px 10px;
  border-radius: 5px;
  font-weight: 600;
  color: var(--heading-color, #1f2328);
  margin-top: 6px;
}
.cat-row:hover {
  background: var(--card-bg, #f6f8fa);
}
.cat-row a {
  color: inherit;
  text-decoration: none;
}
.cat-row a:hover {
  text-decoration: underline;
}

/* ── Post (file) row ── */
.file-row {
  display: flex;
  align-items: baseline;
  gap: 10px;
  padding: 5px 10px;
  border-radius: 4px;
  color: var(--text-color, #24292f);
}
.file-row:hover {
  background: var(--card-bg, #f6f8fa);
}
.file-row .ftitle {
  flex: 1;
  min-width: 0;
}
.file-row .ftitle a {
  color: inherit;
  text-decoration: none;
}
.file-row .ftitle a:hover {
  color: var(--link-color, #0969da);
}
.file-row .fdate {
  font-size: 0.77rem;
  color: var(--label-color, #888);
  white-space: nowrap;
  flex-shrink: 0;
}

/* ── Icons ── */
.ico-folder { color: #e5a430; }
.ico-file   { color: var(--label-color, #bbb); font-size: 0.85em; }

/* ── Post count badge ── */
.cat-count {
  font-size: 0.73rem;
  font-weight: 400;
  color: var(--label-color, #888);
  background: var(--card-bg, #f0f0f0);
  border: 1px solid var(--border-color, #d8d8d8);
  border-radius: 10px;
  padding: 1px 7px;
  margin-left: 2px;
}

/* ── Indent levels ── */
.l0 { padding-left: 0; }
.l1 { padding-left: 22px; }
.l2 { padding-left: 44px; }
.l3 { padding-left: 66px; }
.l4 { padding-left: 88px; }

/* ── Section separator ── */
.tree-sep {
  border: none;
  border-top: 1px solid var(--border-color, #e5e7eb);
  margin: 10px 0 4px;
}
</style>

<div class="ptree">

{%- comment -%} ── AI Development ─────────────────────────────────── {%- endcomment -%}
{% assign ai_dev_posts = site.posts | where_exp: "p", "p.categories[0] == 'AI Development'" | sort: "date" | reverse %}
<div class="cat-row l0">
  <i class="fas fa-folder ico-folder"></i>
  <a href="{{ '/categories/ai-development/' | relative_url }}">AI Development</a>
  <span class="cat-count">{{ ai_dev_posts.size }}</span>
</div>
{% for post in ai_dev_posts %}
<div class="file-row l1">
  <i class="far fa-file-alt ico-file"></i>
  <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
  <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
</div>
{% endfor %}

<hr class="tree-sep">

{%- comment -%} ── AI Study ─────────────────────────────────────────── {%- endcomment -%}
{% assign ai_study_posts = site.posts | where_exp: "p", "p.categories[0] == 'AI Study'" | sort: "date" | reverse %}
<div class="cat-row l0">
  <i class="fas fa-folder ico-folder"></i>
  <a href="{{ '/categories/ai-study/' | relative_url }}">AI Study</a>
  <span class="cat-count">{{ ai_study_posts.size }}</span>
</div>
{% for post in ai_study_posts %}
<div class="file-row l1">
  <i class="far fa-file-alt ico-file"></i>
  <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
  <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
</div>
{% endfor %}

<hr class="tree-sep">

{%- comment -%} ── Paper Review ─────────────────────────────────────── {%- endcomment -%}
{% assign paper_posts = site.posts | where_exp: "p", "p.categories[0] == 'Paper Review'" | sort: "date" | reverse %}
<div class="cat-row l0">
  <i class="fas fa-folder ico-folder"></i>
  <a href="{{ '/categories/paper-review/' | relative_url }}">Paper Review</a>
  <span class="cat-count">{{ paper_posts.size }}</span>
</div>
{% for post in paper_posts %}
<div class="file-row l1">
  <i class="far fa-file-alt ico-file"></i>
  <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
  <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
</div>
{% endfor %}

<hr class="tree-sep">

{%- comment -%} ── Development ──────────────────────────────────────── {%- endcomment -%}
{% assign dev_posts = site.posts | where_exp: "p", "p.categories[0] == 'Development'" | sort: "date" | reverse %}
<div class="cat-row l0">
  <i class="fas fa-folder ico-folder"></i>
  <a href="{{ '/categories/development/' | relative_url }}">Development</a>
  <span class="cat-count">{{ dev_posts.size }}</span>
</div>
{% for post in dev_posts %}
<div class="file-row l1">
  <i class="far fa-file-alt ico-file"></i>
  <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
  <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
</div>
{% endfor %}

<hr class="tree-sep">

{%- comment -%} ── Vibe Coding (3-level hierarchy) ──────────────────── {%- endcomment -%}
{% assign vibe_direct   = site.posts | where_exp: "p", "p.categories[0] == 'Vibe Coding' and p.categories[1] != 'AI Product Builder'" | sort: "date" | reverse %}
{% assign apb_direct    = site.posts | where_exp: "p", "p.categories.last == 'AI Product Builder'" | sort: "date" | reverse %}
{% assign gitblog_posts = site.posts | where_exp: "p", "p.categories.last == '깃블로그 바이브코딩'" | sort: "date" | reverse %}
{% assign vibe_total    = site.categories['Vibe Coding'] %}

<div class="cat-row l0">
  <i class="fas fa-folder-open ico-folder"></i>
  <a href="{{ '/categories/vibe-coding/' | relative_url }}">Vibe Coding</a>
  <span class="cat-count">{{ vibe_total.size }}</span>
</div>

{% for post in vibe_direct %}
<div class="file-row l1">
  <i class="far fa-file-alt ico-file"></i>
  <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
  <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
</div>
{% endfor %}

{%- comment -%} ── Vibe Coding > AI Product Builder ─────────────────── {%- endcomment -%}
{% assign apb_total = site.categories['AI Product Builder'] %}
<div class="cat-row l1">
  <i class="fas fa-folder-open ico-folder"></i>
  <a href="{{ '/categories/ai-product-builder/' | relative_url }}">AI Product Builder</a>
  <span class="cat-count">{{ apb_total.size }}</span>
</div>

{% for post in apb_direct %}
<div class="file-row l2">
  <i class="far fa-file-alt ico-file"></i>
  <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
  <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
</div>
{% endfor %}

{%- comment -%} ── Vibe Coding > AI Product Builder > 깃블로그 바이브코딩 ── {%- endcomment -%}
{% assign gitblog_total = site.categories['깃블로그 바이브코딩'] %}
<div class="cat-row l2">
  <i class="fas fa-folder ico-folder"></i>
  <span>깃블로그 바이브코딩</span>
  <span class="cat-count">{{ gitblog_total.size }}</span>
</div>

{% for post in gitblog_posts %}
<div class="file-row l3">
  <i class="far fa-file-alt ico-file"></i>
  <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
  <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
</div>
{% endfor %}

<hr class="tree-sep">

{%- comment -%} ── Tools & Tips ─────────────────────────────────────── {%- endcomment -%}
{% assign tools_posts = site.posts | where_exp: "p", "p.categories[0] == 'Tools & Tips'" | sort: "date" | reverse %}
<div class="cat-row l0">
  <i class="fas fa-folder ico-folder"></i>
  <a href="{{ '/categories/tools-tips/' | relative_url }}">Tools &amp; Tips</a>
  <span class="cat-count">{{ tools_posts.size }}</span>
</div>
{% for post in tools_posts %}
<div class="file-row l1">
  <i class="far fa-file-alt ico-file"></i>
  <span class="ftitle"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></span>
  <span class="fdate">{{ post.date | date: "%Y.%m.%d" }}</span>
</div>
{% endfor %}

</div>
