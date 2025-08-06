--- 
layout: post 
title: "Dask e novidades" 
date: 2025-06-08 
categories: [] 
--- 
**Dask** é uma biblioteca Python voltada para computação paralela e distribuída, ideal para quem trabalha com grandes volumes de dados e precisa escalar além do que o `pandas` e `NumPy` conseguem oferecer em memória.
---
## ⚙️ O que é Dask?
Dask permite executar operações em paralelo usando múltiplos núcleos ou até clusters distribuídos. Ele replica APIs conhecidas como `pandas`, `NumPy` e `scikit-learn`, facilitando a migração de código existente para ambientes mais escaláveis.
Principais componentes:
- **Dask DataFrame**: similar ao `pandas`, mas com suporte a dados maiores que a RAM.
- **Dask Array**: similar ao `NumPy`, com paralelismo automático.
- **Dask Delayed**: permite construir pipelines de execução preguiçosa.
- **Dask ML**: integra com `scikit-learn` para treinar modelos em paralelo.
---
## 🚀 Novidades recentes
### 1. Integração com Arrow e Parquet
Dask agora tem suporte aprimorado para leitura e escrita de arquivos **Apache Arrow** e **Parquet**, otimizando o desempenho em pipelines de dados modernos.
### 2. Suporte a GPUs com RAPIDS
Com a integração ao ecossistema **RAPIDS**, é possível usar Dask com GPUs para acelerar operações de DataFrame e Machine Learning, especialmente útil em ambientes com CUDA.
### 3. Scheduler adaptativo
O novo scheduler adaptativo permite que Dask ajuste dinamicamente o número de workers com base na carga de trabalho, melhorando o uso de recursos em clusters.
### 4. Melhorias no Dask Gateway
O **Dask Gateway** facilita a criação e gerenciamento de clusters em ambientes como Kubernetes, JupyterHub e HPC. A interface foi simplificada e agora suporta autenticação integrada.
---
## 🧪 Exemplos de uso
### Leitura de dados em paralelo:
```python
import dask.dataframe as dd
df = dd.read_csv('dados/*.csv')
resultado = df.groupby('categoria').valor.mean().compute()
