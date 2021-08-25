#RASCUNHO

# Aplicacao_de_Machine_Learning_em_perfis_LWD

Aluno: Márcio Albuquerque Silveira.

Orientadora: Amanda Lemette e Julia Potratz

Resumo

Há um esforço constante na indústria do petróleo para reduzir os custos e o tempo entre a perfuração de um poço e sua entrada em produção. Ao mesmo tempo, é preciso contar com as melhores informações disponíveis para reduzir as incertezas nas tomadas de decisão. Uma das etapas necessárias na perfuração de um poço é a realização da perfilagem, que pode ser feita de duas formas, a perfilagem LWD (Logging While  Drilling), durante a perfuração, ou a perfilagem  a  cabo, realizada após a  perfuração  do  poço. Os custos associados ao tempo de sonda tornam a perfilagem a cabo muito mais caras do que as perfilagens LWD. No entanto a perfilagem LWD está sujeita a fatores ambientais e assim tende a ser menos precisa quando comparada à perfilagem a cabo. Para redução de custo e aceleração da entrada em operação dos poços, estamos deixando de usar perfis a cabo, mantendo somente a perfilagem LWD.

A proposta deste trabalho é, utilizando a base de dados de poços onde foram corridos perfis LWD e a cabo, treinar um algoritmo de aprendizado de máquina para estimar os perfis de fator foto elétrico a cabo a partir dos perfis LWD. Para isso trabalhamos tendo como dados de entrada os perfis LWD (gamma ray, nêutrons, densidade, caliper, e fator foto elétrico) tendo como alvo o perfil de fator fotoelétrico da perfilagem a cabo.

O fator fotoelétrico é um subproduto do perfil de densidade, que é utilizado para identificação mineralógica, para definir o volume de quartzo/calcita/dolomita na rocha. 
O coeficiente R2 do fator fotoelétrico dos valores medidos por perfil a cabo e LWD eram de XXX. Utilizando um modelo XGBoost, com ajuste dos hiperparâmetros foi possível alcançar um coeficiente R2 de XXXX.

Matrícula: 192671146

Pontifícia Universidade Católica do Rio de Janeiro
Curso de Pós Graduação Business Intelligence Master
