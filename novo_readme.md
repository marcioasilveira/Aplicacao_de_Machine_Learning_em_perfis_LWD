<!-- antes de enviar a versão final, solicitamos que todos os comentários, colocados para orientação ao aluno, sejam removidos do arquivo -->
# Aplicação de Machine Learning em perfis LWD
#### Aluno: [Márcio Albuquerque Silveira](https://github.com/marcioasilveira)
#### Orientadora: [Amanda Lemette](https://github.com/amandalemette) e [Julia Potratz](https://github.com/jupotratz).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

<!-- para os links a seguir, caso os arquivos estejam no mesmo repositório que este README, não há necessidade de incluir o link completo: basta incluir o nome do arquivo, com extensão, que o GitHub completa o link corretamente -->
- [Link para o código: Entrada de dados](https://github.com/marcioasilveira/Aplicacao_de_Machine_Learning_em_perfis_LWD/blob/main/TCC_Notebook1_entrada_de_dados.ipynb).
- [Link para o código: Aplicação do algoritmo](https://github.com/marcioasilveira/Aplicacao_de_Machine_Learning_em_perfis_LWD/blob/main/TCC_Notebook2_FE_xgb.ipynb)  

---

### Resumo

<!-- trocar o texto abaixo pelo resumo do trabalho, em português -->

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

Donec molestie, ante quis tempus consequat, mauris ante fringilla elit, euismod hendrerit leo erat et felis. Mauris faucibus odio est, non sagittis urna maximus ut. Suspendisse blandit ligula pellentesque tincidunt malesuada. Sed at ornare ligula, et aliquam dui. Cras a lectus id turpis accumsan pellentesque ut eget metus. Pellentesque rhoncus pellentesque est et viverra. Pellentesque non risus velit. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.

### Abstract <!-- Opcional! Caso não aplicável, remover esta seção -->

<!-- trocar o texto abaixo pelo resumo do trabalho, em inglês -->

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

Donec molestie, ante quis tempus consequat, mauris ante fringilla elit, euismod hendrerit leo erat et felis. Mauris faucibus odio est, non sagittis urna maximus ut. Suspendisse blandit ligula pellentesque tincidunt malesuada. Sed at ornare ligula, et aliquam dui. Cras a lectus id turpis accumsan pellentesque ut eget metus. Pellentesque rhoncus pellentesque est et viverra. Pellentesque non risus velit. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.

### 1. Introdução

Há um esforço constante na indústria do petróleo para reduzir os custos e o tempo entre a perfuração de um poço e sua entrada em produção. Ao mesmo tempo, é preciso contar com as melhores informações disponíveis para reduzir as incertezas nas tomadas de decisão. Uma das etapas necessárias na perfuração de um poço é a realização da perfilagem, que pode ser feita de duas formas, a perfilagem LWD (Logging While  Drilling), durante a perfuração, ou a perfilagem  a  cabo, realizada após a  perfuração  do  poço. Os custos associados ao tempo de sonda tornam a perfilagem a cabo muito mais caras do que as perfilagens LWD. No entanto a perfilagem LWD está sujeita a fatores ambientais e assim tende a ser menos precisa quando comparada à perfilagem a cabo. 

A proposta deste trabalho é, utilizando a base de dados de poços onde foram corridos perfis LWD e a cabo, treinar um algoritmo de aprendizado de máquina para estimar os perfis de fator foto elétrico a cabo a partir dos perfis LWD. Para isso usamos como dados de entrada os perfis LWD (gamma ray, nêutrons, densidade, caliper, e fator foto elétrico) tendo como alvo o perfil de fator fotoelétrico da perfilagem a cabo. O fator fotoelétrico é um subproduto do perfil de densidade, que é utilizado para identificação mineralógica, para definir o volume de quartzo/calcita/dolomita na rocha. O fator fotoelétrico medido em LWD é muito diferente do cabo em termos relativos.

### 2. Modelagem

Foram fornecidos dados de dois poços (w1 e w2) para treinamento e teste da rede. Os dados não são publicados por questões de confidencialidade. O coeficiente R2 entre a medida a cabo e a medida LWD é, respectivamente, -6.97 e -45.39 nos poços w1 e w2. Os gráficos comparativos entre as medidas de fator fotoelétrico medidos na perfilagem LWD e perfilagem a cabo nos dois poços mostram que as medidas feitas por LWD apresentam valores superiores, provavelmente devido a diferenças no ambiente de perfilagem.

<img src='/imagem/FE_W1-reta45.png' height="300" width="300"> <img src='/imagem/FE_W2-reta45.png' height="300" width="300">

O dataset recebido não tinha dados faltantes nem espúrios. Os dados foram escalonados e foi feito seu balanceamento. 

 Dados desbalanceados                                               Dados após o balancemanto
<img src='/imagem/desbalanceio.png' height="300" width="300"> <img src='/imagem/balanceado.png' height="300" width="300">

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

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

---

Matrícula: 123.456.789

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
