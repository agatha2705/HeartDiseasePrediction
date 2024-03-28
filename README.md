# Heart Failure Prediction
### Projeto modelo de aprendizagem automática para detecção de possíveis riscos cardiovasculares e gestão precoces.
Dataset importado do Kaggle --> **[Dataset do Kaggle aqui](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction)**

## Etapa 1: Importando e entendendo a base de dados
Nessa estapa foi feito o básico: Importação das **bibliotecas** iniciais, importação da **base de dados** do Kaggle, verificação de **valores vazios**(NaN), valores **únicos**... Quais eram as **variáveis** em cada coluna, como quais eram os tipos de dor torácica, quais os resultados do eletrocardiograma em repouso, inclinação do segmento ST(Inclinação ascendente, Plano ou Inclinação descendente - up, flat, down)... Uma **análise rápida** para se familiarizar com o nosso Dataset e ter uma **visão mais geral** do problema.

## Etapa 2: Análise Exploratória (EDA)
Aqui entra uma **análise mais aprofundada** explorando mais **cada coluna** e a sua **relação com a coluna target "HeartDisease"**, que seria justamente a coluna que nos diz (0 ou 1), caso uma pessoa tenha ou não algum risco cardiovascular ou de insuficiência cardíaca.

Foram feitos gráficos com a biblioteca seaborn da **média de idade**, o resultado foi que a média está entre **53~55 anos** mostrando que o risco aumenta conforme a idade avança. Outros gráficos foram feitos para representar a distribuição das demais variáveis. Mostra que o **risco de doenças cardíacas é muito maior em homens do que em mulheres**, e de acordo com pesquisas, afetando cerca de um entre cada três a seis homens. Com base em outro gráfico, outro fator que também se destacou foi o **tipo de dor torácica que predomina em pessoas com risco/doença cardíaca**. O mais preocupante é que **ASY é o tipo de dor torácica assintomática**, a pessoa muitas vezes não tem noção do que pode estar acontecendo. Embora tenha mais pacientes que não possuem angina induzida por exercício, a maioria, **grande parte dos que possuem angina induzida por exercício é diagnosticada com doença cardíaca**. Mais um fator que se destacou foi a **inclinação do seguimento ST**. A maioria diagnosticada com doença cardíaca apresentava inclinação plana, dos **508 diagnosticados, 381 apresentavam inclinação plana**.

## Etapa 3: Tratando as colunas de texto
Como esse dataset não é muito grande, não tem tanta importância, mas é uma boa prática quando se trata de datasets mais volumosos. Essa boa prática consiste em transformar as colunas de texto **`"object"`** em **`"category"`**, isso diminui consideravelmente o espaço ocupado por esses dados.

## Etapa 4: Analisando os outliers
Foi resolvido não tirar os outliers, já que se trata da previsão de possíveis riscos e imprevistos, seria melhor mantê-los.

## Etapa 5: One Hot Encoding
Nessa etapa, as colunas postas como categóricas na etapa 3 foram transformadas em colunas numéricas com o método **`One Hot Encoding`** para o nosso modelo de machine learning. Com o One Hot Encoding, as colunas categorias se transformaram em colunas numéricas onde o número 1 representa o valor afirmativo e o 0 negativo.

## Etapa 6: Balanceando a nossa variável Target
Lembrando, a nossa variável target é a coluna "HeartDisease", a coluna que queremos prever. Há 508(1) e 410(0). Queremos balancear para tornar o nosso modelo mais eficiente, uma vez que o modelo pode interpretar que as chances de uma pessoa possuir algum tipo de risco ou sofrer de uma insuficiência cardíaca é maior do que a possibilidade de não ter nada, ou seja, saudável. O que pode interfirir no resultado final.
 - Usamos o **`SMOTE`**. O SMOTE é uma biblioteca que vai balancear os dados, ele vai avaliar o nosso conjunto de dados e vai criar dados consistentes até **igualar as variáveis**.

## Etapa 7: Separando os dados em dados de treino e teste (Train Test Split) & Padronizando os dados
Após separar os dados com **`Train Test Split`**, chegou a hora de padronizá-los. Para isso foi utilizado o método **`StandardScaler`**. Com isso, padronizei tanto o X_treino quanto o X_teste.

Pelos gráficos anteriores fazia mais sentido normalizá-los, já que a `normalização(normalization)` é mais utilizada, em geral, quando não sabemos a distribuição dos dados, ou sabemos que **`não é uma ditribuição gaussiana (normal)`**, sendo uma ténica útil principalmente em algoritmos que não fazem suposições sobre a distribuição, como KNN ou redes neurais. Já a `padronização(standardization)` é mais usada quando se sabe que a distribuição dos dados **`segue uma curva de distribuição gaussiana`**, ou muito próxima.
- Mas pelos resultados, a padronização(standardization) obteve melhores resultados.

## Etapa 8: Criando, Treinando e Avaliando os Modelos de Machine Learning
Os modelos testados foram o `KNN`(KNeighborsClassifier), `clf`(RandomForestClassifier), e o `lr`(LogisticRegression). 
> O *melhor modelo* foi o **`RandomForestClassifier`** com acurácia de **`87.21`**.

#### Configurando hiperparâmetros
- Depois de ter escolhido o melhor modelo chegou a hora de otimizá-lo. E para isso foi utilizado o método **`GridSearchCV`**. Com ele foi possível ver quais hiperparametros seriam mais adequados ao nosso modelo de previsão.
> A **pontuação** do nosso modelo de previsão para os dados de **treino** foi de **`98.31%`**.
> 
> A **pontuação** do nosso modelo de previsão para os dados de **teste** foi de **`89.18%`**.

#### Criando um Sistema de previsão simples
Nessa etapa foi criado um sistema de previsão simples com input de data que retornasse se a pessoa tem ou não risco cardiovascular ou de insuficiência cardíaca.

## Etapa 9: Salvando o nosso modelo com o pickle
Nessa última etapa foi utilizado o **`pickle`** para salvar tanto o **modelo de previsão**(**`RandoForestClassifier`**), quanto para salvar o nosso **padronizador**(**`StandardScaler`**), e novamente, testando no nosso sistema de previsão simples.
