# Capacitismo-automatizado
Entre Linguagem e Discriminação: Uma Análise Computacional do Capacitismo no Português Brasileiro

# Visão Geral
Este projeto investiga a detecção automática de expressões capacitistas em língua portuguesa utilizando técnicas de Processamento de Linguagem Natural (PLN) e modelos Transformer (BERTimbau).
O estudo integra três corpora complementares:
TuPy-E — corpus anotado com categorias de discurso ofensivo (incluindo ableism).
Capta-PTBR — conjunto criado a partir da extração de padrões léxico-sintáticos associados ao capacitismo.
BiasTube-PTBR — grande corpus de comentários do YouTube não anotados (500k+ sentenças).

O pipeline envolve extração baseada em padrões, anotação manual, treinamento supervisionado, DAPT (Domain-Adaptive Pretraining) e predição em larga escala, permitindo analisar como o capacitismo aparece em ambientes digitais brasileiros.

# Objetivos do Projeto

Detectar padrões linguísticos associados ao capacitismo em português.

Treinar modelos supervisionados para distinguir usos ofensivos de usos neutros de termos relacionados à deficiência.

Aplicar o modelo em larga escala para identificar capacitismo em um corpus não anotado (BiasTube-PTBR).

Avaliar transferência entre domínios e comportamento do modelo em dados reais.

Produzir análise qualitativa e quantitativa do fenômeno.

# Metodologia
1) Extração baseada em padrões

Padrões léxico-sintáticos (como "idiota", "retardado", "cego", "surdo", etc.) foram aplicados ao TuPy-E para identificar sentenças com potencial capacitismo.

2) Anotação manual

727 sentenças extraídas foram anotadas quanto à polaridade (negativa, neutra, positiva), com foco em diferenciar insultos explícitos de usos figurados ou descritivos.

3) DAPT — Domain-Adaptive Pretraining

O modelo BERTimbau foi re-treinado (MLM) no corpus BiasTube-PTBR para adaptação ao domínio de comentários da internet.

4) Fine-tuning supervisionado

Treinamento do classificador com o Capta-PTBR, incluindo:

divisão estratificada 80/20

oversampling

class weights

métricas: Accuracy, Precision, Recall, F1, AUROC, AUPRC

5) Predição no BiasTube-PTBR

O modelo gera:

prob_capacitismo — probabilidade estimada

classe_predita — rótulo final (0/1)

Mais de 531k comentários foram processados.


