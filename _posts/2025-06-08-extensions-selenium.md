---
layout: post
title: "Usar Extensões do Chrome (.crx) com Selenium"
date: 2025-06-08
categories: [automacao, selenium, navegador]
---

## 🔍 Visão Geral

Neste post mostro como **usar extensões do Chrome (.crx)** com Selenium, focando em automações como testes de WhatsApp Web, YouTube etc.

---

## 🎯 Passo 1 — Encontrar o ID da extensão

Exemplo:

https://chromewebstore.google.com/detail/sponsorblock/mnjggcdmjocbbbhaepdhchncahnbgone


ID: `mnjggcdmjocbbbhaepdhchncahnbgone`

---

## 🧩 Passo 2 — Baixar o `.crx`

Use um dos sites:

- [chrome-extension-downloader.com](https://chrome-extension-downloader.com)
- [crx.dam.io](https://crx.dam.io)

Cole o link da extensão e baixe o `.crx`.

---

## 💻 Passo 3 — Usar com Selenium

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

options = Options()
options.add_extension('/caminho/para/SponsorBlock.crx')

driver = webdriver.Chrome(options=options)
driver.get("https://web.whatsapp.com")

🧠 Dica extra: Repositório de extensões confiáveis
Você pode manter um diretório com .crx revisados para uso interno ou educacional.

Exemplo de estrutura:

plaintext
Copiar
Editar
meu_blog/
└── assets/
    └── crx/
        ├── sponsorblock.crx
        ├── darkreader.crx
        └── custom-blocker.crx
E incluir no Selenium:

python
Copiar
Editar
options.add_extension('assets/crx/sponsorblock.crx')
📘 Finalizando
Esse método permite uma automação mais flexível, sem depender de uma instalação manual das extensões no navegador. Ideal para projetos com foco em testes, scraping, e automações web avançadas.

Fique à vontade para adaptar o código e ampliar a lista de extensões úteis! 🚀