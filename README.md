# 📊 Análise do Mercado de Banda Larga — ISPs no Brasil

## Contexto

Um fundo de investimento hipotético considera entrar no mercado brasileiro de banda larga por meio da **aquisição de Provedores de Serviços de Internet (ISPs)**.  
O objetivo é avaliar as **perspectivas de crescimento** do mercado, considerando **tecnologias** (fibra óptica, cobre etc.) e **regiões** (UFs, macrorregiões, Brasil como um todo).

Este projeto foi desenvolvido como parte de um **case de Data Science Internship** e conduzido em Python/Jupyter Notebook.

---

## Estrutura do Projeto

O projeto segue uma arquitetura em camadas:

```
RAW (dados originais Anatel/IBGE)
↓ limpeza/normalização
TRUSTED (dados limpos em Parquet — Anatel particionado por ano/UF)
↓ Analíses
1 - Penetração por UF/ano/tecnologia
2 - Crescimento/CAGR por tecnologia e região
3 - Market share por UF/ano — total e ISPs
4 - Tamanho do player ISP — assinantes totais + nº de municípios atendidos (2023)
5 - Crescimento por tecnologia (Brasil) 2019→2023
6 - Forecast 2024: aplica CAGR (2020→2023) por UF × tecnologia na base de 2023
7 - ISPs-alvo
8 - Domicílios com e sem internet (Brasil, base 2023) + % formatadas
9 - Sumário: principais tabelas para o relatório
↓ Conclusão
Conclusões & Recomendações
```

---

## Fontes de Dados

- **Anatel**: acessos de banda larga fixos por município, empresa, tecnologia e velocidade.
- **IBGE**: estatísticas domiciliares (população, domicílios totais e ocupados).

Arquivos:

- 17 arquivos `.csv` (Anatel)
- 1 arquivo `.parquet` (IBGE)

---

## Métricas-Chave

O projeto implementa as seguintes métricas:

- **Penetração** = assinantes de banda larga ÷ domicílios total (IBGE).
- **Crescimento (CAGR)** = variação anualizada de assinantes em determinado período.
- **Market Share** = % dos assinantes totais por grupo econômico (ISPs vs grandes).
- **Tamanho do Player** = número de assinantes (2023) e footprint (municípios atendidos).
- **Forecast 2024** = baseline usando CAGR 2020–2023 por UF × tecnologia.

---

## Principais Achados

- **Fibra** teve um crescimento de 24,38% de participação em 2019 para 75,36% de participação em 2023. Com foco em FTTH.
- Regiões com maior crescimento: **Nordeste e Norte**.
- ISPs têm **35,37% de market share** no país.
- **Shortlist de ISPs candidatos**: players do grupo economico ISP, ≥ 50k assinantes, ≥ 30 municípios, ≥ 50% em fibra e CAGR ≥ 9% a.a.

---

## Estrutura dos Notebooks

- `analise_isp.ipynb`: notebook principal, com ingestão e análises.

---

## Como Executar

1. Clone o repositório:
   ```bash
   git clone https://github.com/<seu-usuario>/<seu-repo>.git
   cd <seu-repo>
   ```
2. Crie uma pasta Raw e coloque os arquivos 17 arquivos csv da Anatel e o parquet do IBGE

3. Crie o ambiente virtual e instale dependências:

   ```bash
   python -m venv venv
   source venv/bin/activate   # Linux/Mac
   venv\Scripts\activate      # Windows

   pip install -r requirements.txt
   ```

4. Execute `analise_isp.ipynb`.

## Stack Utilizada

- Python 3.10+
- Pandas — análise tabular
- PyArrow — leitura otimizada de Parquet
- DuckDB — engine SQL para analíses
- Matplotlib — visualização
- Jupyter Notebook — desenvolvimento e apresentação
