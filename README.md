# Capacitismo Automatizado

## Entre Linguagem e Discriminação: Uma Análise Computacional do Capacitismo no Português Brasileiro

Este repositório reúne os códigos, experimentos e resultados desenvolvidos no contexto de uma pesquisa sobre **capacitismo linguístico em discursos digitais em Português Brasileiro (PT-BR)**, utilizando técnicas de **Processamento de Linguagem Natural (PLN)**.

A pesquisa investiga como manifestações capacitistas podem ser identificadas computacionalmente considerando não apenas a ocorrência de termos potencialmente discriminatórios, mas também o **contexto linguístico em que esses termos são empregados**.

O trabalho envolve a construção e validação de dados anotados, treinamento de modelos baseados no **BERTimbau Base**, adaptação de domínio e avaliação das predições em comentários provenientes de ambientes digitais brasileiros.

---

## Objetivo

O objetivo principal é investigar métodos computacionais para a identificação de **capacitismo linguístico em Português Brasileiro**, considerando a distinção entre manifestações discriminatórias e usos legítimos de termos relacionados à deficiência.

O estudo busca analisar:

- padrões linguísticos associados ao capacitismo;
- construção e validação de dados anotados em PT-BR;
- desempenho de modelos de classificação;
- efeito da adaptação de domínio;
- capacidade de generalização do classificador;
- influência de pistas lexicais nas decisões do modelo;
- erros e limitações da classificação automática.

---

## Estrutura do repositório

```text
Capacitismo-automatizado/
│
├── CAPTA-PTBR/
│   ├── Estagio 1/
│   └── Estagio 2/
│
├── BiasTube-PTBR/
│   ├── Extração/
│   ├── Treinamentos/
│   ├── Resultados/
│   └── Validação/
│
├── .gitattributes
└── README.md
```

O repositório está organizado em dois componentes principais: **CAPTA-PTBR** e **BiasTube-PTBR**.

---

# CAPTA-PTBR

O diretório `CAPTA-PTBR` reúne os materiais relacionados à construção e anotação do conjunto de dados utilizado no desenvolvimento do classificador.

## Estágio 1

O primeiro estágio está relacionado à identificação e seleção inicial de sentenças potencialmente relevantes para a investigação do capacitismo linguístico.

Essa etapa utiliza recursos lexicais e padrões linguísticos para auxiliar na recuperação de ocorrências candidatas.

```text
CAPTA-PTBR/
└── Estagio 1/
```

## Estágio 2

O segundo estágio corresponde à ampliação e validação do conjunto de dados, incluindo sentenças selecionadas a partir das probabilidades atribuídas pelo modelo.

```text
CAPTA-PTBR/
└── Estagio 2/
```

A anotação humana considera, entre outros aspectos:

**Presença de capacitismo**

- capacitista;
- não capacitista.

**Categoria da manifestação**

- insulto direto;
- uso metafórico;
- uso aparentemente neutro.

**Polaridade**

- positiva;
- negativa;
- neutra.

As decisões finais utilizadas nas análises são obtidas a partir do **voto majoritário dos anotadores**.

---

# BiasTube-PTBR

O diretório `BiasTube-PTBR` reúne os experimentos realizados sobre comentários provenientes do **BiasTube-PTBR**, utilizado para avaliar o comportamento do classificador em um conjunto distinto daquele empregado no treinamento.

```text
BiasTube-PTBR/
├── Extração/
├── Treinamentos/
├── Resultados/
└── Validação/
```

## Extração

Contém os códigos utilizados na preparação e extração dos dados empregados nos experimentos com o BiasTube-PTBR.

```text
BiasTube-PTBR/Extração/
```

---

## Treinamentos

Contém os experimentos de treinamento e aplicação dos modelos de classificação.

O principal modelo utilizado nos experimentos é o **BERTimbau Base**, modelo BERT pré-treinado para o Português Brasileiro.

Os experimentos consideram configurações com e sem **Domain-Adaptive Pretraining (DAPT)**, permitindo avaliar o efeito da adaptação do modelo ao domínio textual investigado.

```text
BiasTube-PTBR/Treinamentos/
```

---

## Resultados

Contém arquivos produzidos durante os experimentos, incluindo predições e resultados das avaliações dos modelos.

```text
BiasTube-PTBR/Resultados/
```

Entre as métricas utilizadas na avaliação estão:

- Precisão;
- Recall;
- F1-score;
- F1-macro;
- AUROC;
- AUPRC.

---

# Validação no BiasTube-PTBR

O diretório:

```text
BiasTube-PTBR/Validação/
```

reúne as análises relacionadas à **validação manual das predições realizadas pelo modelo**.

Foram selecionadas **3.000 sentenças** para anotação humana, considerando diferentes faixas de probabilidade atribuídas pelo classificador.

As decisões dos anotadores foram agregadas por voto majoritário e comparadas posteriormente às predições do modelo.

A comparação permitiu identificar:

| Resultado | Quantidade |
|---|---:|
| Verdadeiros Positivos (VP) | 1.303 |
| Verdadeiros Negativos (VN) | 1.402 |
| Falsos Positivos (FP) | 248 |
| Falsos Negativos (FN) | 44 |

Os casos de erro também foram analisados qualitativamente para investigar padrões linguísticos associados às decisões incorretas do classificador.

---

# Análise da dependência lexical

Uma análise adicional investiga se o classificador depende predominantemente dos termos empregados no recurso lexical utilizado para recuperar os dados ou se consegue identificar manifestações capacitistas para além dessas ocorrências.

Para isso, as sentenças foram comparadas segundo:

1. presença ou ausência de termos do dicionário;
2. classificação atribuída pelo modelo;
3. voto majoritário dos anotadores.

Foram observados os seguintes grupos:

| Termo no dicionário | Anotação | Predição | Interpretação | N |
|---|---|---|---|---:|
| Sim | Capacitista | Capacitista | VP com termo | 1.016 |
| Não | Capacitista | Capacitista | VP sem termo | 287 |
| Sim | Não capacitista | Não capacitista | VN com termo | 3 |
| Sim | Não capacitista | Capacitista | FP com termo | 23 |

Dos **1.303 verdadeiros positivos**, **287 (22,03%)** não apresentaram correspondência direta com os termos utilizados no recurso lexical.

Esse resultado indica que parte das classificações corretas não pode ser explicada exclusivamente pela presença literal dos termos empregados na recuperação dos dados.

Por outro lado, entre as **26 sentenças consideradas não capacitistas pelos anotadores que continham termos do dicionário**, 23 foram classificadas como capacitistas pelo modelo.

Assim, os resultados sugerem que a capacidade de generalização para além do recurso lexical coexiste com uma sensibilidade relevante a determinadas pistas lexicais.

---

# Pipeline experimental

De forma geral, o fluxo metodológico utilizado no projeto pode ser representado por:

```text
Recursos lexicais
       ↓
Recuperação de sentenças
       ↓
Anotação humana
       ↓
Construção do conjunto supervisionado
       ↓
BERTimbau Base
       ↓
Adaptação de domínio (DAPT)
       ↓
Treinamento do classificador
       ↓
Predição no BiasTube-PTBR
       ↓
Validação humana
       ↓
Análise quantitativa e qualitativa
       ↓
Análise da dependência lexical
```

---

# Tecnologias

Os experimentos são desenvolvidos principalmente em **Python** e **Jupyter Notebook/Google Colab**.

Principais bibliotecas e tecnologias utilizadas ao longo do projeto incluem:

- Python;
- Pandas;
- NumPy;
- Scikit-learn;
- PyTorch;
- Transformers;
- Hugging Face;
- BERTimbau;
- Google Colab.

---

# Organização da pesquisa

O repositório faz parte de uma pesquisa acadêmica sobre **Processamento de Linguagem Natural, linguagem discriminatória e capacitismo em Português Brasileiro**.

A abordagem combina:

- análise linguística;
- construção de corpus;
- anotação humana;
- aprendizado de máquina;
- modelos de linguagem pré-treinados;
- avaliação quantitativa;
- análise qualitativa de erros.

O objetivo não é simplesmente identificar palavras relacionadas à deficiência, mas investigar **como essas palavras e outras construções linguísticas são utilizadas em contexto**, distinguindo manifestações capacitistas de usos clínicos, descritivos, informativos ou sociais.

---

# Reprodutibilidade

Os notebooks disponibilizados no repositório documentam diferentes etapas do pipeline experimental.

Para reproduzir os experimentos, recomenda-se:

```bash
git clone <URL-DO-REPOSITORIO>
cd Capacitismo-automatizado
```

Os notebooks podem ser executados localmente em ambiente Jupyter ou no Google Colab.

Dependendo do experimento, pode ser necessário ajustar os caminhos de entrada e saída dos conjuntos de dados.

---

# Autoria

**Janaina Nogueira**

Universidade Federal de Mato Grosso do Sul  
Faculdade de Computação  
Programa de Pós-Graduação em Computação Aplicada

Área de pesquisa:

**Processamento de Linguagem Natural, Inteligência Artificial e análise computacional do capacitismo linguístico.**

---

## Observação ética

O conjunto de dados analisado pode conter linguagem ofensiva, discriminatória ou potencialmente sensível.

Esses conteúdos são mantidos exclusivamente para fins de **pesquisa científica, análise linguística e desenvolvimento e avaliação de métodos computacionais para identificação de linguagem capacitista**.
