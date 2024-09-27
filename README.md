# ia-feminista-elas-no-congresso

A IA-Feminista Elas no Congresso é um projeto de inteligência artificial desenvolvido para analisar e rotular automaticamente os temas de projetos de lei em tramitação no Congresso Nacional, com foco em questões de gênero e feminismo. A solução utiliza dois modelos de linguagem pré-treinados e fine-tunados, o BERT e o LLaMA, para classificar os projetos em categorias específicas, como violência contra a mulher, direitos sexuais e reprodutivos, economia e trabalho, entre outros.

O projeto busca facilitar a análise e o acompanhamento de projetos de lei relacionados a temas feministas e de gênero, fornecendo insights automatizados que auxiliem na tomada de decisão, defesa de políticas públicas e divulgação de informação.


Modelos Fine-Tunados: Ambos os classificadores foram ajustados para reconhecer nossos temas de interesse.
Os temas são:

- genero
- direitos sociais
- economia,
- violencia contra a mulher,
- maternidade
- direitos sexuais e reprodutivos,
- dignidade sexual,
- politica,
- feminicidio


Dados

Os dados utilizados para o treinamento dos modelos consistem em resumos de projetos de lei em tramitação no Congresso Nacional. Esses dados foram pré-processados e rotulados manualmente para servir de base para o ajuste fino dos classificadores. ##COLOCAR INFO DOS DADOS FINAIS

Modelos Utilizados

BERT (Bidirectional Encoder Representations from Transformers)
LLaMA (Large Language Model Meta AI)

Arquitetura do Projeto
Data Preprocessing: Scripts de limpeza e preparação de dados dos projetos de lei.
Fine-Tuning: Fine-tuning dos modelos BERT e LLaMA nos dados rotulados.
Avaliação: Avaliação da performance dos modelos em um conjunto de validação com métricas de acurácia, F1-score, precisão e recall.


###COLOCAR MÉTRICAS
