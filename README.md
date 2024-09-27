# IA-Feminista Elas no Congresso

A **IA-Feminista Elas no Congresso** é um projeto de inteligência artificial desenvolvido para **analisar e rotular automaticamente os temas de projetos de lei** em tramitação no Congresso Nacional, com foco em questões de gênero e feminismo. A solução utiliza dois modelos de linguagem pré-treinados e fine-tunados, o **BERT** e o **LLaMA**, para classificar os projetos em categorias específicas, como violência contra a mulher, direitos sexuais e reprodutivos, economia e trabalho, entre outros.

O objetivo do projeto é **facilitar a análise e o acompanhamento de projetos de lei** relacionados a temas feministas e de gênero, fornecendo **insights automatizados** que auxiliem na tomada de decisão, defesa de políticas públicas e divulgação de informações relevantes.

## Modelos Fine-Tunados
Ambos os classificadores (BERT e LLaMA) foram ajustados para reconhecer temas de interesse específicos. Os temas que o modelo consegue identificar incluem:

- Gênero
- Direitos sociais
- Economia
- Violência contra a mulher
- Maternidade
- Direitos sexuais e reprodutivos
- Dignidade sexual
- Política
- Feminicídio

## Dados

Os dados utilizados para o treinamento dos modelos consistem em **resumos de projetos de lei** em tramitação no Congresso Nacional. Esses dados foram **pré-processados e rotulados manualmente**, servindo de base para o fine-tuning dos classificadores. 

### Informação dos Dados (em construção)
*COLOCAR INFO DOS DADOS FINAIS*

## Modelos Utilizados

- **BERT** (Bidirectional Encoder Representations from Transformers)
- **LLaMA** (Large Language Model Meta AI)

## Arquitetura do Projeto

1. **Pré-processamento de Dados**: Scripts de limpeza e preparação de dados dos projetos de lei.
2. **Fine-Tuning**: Ajuste fino dos modelos **BERT** e **LLaMA** com base nos dados rotulados manualmente.
3. **Avaliação**: Avaliação da performance dos modelos utilizando métricas como:
   - **Acurácia**
   - **F1-Score**
   - **Precisão**
   - **Recall**

### Métricas de Avaliação (em construção)
*COLOCAR MÉTRICAS*

---
=======