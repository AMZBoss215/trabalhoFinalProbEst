# 📊 Pipeline Estatístico para Análise de Reprocessos — SprintForge S.A.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![R Version](https://img.shields.io/badge/R-v4.6.0-blue.svg)](https://www.r-project.org/)

Este repositório contém o pipeline automatizado de análise estatística e modelagem probabilística desenvolvido para avaliar o índice de retrabalho (*reprocessos*) de um *squad* de desenvolvimento da **SprintForge S.A.** O projeto integra conceitos de Engenharia de Software Ágil (Framework Scrum) com inferência estatística avançada para suporte à tomada de decisão e governança de TI.

O relatório técnico deste projeto foi estruturado a partir da adaptação customizada de um modelo de iniciação científica, sendo refinado e simplificado para focar estritamente nos requisitos de governança de TI e engenharia de software da organização.

---

## 🎯 Contexto e Objetivo do Problema

No ecossistema da SprintForge S.A., o volume excessivo de cartões de tarefas reabertos por sprint compromete a previsibilidade das entregas e infla os débitos técnicos. A governança de TI estipulou uma meta de qualidade operacional de, no máximo, **3 reprocessos por sprint**. 

Com base em uma amostra empírica de **30 sprints consecutivas** conduzidas ao longo do ano de 2025, este pipeline foi construído para responder eletronicamente e de forma científica à pergunta:  
> *A média populacional de reprocessos do squad viola o teto tolerável estabelecido pela governança?*

---

## 📁 Estrutura do Repositório

O projeto segue uma estrutura modular de diretórios para garantir o versionamento limpo e a reprodutibilidade da pesquisa:

```text
├── data/
│   └── sprints.csv                 # Base de dados empírica (30 observações)
├── plots/
│   └── grafico_modelos_teoricos.png # Gráfico ggplot2 unificando dados e modelos
├── R/
│   └── analise_estatistica.R        # Script de automação e modelagem paramétrica
├── .gitignore                      # Filtros de workspace do RStudio (.RData, .Rhistory)
├── LICENSE                         # Licença MIT de código aberto
└── README.md                       # Documentação principal do ecossistema

```

---

## 📊 Principais Resultados Estatísticos

Os dados foram processados via **RStudio** através de estimadores de máxima verossimilhança e testes de significância frequentistas. Os resultados exatos obtidos no console foram:

### 📈 Análise Descritiva

* **Média Amostral ($\bar{X}$):** `4,733` reprocessos por sprint (violando a meta de $\le 3$).
* **Variância Amostral ($S^2$):** `2,823` | **Desvio Padrão ($S$):** `1,680`.
* **Coeficiente de Variação (CV):** `35,50%` (Dispersão moderada com picos extremos de 8 reprocessos).

### 🎲 Modelagem Probabilística (Binomial Negativa vs Poisson)

Devido à interdependência de tarefas no framework Scrum (onde a falha de um componente arquitetural causa a reabertura de cartões em bloco), os dados violaram a premissa de independência de Poisson, apresentando **superdispersão latente**.

* O ajuste por máxima verossimilhança estimou os parâmetros da **Binomial Negativa** em $r = 284,98$ e $p = 0,984$.
* sob este modelo, a probabilidade de o *squad* enfrentar cenários críticos de alta saturação ($\ge 6$ reprocessos) é de **$33,77\%$** (1 em cada 3 sprints).

### 🧮 Inferência e Teste de Hipótese

* **Intervalo de Confiança (IC 95%):** $[4,106 \ ; \ 5,361]$. Como o limite inferior ($4,106$) é estritamente maior que 3, há evidência bauxal de desconformidade crônica.
* **Teste t-Student Unilateral à Direita:** Com $t = 5,651$ e **Valor-p = $2,09 \times 10^{-6}$**, a hipótese nula $H_0: \mu = 3$ é categoricamente rejeitada ao nível de significância de $5\%$.

---

## 🚀 Como Executar o Pipeline

### Pré-requisitos

Certifique-se de ter o **R** e o **RStudio** instalados em seu ambiente de desenvolvimento (Linux/WSL ou Windows).

### Execução

1. Clone este repositório em sua máquina:
```bash
git clone [https://github.com/SEU_USUARIO_CORRETO/trabalhoFinalProbEst.git](https://github.com/SEU_USUARIO_CORRETO/trabalhoFinalProbEst.git)

```


2. Abra o arquivo do script localizado em `R/analise_estatistica.R`.
3. Certifique-se de que as dependências necessárias (`MASS`, `ggplot2` e `readr`) serão instaladas automaticamente executando as primeiras linhas do código.
4. Rode o script completo para gerar o sumário estatístico no console e atualizar a plotagem teórica na pasta `plots/`.

---

## ⚖️ Licença

Este projeto está licenciado sob a **Licença MIT** - consulte o arquivo [LICENSE](./LICENSE) para obter detalhes. O código é livre para modificação, distribuição e uso em portfólios, mantendo a atribuição original do autor.

---

