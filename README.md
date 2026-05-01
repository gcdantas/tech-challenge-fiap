# Tech Challenge Fase 1 — IA para Apoio ao Diagnóstico Médico

## Introdução

Este projeto foi desenvolvido no contexto do **Tech Challenge — Fase 1 da Pós Tech/FIAP**, cujo objetivo é aplicar os fundamentos de Inteligência Artificial, Machine Learning e Visão Computacional em problemas relacionados ao processamento de dados médicos e exames clínicos.

O cenário proposto considera um grande hospital universitário que busca implementar uma solução inteligente de apoio ao diagnóstico, capaz de auxiliar equipes médicas na análise inicial de exames, na triagem de pacientes e na identificação de informações relevantes para a tomada de decisão. A proposta não substitui a avaliação médica, mas oferece uma base inicial de suporte computacional para classificação de doenças a partir de dados estruturados e, de forma complementar, imagens médicas.

Neste repositório, foram desenvolvidos notebooks com diferentes abordagens de modelagem preditiva aplicadas a bases médicas públicas. Os estudos incluem classificação de câncer de mama, diabetes, síndrome dos ovários policísticos e, como etapa extra de visão computacional, detecção de pneumonia em radiografias.

O PDF do **Tech Challenge Fase 1** anexado ao projeto pode ser consultado como documento de referência para o escopo, requisitos técnicos e critérios de entrega.

## Como executar o projeto

1. Clone este repositório ou baixe os arquivos do projeto.
2. Crie e ative um ambiente virtual, se desejar.
3. Instale as dependências do projeto:

```bash
pip install -r requirements.txt
```

4. Execute os notebooks Jupyter um a um, na ordem desejada:

```text
01_modelagem_breast_cancer.ipynb
02_modelagem_diabetes.ipynb
03_modelagem_ovario_polissistico.ipynb
04_Deteccao_de_Pneumonia_em_Radiografias.ipynb
```

Os datasets utilizados são referenciados nos próprios notebooks. Em especial, o dataset de radiografias de tórax possui tamanho elevado e, por isso, não foi versionado diretamente no GitHub. Porém, o código do notebook faz o download automático do dataset. Para essa etapa funcionar corretamente, é **necessário** estar conectado na internet. 

## Notebooks do projeto

### 01_modelagem_breast_cancer.ipynb

Este notebook desenvolve um modelo de classificação para diagnóstico de câncer de mama, utilizando o dataset **Breast Cancer Wisconsin** `datasets/dataset-wisconsin-breast-cancer.csv`. O fluxo inclui carregamento dos dados, inspeção inicial, remoção de colunas sem relevância analítica, padronização dos nomes das variáveis, conversão da variável alvo para formato numérico e análise exploratória com foco na distribuição das classes e na correlação entre atributos.

Na etapa de modelagem, são comparados modelos supervisionados como Regressão Logística, KNN e Random Forest. O notebook também avalia diferentes valores de `K` para o KNN, discute hiperparâmetros, seleciona o melhor modelo com base nas métricas obtidas e apresenta avaliação final com matriz de confusão, interpretação dos resultados e discussão crítica sobre o uso do modelo como apoio à decisão médica.

### 02_modelagem_diabetes.ipynb

Este notebook trata do diagnóstico preditivo de diabetes a partir do dataset `datasets/dataset-diabetes.csv`. A análise começa com inspeção estatística, identificação de inconsistências e tratamento de valores biologicamente impossíveis, como zeros em variáveis clínicas nas quais esse valor não faz sentido. Esses valores são convertidos para nulos e tratados posteriormente por imputação, reduzindo o risco de o modelo aprender padrões incorretos.

O processo inclui divisão estratificada entre treino e teste, análise de correlação, imputação pela mediana, padronização das variáveis e treinamento de modelos como Regressão Logística, Árvore de Decisão e Random Forest. A avaliação prioriza métricas relevantes ao contexto médico, especialmente o recall para a classe positiva, considerando que falsos negativos representam maior risco em problemas de triagem clínica.

### 03_modelagem_ovario_polissistico.ipynb

Este notebook aborda a classificação da **Síndrome dos Ovários Policísticos (SOP)** utilizando um dataset clínico em formato Excel `datasets/PCOS_data_without_infertility.xlsx`. O trabalho inclui carregamento da base, inspeção inicial, remoção de colunas de identificação ou sem utilidade analítica, tratamento de valores ausentes, padronização de colunas e conversão de atributos para formatos numéricos adequados à modelagem.

Após a análise exploratória, os dados são separados em treino e teste para o treinamento de modelos de classificação, incluindo Árvore de Decisão e Random Forest. O notebook apresenta métricas de avaliação, matrizes de confusão, análise de importância das variáveis e uso de SHAP Values para apoiar a interpretabilidade dos resultados, além de salvar os modelos treinados ao final do fluxo.

### 04_Deteccao_de_Pneumonia_em_Radiografias.ipynb

Este notebook corresponde à etapa extra de Visão Computacional, utilizando o dataset **Chest X-Ray Pneumonia** para classificação de radiografias entre casos normais e pneumonia. Como o dataset possui tamanho superior a 2 GB, o notebook verifica se os arquivos já estão disponíveis na pasta local esperada e, caso necessário, realiza o download utilizando a biblioteca `kagglehub`.

O modelo utiliza Transfer Learning com a arquitetura **MobileNetV2**, aplicando redimensionamento das imagens, normalização dos pixels e Data Augmentation nos dados de treino. A rede convolucional pré-treinada é mantida congelada e recebe camadas densas adicionais para classificação binária. A avaliação é feita por matriz de confusão e relatório de classificação, com atenção especial ao recall, pois a redução de falsos negativos é crítica em aplicações médicas.

## Datasets utilizados

- **Breast Cancer Wisconsin** — classificação de câncer de mama como benigno ou maligno.
- **N. Inst. of Diabetes & Diges. & Kidney Dis. Diabetes** — classificação de pacientes com ou sem diabetes.
- **PCOS Dataset** — classificação de Síndrome dos Ovários Policísticos.
- **Chest X-Ray Pneumonia** — classificação de radiografias entre normal e pneumonia.

## Observação sobre uso clínico

Os modelos desenvolvidos neste projeto têm finalidade acadêmica e demonstrativa. Eles podem apoiar análises iniciais e experimentos de triagem, mas não devem ser utilizados isoladamente para diagnóstico médico. A decisão clínica deve permanecer sob responsabilidade de profissionais de saúde qualificados.

## Documento de referência

O arquivo PDF anexado ao projeto, **IADT - Fase 1 - Tech challenge B.pdf**, pode ser utilizado como referência para o problema proposto, os requisitos de modelagem, os critérios de avaliação e os entregáveis esperados da fase.
