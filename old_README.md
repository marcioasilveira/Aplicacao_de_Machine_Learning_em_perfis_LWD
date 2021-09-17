#RASCUNHO

# Aplicacao_de_Machine_Learning_em_perfis_LWD

Aluno: Márcio Albuquerque Silveira.

Orientadora: Amanda Lemette e Julia Potratz

Resumo

Há um esforço constante na indústria do petróleo para reduzir os custos e o tempo entre a perfuração de um poço e sua entrada em produção. Ao mesmo tempo, é preciso contar com as melhores informações disponíveis para reduzir as incertezas nas tomadas de decisão. Uma das etapas necessárias na perfuração de um poço é a realização da perfilagem, que pode ser feita de duas formas, a perfilagem LWD (Logging While  Drilling), durante a perfuração, ou a perfilagem  a  cabo, realizada após a  perfuração  do  poço. Os custos associados ao tempo de sonda tornam a perfilagem a cabo muito mais caras do que as perfilagens LWD. No entanto a perfilagem LWD está sujeita a fatores ambientais e assim tende a ser menos precisa quando comparada à perfilagem a cabo. 

A proposta deste trabalho é, utilizando a base de dados de poços onde foram corridos perfis LWD e a cabo, treinar um algoritmo de aprendizado de máquina para estimar os perfis de fator foto elétrico a cabo a partir dos perfis LWD. Para isso usamos como dados de entrada os perfis LWD (gamma ray, nêutrons, densidade, caliper, e fator foto elétrico) tendo como alvo o perfil de fator fotoelétrico da perfilagem a cabo. O fator fotoelétrico é um subproduto do perfil de densidade, que é utilizado para identificação mineralógica, para definir o volume de quartzo/calcita/dolomita na rocha. O fator fotoelétrico medido em LWD é muito diferente do cabo em termos relativos.

Foram fornecidos dados de dois poços (w1 e w2) para treinamento e teste da rede. Os dados não são publicados por questões de confidencialidade. O coeficiente R2 entre a medida a cabo e a medida LWD é, respectivamente, -6.97 e -45.39 nos poços w1 e w2. Os gráficos comparativos entre as medidas de fator fotoelétrico medidos na perfilagem LWD e perfilagem a cabo nos dois poços mostram que as medidas feitas por LWD apresentam valores superiores, provavelmente devido a diferenças no ambiente de perfilagem.

<img src='/imagem/FE_W1-reta45.png' height="300" width="300"> <img src='/imagem/FE_W2-reta45.png' height="300" width="300">

O dataset recebido não tinha dados faltantes nem espúrios. Os dados foram escalonados e foi feito seu balanceamento. Para a predição foi utilizado o algoritmo XGBoost, com tunning dos hiperparâmetros.

Como resultado foi obtido um coeficiente R2 entre os valores a cabo e os valores preditos para os dados de teste de 0.53 e 0.72 para w1 e w2, respectivamente. 

<img src='/imagem/FE_W1 previsto-reta45.png' height="300" width="300"> <img src='/imagem/FE_W2 previsto-reta45.png' height="300" width="300">

As curvas de densidade de probabilidade mostram que a distribuição dos valores previstos está mais próxima da distribuição dos valores medidos a cabo em comparação com os valores obtidos pela perfilagem LWD.

<img src='/imagem/FE_W1-kde.png' height="300" width="300"> <img src='/imagem/FE_W2-kde.png' height="300" width="300">

Para futuros trabalhos irá se ampliar a base de dados e realizar a predição de outras propriedades.

Matrícula: 192671146

Pontifícia Universidade Católica do Rio de Janeiro
Curso de Pós Graduação Business Intelligence Master





