# Heart Failure Prediction
Projeto para previsão de insuficiência cardíaca - **[Dataset do Kaggle aqui](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction)**

## Etapa 1: Importando e entendendo a base de dados
Nessa estapa foi feito apenas o básico, importação das bibliotecas, da base de dados do Kaggle, verificação de valores vazios, valores únicos... Mais uma análise visual rápida para uma visão mais geral do problema.

## Etapa 2: Análise Exploratória (EDA)
Aqui entra uma análise mais aprofundada explorando mais **cada coluna** e a sua **relação com a coluna target "HeartDisease"**, que seria justamente a coluna que nos diz (0 ou 1), caso uma pessoa tenha ou não algum risco. Além de demonstrações gráficas mais intuitivas.

## Etapa 3: Tratando as colunas de texto
Como esse dataset não é muito grande, não tem tanta importância, mas é uma boa prática quando se trata de datasets mais volumosos. Essa boa prática consiste em transformar as colunas de texto **`"object"`** para **`"category"`**, isso diminui consideravelmente o espaço ocupado por esses dados.

## Etapa 4: Analisando os outliers
Foi resolvido não tirar os outliers, já que se trata da previsão de possíveis riscos e imprevistos, então achei melhor mantê-los.

## Etapa 5: One Hot Encoding
Nessa etapa, as colunas postas como categóricas na etapa 3 foram transformadas em colunas numéricas com o método **`One Hot Encoding`** para o nosso modelo de machine learning.

## Etapa 6: Balanceando a nossa variável Target
Lembrando, a nossa variável target é a coluna "HeartDisease", a coluna que queremos prever. Há 508(1) e 410(0). Queremos balancear para tornar o nosso modelo mais eficiente, afinal, ele pode interpretar que as chances de uma pessoa estar em risco ou sofrer de uma insuficiência cardíaca é maior do que a possibilidade de não ter nada, ou seja, saudável. O que pode interfirir no resultado final.
 - Usamos o **`SMOTE`**. O SMOTE é uma biblioteca que vai balancear os dados, ele vai avaliar o nosso conjunto de dados e vai criar dados consistentes até **igualar as variáveis**.

## Etapa 7: Separando os dados em dados de treino e teste (Train Test Split) & Padronizando os dados
Após separar os dados com **`Train Test Split`**, chegou a hora de padronizá-los. Para isso foi utilizado o método **`StandardScaler`**. Com isso, padronizei tanto o X_treino quanto o X_teste.

Pelos gráficos anteriores fazia mais sentido normalizá-los, já que a `normalização(normalization)` é mais utilizada, em geral, quando não sabemos a distribuição dos dados, ou sabemos que **`não é uma ditribuição gaussiana (normal)`**, sendo uma ténica útil principalmente em algoritmos que não fazem suposições sobre a distribuição, como KNN ou redes neurais. Já a `padronização(standardization)` é mais usada quando se sabe que a distribuição dos dados **`segue uma curva de distribuição gaussiana`**, ou muito próxima.
- Mas pelos resultados, a padronização(standardization) obteve melhores resultados.

## Etapa 8: Criando, Treinando e Avaliando os Modelos de Machine Learning
Os modelos testados foram o `KNN`(KNeighborsClassifier), `clf`(RandomForestClassifier), e o `lr`(LogisticRegression). 
- O *melhor modelo* foi o **`RandomForestClassifier com acurácia de 87.21`**.

#### Configurando hiperparâmetros
- Depois de ter escolhido o melhor modelo chegou a hora de otimizá-lo. E para isso foi utilizado o método **`GridSearchCV`**. Com ele foi possível ver quais os hiperparametros que seriam mais adequados ao nosso modelo de previsão.
- A **pontuação** do nosso modelo de previsão para os dados de **treino** foi de `98.45%`
- A **pontuação** do nosso modelo de previsão para os dados de **teste** foi de `88.20%`

#### Criando um Sistema de previsão simples
Nessa etapa foi criado um sistema de previsão simples com input de data que retornasse se a pessoa tem ou não risco cardiovascular.

## Etapa 9: Salvando o nosso modelo com o pickle
Nessa última etapa foi utilizado o **`pickle`** para salvar tanto o **modelo de previsão**(RandoForestClassifier), quanto para salvar o nosso **padronizador**(StandardScaler), e novamente, testando no nosso sistema de previsão simples.
