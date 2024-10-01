[[2024-10-01]]


### Funções de ativação e não-lineariedade

#### Sigmoide
A função Sigmoide é capaz de mapear o 0/1 (baixo/alto) em probalidade. Outra propriedade interessante e notável dessa função de ativação é que ela é derivável em todos os seus pontos. Isto é importante para determinar o nível de certeza que temos ao interpretar os resultados. Ter uma função derivável te permite analisar e avaliar um grau de certeza de um determinado resultado. Isso será muito importante em algoritmos de cálculo de gradiente. De forma abstrata, podemos encarar o valor dessa derivada como o grau de certeza que temos de um resultado dado pela Sigmoide.
#### ReLU
ReLU stands for “Rectified Linear Unit”. A ReLU não é suave, mas também é não-linear, assim como a sigmoide. ReLU é muito utilizada em casos específicos, como em redes relacionadas à visão computacional. Ela também é suave em todos os pontos, isto é, ela pode ser derivada para o cálculo de SGD (ainda que para este fator ela seja menos poderosa que a sigmoide).
#### GELU
GELU stands for “Gaussian Error Linear Unit”. Muito usada em aplicações de NLP, principalmente em redes convolucionais. 

### Convolução
A convolução é uma forma de pensar similaridade. A convolução também é uma forma de se pensar em correlação.

### Complexidade e Capacidade
Vimos anteriormente que o Perceptron tem um problema de capacidade. Ele só é capaz de modelar dados pouco complexos e não-lineares. Uma função ser mais complexa significa que é uma função que precisa de muitos parâmetros para ser descrita. Ter mais parâmetros implica, também, em uma modelagem que necessita de muitos dados durante a fase de treinamento. A complexidade de uma função que você vai gerar deve estar atrelada a quantidade de dados de treinamento disponíveis.

**Note que a complexidade se refere ao atributo de uma função. Já a capacidade está relacionada ao algoritmo que é capaz de gerar a aproximação de uma função.**
#### Minimum Description Length Principle (MDL)
MDL é uma medida não computável - é impossível calcular o MDL. O MDL é o menor modelo (no sentido de complexidade) que representa um dado. Não é interessante ter uma função de complexidade maior que o MDL. Para além de explicações como a navalha de Occam, existem provas matemáticas que mostram que é muito importante ter um modelo mais próximo ao MDL. Não existe uma fórmula de se calcular o MDL, mas é possível estimá-lo com algumas métricas. Dentre elas, destaca-se, principalmente no contexto de NLP:
#### Entropia
A entropia é capaz de medir a incerteza de uma distribuição. A entropia pode ser encarada como uma heurística de se medir o MDL. Minimizar a entropia é uma forma de buscar o MDL.
#### Cross-Entropy
A entropia cruzada é uma medida que compara duas distribuições. A cross-entropy consegue dizer qual é a discrepância entre duas distribuições. Ela te dá o menor número de *bits* necessários para transformar uma distribuição em outra. Essa é possivelmente a métrica mais usada em redes de aprendizado profundo em NLP.
#### Kullback-Leibler Divergence
A divergência Kullback-Leibler (KL) também mede a diferença entre duas distribuições. No entanto, ela é mais custosa de ser calculada - e, por isso, é menos usada. Normalmente não é usada durante o treinamento de um modelo, mas normalmente ao se comparar duas distribuições de modelos diferentes.


### Regularização
#### L2
Uma regularização muito utilizada no contexto de NLP é a Regularização L2. Regularizar é restringir a magnitude dos pesos. Ela faz isso penalizando o modelo para que ele não aumente muito os seus pesos - treinar um modelo podendo fazer isso é muito mais fácil e, por consequência, pior para o modelo. A importância de se regularizar os pesos é que com pesos de magnitude alta, a saída depende pouco da entrada - estamos overfittando!


### Stochastic Gradient Descent (SGD)
O SGD é o algoritmo base responsável por atualizar os pesos de uma rede. Ele parte de uma premissa gulosa: para encontrar a melhor configuração de pesos da rede ele sempre aplica um passo de modo a minimizar o erro. Apesar disso ter uma série de vantagens, isso também pode fazer com que seja muito difícil sair de mínimos locais. Com isso, acabamos encontrando redes subótimas que, apesar de funcionarem e serem úteis (se é que vão funcionar e ser úteis!), não representam as funções verdadeiras. É justamente isso que pode fazer com que redes se viciem e sejam treinadas de formas inesperadas, o que pode trazer problemas de causalidade e de explicabilidade.