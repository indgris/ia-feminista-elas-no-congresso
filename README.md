# IA-Feminista Elas no Congresso

A **IA-Feminista Elas no Congresso** é um projeto de inteligência artificial desenvolvido para **analisar e rotular automaticamente os temas de projetos de lei** no Congresso Nacional, com foco em questões de gênero e feminismo. A solução avaliou a performance de diversos modelos de linguagem pré-treinados e fine-tunados para classificar os projetos. Este repositório concentra as informações sobre a pesquisa e desenvolvimento de soluções para aperfeiçoar o processo de rotulagem de dados dos projetos de lei (PL) por meio de técnicas de Processamento de Linguagem Natural e a coleta automatizada de dados no site da Câmara e Senado Federal.

Como parte de seu monitoramento legislativo, a equipe do [Instituto AzMina](https://azmina.com.br/) filtra propostas de interesse por meio de palavras-chaves. As propostas são então revisadas e rotuladas pela equipe e instituições parceiras com um duplo objetivo:

- Tema: Definir o tema da proposta a partir do resumo (ementa) do PL, designando uma das categorias definidas pela contratante.

- Avaliação: Definir se a proposta é favorável ou não ao direito das mulheres, a partir de uma análise da ementa e do inteiro teor do PL.

Devido ao alto número de propostas coletadas, a rotulagem completamente manual é custosa e demanda alto investimento de recursos humanos. O desenvolvimento dos modelos de inteligência artificial supervisionados visa facilitar processo de rotulagem inicial dos dados. 

O objetivo do projeto é **facilitar a análise e o acompanhamento de projetos de lei** relacionados a temas feministas e de gênero, fornecendo **insights automatizados** que auxiliem na tomada de decisão, defesa de políticas públicas e divulgação de informações relevantes.

# Trabalhos prévios

A utilização de modelos de IA em documentos oficiais em português ainda é incipiente. Foi possível identificar trabalhos prévios que utilizam técnicas de processamento de linguagem natural (NLP) para textos legais, mas poucos guardam similaridade com as tarefas em questão. Não foi possível localizar nenhum trabalho prévio focado na classificação de textos legais entre favoráveis ou desfavoráveis aos direitos das mulheres, porém alguns trabalhos anteriores já utilizaram técnicas de NLP para classificação de textos legais em temas pré-determinados.

Os trabalhos listados propõe diferentes categorizações em documentos do âmbito jurídico ou legislativo. Apesar da similaridade da tarefa em questão, estes esforços não servem como um benchmark direto para o nosso projeto, uma vez que a taxonomia e os exemplos diferem daqueles usados no presente projeto. Dito isso, o trabalho que mais se aproxima ao nosso em termos comparativos é o [“A classification approach for estimating subjects of bills in the Brazilian Chamber of Deputies”](https://lume.ufrgs.br/handle/10183/267612), onde o autor experimentou classificadores para temas de proposições da Câmara dos Deputados do Brasil, comparando dois modelos BERT adaptados para o português, usando o texto da ementa. Os melhores resultados relatados foram com o modelo BERTimbau, alcançando 78,94% de pontuação F1 ponderada.

| Referência                                                                                                     | Acurácia | F1-score | Recall |
|---------------------------------------------------------------------------------------------------------------|----------|----------|--------|
| [A classification approach for estimating subjects of bills in the Brazilian Chamber of Deputies](https://lume.ufrgs.br/handle/10183/267612)               | 65%      | 73%      | 70%    |
| [verBERT: Automating Brazilian Case Law Document Multi-label Categorization Using BERT](https://sol.sbc.org.br/index.php/stil/article/view/17803)                         | 38%      | 71%      | 66%    |
| [Classificação de documentos jurídicos utilizando a arquitetura Transformer: uma análise comparativa com algoritmos tradicionais de Machine Learning e ChatGPT](https://ojs.brazilianjournals.com.br/ojs/index.php/BRJD/article/view/60747) | 62%      | 62%      | 62%    |

# Dados de treinamento

Os dados utilizados para o treinamento dos modelos consistem em **resumos de projetos de lei** em tramitação no Congresso Nacional. Esses dados foram **pré-processados e rotulados manualmente**, servindo de base para o fine-tuning dos classificadores. Os dados rotulados estão disponíveis como um dataset no HuggingFace [`azmina/ementas_congresso`](https://huggingface.co/datasets/azmina/ementas_congresso). Ao todo, o dataset contém 1.399 exemplos de projeto de lei, sendo 112 deles reservados para validação (e posteriormente incorporados aos dados de treinamento após a definição do modelo final) e 168 reservados para teste, que não foram usados em nenhum momento durante o treinamento.

# Arquitetura do Projeto

1. **Pré-processamento de Dados**: Scripts de limpeza e preparação de dados dos projetos de lei.
2. **Fine-Tuning**: Ajuste fino dos modelos com base nos dados rotulados manualmente.
3. **Avaliação**: Avaliação da performance dos modelos utilizando métricas como:
   - **Acurácia**
   - **F1-Score**
   - **Precisão**
   - **Recall**

# Modelo

## Modelo de classificação de temas

Os temas utilizados para classificação dos projetos de lei são:

```
{0: 'economia',
 1: 'genero',
 2: 'dignidade sexual',
 3: 'violencia contra a mulher',
 4: 'politica',
 5: 'direitos sexuais e reprodutivos',
 6: 'direitos sociais',
 7: 'maternidade',
 8: 'feminicidio'}
```

## Definição dos temas:

- economia: todos os projetos de lei que envolver questões de produção, distribuição, acumulação e consumo de bens materiais com recorte de gênero. A categoria inclui, por exemplo, a concessão de benefícios financeiros exclusivos para mulheres e pessoas LGBT, participação econômica de mulheres e outros grupos, abordando temas como igualdade salarial, empreendedorismo feminino, inclusão no mercado de trabalho, acesso a crédito e medidas para combater a precarização do trabalho feminino.

- genero: construções sociais e culturais atribuídas aos papéis masculinos e femininos na sociedade, que influenciam comportamentos, oportunidades e relações entre os sexos. O conceito de gênero é fundamental para entender desigualdades sociais e promover políticas que visem à equidade. Eeste conjunto de projetos de lei, inclui propostas sobre ideologia de gênero, igualdade de gênero, lgbtfobia, orientação sexual e identidade de gênero, propostas para promover a igualdade e eliminar discriminações e preconceitos baseados no gênero, medidas para garantir direitos e oportunidades iguais para mulheres, homens, pessoas trans e não-binárias em áreas como trabalho, educação, saúde, segurança e participação política.

- dignidade sexual: refere-se ao reconhecimento do valor de cada indivíduo em relação à sua sexualidade. Isso implica que todas as pessoas têm o direito de viver sua sexualidade de maneira plena e respeitosa, sem discriminação ou violência. A dignidade sexual garante as relações interpessoais sejam baseadas no respeito mútuo e no consentimento. Neste conjunto de projetos de lei, estão incluídos nessa categoria todos os textos que envolvem crimes contra a dignidade sexual, incluindo estupro e atos relacionados, violação sexual mediante fraude, assédio sexual, divulgação de cena de sexo ou de pornografia, tráfico de pessoas e ato obsceno.

- violencia contra a mulher: qualquer ato de violência baseado no gênero que resulte em danos para mulheres. Inclui projetos para prevenir, punir e erradicar a violência contra mulheres em todas as suas formas, incluindo violência física, psicológica, sexual, patrimonial e moral. Envolvem políticas de proteção, atendimento e apoio às vítimas, bem como campanhas educativas e ações para responsabilizar os agressores. Essa categoria inclui todos os tipos de violência contra mulheres, com exceção dos crimes contra a dignidade sexual, que estão agrupados em categoria homônima.

- politica: atividade relacionada à governança do Estado nos níveis minucipal, estadual e federal, e às relações de poder entre indivíduos ou grupos. Envolve projetos de lei voltados à participação política das mulheres e à promoção da equidade de gênero na esfera política. Incluem propostas para aumentar a representatividade feminina em cargos eletivos e de liderança, além de garantir a participação em processos de tomada de decisão e elaboração de políticas públicas.

- direitos sexuais e reprodutivos: conjunto de direitos humanos que garantem a todos os indivíduos liberdade e capacidade para decidir sobre sua vida sexual e reprodutiva. Isso inclui o direito à informação, à educação, ao acesso a serviços de saúde reprodutiva, ao aborto, ao planejamento familiar, assistência médica durante a gravidez, parto e pós-parto e ao livre exercício da sexualidade.

- direitos sociais: aqueles que garantem condições mínimas de vida digna a todos os indivíduos, incluindo acesso à educação, saúde, trabalho, moradia e seguridade social. Esses direitos visam promover a igualdade e a justiça social, assegurando que todos tenham oportunidades iguais para desenvolver seu potencial humano.

- maternidade: é a qualidade ou estado de ser mãe, envolvendo não apenas o ato biológico da gestação e do parto, mas também o cuidado, educação e proteção oferecidos à criança. Inclui iniciativas sobre licença-maternidade, saláario maternidade e adoção, proteção no ambiente de trabalho, acesso a creches, políticas de apoio à amamentação e assistência a mães em situação de vulnerabilidade.

- feminicidio: assassinato de mulheres motivado por questões de gênero, ou seja, por ela ser do sexo feminino. Inclui projetos para prevenir, combater e punir o feminicídio, como políticas para a prevenção, investigação e julgamento de crimes de feminicídio, bem como medidas de apoio e proteção às vítimas de violência de gênero.


### Avaliação

Para avaliação da linha base (baseline), foram utilizados 2 modelos de zero-shot e um modelo Naive-Bayes. Para a avaliação final, foram utilizados diversos modelos baseados na arquitetura Transformer, tanto da família BERT quanto aplicações de modelos generativos.

| Modelo                                 | Precisão | Recall | F1   |
|---------------------------------------|-----------|--------|------|
| Naive-Bayes                           | 0.54      | 0.16   | 0.16 |
| [mDeBERTa-v3-base-mnli-xnli](https://huggingface.co/MoritzLaurer/mDeBERTa-v3-base-mnli-xnli) (zero-shot)| 0.32      | 0.28   | 0.27 |
| [facebook/bart-large-mnli](https://huggingface.co/facebook/bart-large-mnli) (zero-shot)  | 0.34      | 0.25   | 0.25 |
| [legal-bert-base-cased-ptbr](https://huggingface.co/dominguesm/legal-bert-base-cased-ptbr)                             | 0.75      | 0.63   | 0.66 |
| [DeBERTina](tgsc/debertina-base-32k-vocab) | 0.82 | 0.74   | 0.75 |
| [BERTimbau large](https://huggingface.co/neuralmind/bert-large-portuguese-cased/)                             | 0.82      | 0.74   | 0.75 |
| [Congretimbau](https://huggingface.co/belisards/congretimbau)                          | 0.80      | 0.79   | 0.79 |
| [Gemma-9b](https://huggingface.co/unsloth/gemma-2-9b-bnb-4bit)                                 | 0.70      | 0.70   | 0.69 |
| [LLama3-8b](https://huggingface.co/unsloth/llama-3-8b-Instruct-bnb-4bit)                                | 0.66      | 0.61   | 0.61 |

O modelo com melhor performance foi adotado em produção e atingiu as seguintes métricas no conjunto de teste:


### Versões
- Transformers 4.45.1
- Pytorch 2.4.1+cu121
- Datasets 3.0.1
- Tokenizers 0.20.0


## Modelo de classificação dos projetos

O segundo modelo tem como objetivo definir se a proposta é favorável ou não ao direito das mulheres.
