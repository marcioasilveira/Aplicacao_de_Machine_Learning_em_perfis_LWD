
# Aplicação de Machine Learning em perfis LWD
#### Aluno: [Márcio Albuquerque Silveira](https://github.com/marcioasilveira)
#### Orientadoras: [Amanda Lemette T. Brandão](https://github.com/amandalemette) e [Júlia Potratz](https://github.com/jupotratz).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- [Link para o código: Entrada de dados](https://github.com/marcioasilveira/Aplicacao_de_Machine_Learning_em_perfis_LWD/blob/main/TCC_Notebook1_entrada_de_dados.ipynb).
- [Link para o código: Aplicação do algoritmo](https://github.com/marcioasilveira/Aplicacao_de_Machine_Learning_em_perfis_LWD/blob/main/TCC_Notebook2_FE_xgb.ipynb)  

---

### Resumo

Este trabalho teve como objetivo realizar uma aplicação de aprendizado de máquina em perfis adquiridos por ferramentas LWD (Logging While Drilling) para que eles reproduzissem os resultados  do perfil fator fotoelétrico adquirido por ferramentas a cabo. Foi utlizado um *dataset* limitado, com apenas dois poços, e aplicado o algoritmo *Extreme Gradient Boosting* (XGBoost). O ajuste realizado reduziu significantemente o erro médio quadrático, obtendo valores próximos dos encontrados na perfilagem a cabo. A continuação deste trabalho, com um *dataset* mais robusto, deve incorporar poços de diferentes contextos geológicos.  

### 1. Introdução

Há um esforço constante na indústria do petróleo para reduzir os custos e o tempo entre a perfuração de um poço e sua entrada em produção. Ao mesmo tempo, é preciso contar com as melhores informações disponíveis para reduzir as incertezas nas tomadas de decisão. Uma das etapas necessárias na perfuração de um poço é a realização da perfilagem, que pode ser feita de duas formas: a perfilagem LWD, durante a perfuração, ou a perfilagem a cabo, realizada após a perfuração do poço. Os custos associados ao tempo de sonda tornam a perfilagem a cabo muito mais cara do que a perfilagem LWD. No entanto a perfilagem LWD está mais sujeita a fatores ambientais e assim tende a ser menos precisa quando comparada à perfilagem a cabo.

A proposta deste trabalho é, utilizando uma base de dados de poços onde foram corridos perfis LWD e a cabo, treinar o algoritmo de aprendizado de máquina XGBoost para estimar os perfis de fator fotoelétrico a cabo a partir dos perfis LWD. Para isso usamos como dados de entrada os perfis LWD (*gamma ray*, nêutrons, densidade, caliper, e fator fotoelétrico) tendo como alvo o perfil de fator fotoelétrico da perfilagem a cabo. O fator fotoelétrico é um subproduto do perfil de densidade, que é utilizado para identificação mineralógica, para definir o volume de quartzo/calcita/dolomita na rocha. O fator fotoelétrico medido em LWD é muito diferente do cabo em termos relativos.

### 2. Modelagem

Foram fornecidos dados de dois poços (w1 e w2) para treinamento e teste da rede. Os dados não são publicados por questões de confidencialidade. Os gráficos comparativos entre as medidas de fator fotoelétrico medidos na perfilagem LWD e perfilagem a cabo nos dois poços mostram que as medidas feitas por LWD apresentam valores superiores, provavelmente devido a diferenças no ambiente de perfilagem.

<img src='/imagem/FE_W1-reta45.png' height="250" width="300"> <img src='/imagem/FE_W2-reta45.png' height="250" width="300">

O dataset recebido não tinha dados faltantes nem espúrios. No entanto estavam muito desbalanceados. 
 
Distribuição do Dataset original.               

<img src='/imagem/desbalanceio.png' height="250" width="300"> 

Para balacear as amostras foram gerados dados sintéticos do poço com menor quantidade de dados. Para isso foi utilizado a ferramenta SMOTE (*Synthetic Minority Over-sampling Technique*) da biblioteca python imblearn. O SMOTE utiliza o algoritmo k-nearest neighbor (KNN) para gerar os dados sintéticos.

Dataset após o balanceamento.

<img src='/imagem/balanceado.png' height="250" width="300">

O *tuning* dos hiperparâmetros do algoritmo XGBoost foi realizado utilizando a biblioteca python HyperOpt, baseada em otimização bayesiana. Os hiperparâmetros otimizados foram *max_depth*, *min_child_weight*, *gamma*, *subsample*, *colsample_bytree*, *colsample_bylevel*, *reg_alpha*, *reg_lambda* e *learning_rate*, sendo os restantes deixados com valores *default*.

Para avaliar a performance foi utilizado o erro quadrático médio, obtido com uso da métrica *mean_squared_error* (MSE) da biblioteca sklearn.

### 3. Resultados

O ajuste realizado conseguiu reduzir significantemente o MSE nos dois poços analisados, o que pode ser verificado pelo alinhamento dos valores previstos pelo algoritimo e os valores obtidos na perfilagem a cabo.

|   MSE   |  cabo x LWD    |   cabo x predito   |
| :---:  |     :---:      |         :---:      |
| Poço w1| 2.130          | 0.129               |
| Poco w2| 12.304         | 0.075               |

<img src='/imagem/FE_W1 previsto-reta45.png' height="250" width="300"> <img src='/imagem/FE_W2 previsto-reta45.png' height="250" width="300">

As curvas de densidade de probabilidade mostram que a distribuição dos valores previstos está mais próxima da distribuição dos valores medidos a cabo em comparação com os valores obtidos pela perfilagem LWD. A inspeção visual das curvas a cabo, LWD e previstas, evidenciam esta constatação. 

<img src='/imagem/FE_W1-kde.png' height="300" width="300"> <img src='/imagem/FE_W2-kde.png' height="300" width="300">

Comparativo das curvas de fator foto elétrico a cabo (vermelha), LWD (verde) e prevista (azul) -POÇO W1

<img src='/imagem/curvas w1.png' height="400" width="250"> 

Comparativo das curvas de fator foto elétrico a cabo (vermelha), LWD (verde) e prevista (azul) -POÇO W2

<img src='/imagem/curva w2.png' height="400" width="250">

### 4. Conclusões

Utilizando o algoritmo XGBoost foi possível gerar uma correção do fator fotoelétrico obtido por perfilagem LWD para minimizar a influência de fatores ambientais e reproduzir o resultado de uma perfilagem a cabo com um erro relativamente pequeno. Este estudo pode ser reproduzido para englobar toda gama de parâmetros obtidos na perfilagem. Para próximos estudos é desejável ampliar o dataset de treinamento para melhorar a acurácia do algoritmo, englobando poços perfurados em diferentes contextos geológicos.

---

Matrícula: 192.671.146

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
