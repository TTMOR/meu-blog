---
layout: home
title: " Blog Técnico Tiago Moreira "
---

# 📘 Saudações! 

Criei via Backend  para documentar aprendizados, testes de código, relatórios técnicos etc.( Em construção!!)

## 🛠️ Tecnologias abordadas:
- Python
- Jekyll
- GitHub Pages
- Markdown
- Automação e scripts
- IoT
- Jupyter Lab
- E Muito mais.

## 📂 Últimos Posts
{% for post in site.posts limit:5 %}
- [{{ post.title }}]({{ post.url }})
{% endfor %}
