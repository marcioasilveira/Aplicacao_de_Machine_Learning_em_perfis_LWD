
# Aplicação de Machine Learning em perfis LWD
#### Aluno: [Márcio Albuquerque Silveira](https://github.com/marcioasilveira)
#### Orientadora: [Amanda Lemette](https://github.com/amandalemette) e [Julia Potratz](https://github.com/jupotratz).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- [Link para o código: Entrada de dados](https://github.com/marcioasilveira/Aplicacao_de_Machine_Learning_em_perfis_LWD/blob/main/TCC_Notebook1_entrada_de_dados.ipynb).
- [Link para o código: Aplicação do algoritmo](https://github.com/marcioasilveira/Aplicacao_de_Machine_Learning_em_perfis_LWD/blob/main/TCC_Notebook2_FE_xgb.ipynb)  

---

### Resumo

Este trabalho teve como objetivo realizar uma aplicação de aprendizado de máquina em perfis adquiridos por ferramentas LWD (Logging While Drilling) para que eles reproduzissem os resultados  do perfil fator fotoelétrico adquirido por ferramentas a cabo. Foi utlizado um dataset limitado, com apenas dois poços, e aplicado o algoritmo XGBoost. Foi possível reproduzir aproximadamente o resultado de uma perfilagem a cabo, mas com uma acurácia insuficiente para uma aplicação em situação real. A continuação deste trabalho, com um dataset mais robusto, pode alcançar uma correlação entre valores previstos e medidos mais alta.  

### 1. Introdução

Há um esforço constante na indústria do petróleo para reduzir os custos e o tempo entre a perfuração de um poço e sua entrada em produção. Ao mesmo tempo, é preciso contar com as melhores informações disponíveis para reduzir as incertezas nas tomadas de decisão. Uma das etapas necessárias na perfuração de um poço é a realização da perfilagem, que pode ser feita de duas formas: a perfilagem LWD, durante a perfuração, ou a perfilagem a cabo, realizada após a perfuração do poço. Os custos associados ao tempo de sonda tornam a perfilagem a cabo muito mais cara do que a perfilagem LWD. No entanto a perfilagem LWD está mais sujeita a fatores ambientais e assim tende a ser menos precisa quando comparada à perfilagem a cabo.

A proposta deste trabalho é, utilizando a base de dados de poços onde foram corridos perfis LWD e a cabo, treinar um algoritmo de aprendizado de máquina para estimar os perfis de fator fotoelétrico a cabo a partir dos perfis LWD. Para isso usamos como dados de entrada os perfis LWD (gamma ray, nêutrons, densidade, caliper, e fator fotoelétrico) tendo como alvo o perfil de fator fotoelétrico da perfilagem a cabo. O fator fotoelétrico é um subproduto do perfil de densidade, que é utilizado para identificação mineralógica, para definir o volume de quartzo/calcita/dolomita na rocha. O fator fotoelétrico medido em LWD é muito diferente do cabo em termos relativos.


### 2. Modelagem

Foram fornecidos dados de dois poços (w1 e w2) para treinamento e teste da rede. Os dados não são publicados por questões de confidencialidade. O coeficiente R2 entre a medida a cabo e a medida LWD é, respectivamente, -6.97 e -45.39 nos poços w1 e w2. Os gráficos comparativos entre as medidas de fator fotoelétrico medidos na perfilagem LWD e perfilagem a cabo nos dois poços mostram que as medidas feitas por LWD apresentam valores superiores, provavelmente devido a diferenças no ambiente de perfilagem.

<img src='/imagem/FE_W1-reta45.png' height="300" width="300"> <img src='/imagem/FE_W2-reta45.png' height="300" width="300">

O dataset recebido não tinha dados faltantes nem espúrios. Os dados foram escalonados e foi feito seu balanceamento. 
 
Distribuição do Dataset original.

<img src='/imagem/desbalanceio.png' height="300" width="300"> 

Dataset após o balancemanto.

<img src='/imagem/balanceado.png' height="300" width="300">

Para a predição foi utilizado o algoritmo XGBoost, com tunning dos hiperparâmetros.

### 3. Resultados

Como resultado foi obtido um coeficiente R2 entre os valores a cabo e os valores preditos para os dados de teste de 0.53 e 0.72 para w1 e w2, respectivamente.

<img src='/imagem/FE_W1 previsto-reta45.png' height="300" width="300"> <img src='/imagem/FE_W2 previsto-reta45.png' height="300" width="300">

As curvas de densidade de probabilidade mostram que a distribuição dos valores previstos está mais próxima da distribuição dos valores medidos a cabo em comparação com os valores obtidos pela perfilagem LWD.

<img src='/imagem/FE_W1-kde.png' height="300" width="300"> <img src='/imagem/FE_W2-kde.png' height="300" width="300">

Comparativo das curvas de fator foto elétrico a cabo (vermelha), LWD (verde) e prevista (azul) -POÇO W1

<img src='/imagem/curvas w1.png' height="400" width="250"> 

Comparativo das curvas de fator foto elétrico a cabo (vermelha), LWD (verde) e prevista (azul) -POÇO W2

<img src='/imagem/curva w2.png' height="400" width="250">

### 4. Conclusões

Utilizando o algoritmo XGBoost foi possível gerar uma correção do fator fotoelétrico obtido por perfilagem LWD para minimizar a influência de fatores ambientais e reproduzir o resultado de uma perfilagem a cabo. No entanto, a correlação entre a curva de fator fotoelétrico obtida neste estudo e a curva original a cabo tem um coeficiente de correlação relativamente baixo. Para próximos estudos é desejável ampliar o dataset de treinamento para melhorar a acurácia do algoritmo.

---

Matrícula: 192.671.146

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
