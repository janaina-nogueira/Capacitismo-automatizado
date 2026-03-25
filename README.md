# 🧠 Capacitismo-automatizado  
Capacitismo Linguístico no Português Brasileiro: Uma Análise Computacional da Representação de Pessoas com Deficiência

---

## 📌 Sobre o Projeto

Este projeto investiga a detecção automática de expressões capacitistas em língua portuguesa utilizando técnicas de **Processamento de Linguagem Natural (PLN)** e modelos baseados em **Transformers (BERTimbau)**.

A pesquisa parte da hipótese de que termos relacionados à deficiência são frequentemente utilizados em contextos linguísticos com carga negativa, contribuindo para a reprodução de estereótipos e discriminação em ambientes digitais.

O trabalho combina análise linguística e modelagem computacional para identificar, classificar e analisar essas manifestações em larga escala.

---

## 🔎 Revisão Sistemática da Literatura

O projeto foi fundamentado a partir da Revisão Sistemática da Literatura:

**Automated Ableism: A Systematic Review on AI and Discrimination against People with Disabilities**

**Autores:**  
Janaina Nogueira de Souza Lopes  
Valéria Quadros dos Reis  
Anderson Corrêa de Lima  
Amaury Antônio de Castro Junior  


**Instituição:**  
Faculdade de Computação — Universidade Federal de Mato Grosso do Sul (UFMS)

### Principais achados:
- A literatura sobre viés algorítmico ainda explora pouco o capacitismo
- A maioria dos estudos concentra-se em inglês e contextos internacionais
- Há carência de recursos linguísticos estruturados em português
- Necessidade de abordagens que integrem linguística + IA

👉 A partir dessas lacunas, este projeto foi estruturado.

---

## 🎯 Objetivos

- Detectar padrões linguísticos associados ao capacitismo em português
- Distinguir usos ofensivos de usos neutros ou figurativos
- Treinar modelos supervisionados para classificação de capacitismo
- Avaliar generalização entre domínios
- Aplicar o modelo em larga escala (YouTube)
- Produzir análises qualitativas e quantitativas

---

## 🗂️ Corpora Utilizados

### 📘 TuPy-E
- Corpus anotado de discurso de ódio em português
- Contém categoria explícita de *ableism*
- Base inicial para extração de padrões

### 🧪 Capta-PTBR
Corpus criado neste projeto:
- **Estágio 1:** extração automática via padrões léxico-sintáticos  
- **Estágio 2:** refinamento com anotação manual  

### 🌐 BiasTube-PTBR
- +531 mil comentários do YouTube
- Dados reais e não anotados
- Usado para predição em larga escala

---

## ⚙️ Metodologia

A metodologia combina abordagens linguísticas e computacionais em um pipeline estruturado:

### 1️⃣ Extração baseada em padrões
- Definição de padrões léxico-sintáticos (ex: predicação, modificação)
- Uso de **spaCy (DependencyMatcher + Matcher)**
- Identificação de sentenças com potencial capacitismo

### 2️⃣ Construção do Capta-PTBR
- Extração inicial → **781 sentenças**
- Filtragem automática → **633 sentenças elegíveis**
- Formação do corpus intermediário

### 3️⃣ Anotação manual
- Total de **1500 sentenças**
  - 633 positivas (extraídas)
  - + negativas (amostragem aleatória)
- Anotação considerando:
  - presença de capacitismo (binário)
  - polaridade (negativa, neutra, positiva)
  - contexto semântico

### 4️⃣ DAPT (Domain-Adaptive Pretraining)
- Re-treinamento do BERTimbau com MLM
- Corpus: BiasTube-PTBR
- Objetivo: adaptação ao domínio de comentários

### 5️⃣ Fine-tuning supervisionado
- Treinamento com Capta-PTBR
- Estratégias:
  - divisão estratificada (80/20)
  - oversampling
  - class weights

### 6️⃣ Avaliação
Métricas utilizadas:
- Accuracy
- Precision
- Recall
- F1-score
- F1-macro
- AUROC
- AUPRC

### 7️⃣ Predição em larga escala
- Aplicação no BiasTube-PTBR
- +531 mil comentários analisados

Saídas:
- `prob_capacitismo`
- `classe_predita`

---


## 📊 Principais Contribuições

- Construção do **Capta-PTBR**, corpus inédito para capacitismo
- Formalização de padrões léxico-sintáticos interpretáveis
- Integração entre linguística e aprendizado de máquina
- Análise em larga escala do capacitismo em português
- Evidências empíricas sobre linguagem discriminatória em ambientes digitais



