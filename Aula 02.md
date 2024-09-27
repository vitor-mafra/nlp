[[2024-09-26]]

### Perceptron
Perceptron como função matemática: pega uma entrada e a transforma expondo isso em sua saída. Dado como vetor -> todo algoritmo depende de vetorização do dado (ainda que isso não esteja explícito ao usuário). Esse vetor é n-dimensional, com cada uma delas representando uma *feature*.

O aprendizado do Perceptron está relacionado aos seus pesos, analogamente a uma sinapse. Outro termo usado para falar desses pesos é tratar isso como parâmetros. O peso wi  determina a importância da dimensão xi em um determinado problema. No cenário mais simples, o de um único Perceptron, temos um peso associado a cada dimensão do problema. Faz-se então uma soma das dimensões ponderada pelos pesos aprendidos pelo Perceptron. Essa agregação tem como resultado uma saída que pode ser entendida como alta ou baixa. Para determinar isso, é necessário uma função de ativação que, na prática, define um limite para ativar ou não um Perceptron com base no valor da agregação anteriormente calculado. Essa função de ativação é importante, para além do Perceptron, para buscar não-lineariedade em diversos problemas. 

É importante destacar que o Perceptron sempre encontra uma separação linear - isto é, é incapaz de separar dados de forma não-linear. Essa restrição é muito importante porque a maioria dos problemas de interesse são justamente problemas não lineares. Um Perceptron é extremamente restrito em sua capacidade de transformar o dado de entrada - justamente por isso é importante destacar essa linearidade. 

O aprendizado em um único Perceptron consiste em atualizar seus pesos de modo a encontrar um conjunto de pesos que minimize um erro: este é o que chamamos de erro de treinamento. Esse processo de minimizar o erro exige essa sintonização, isto é, encontrar os melhores valores para estes pesos. Essa sintonização acontece através de uma regra de atualização que determinamos a um Perceptron. Esse processo precisa acontecer de forma repetida e numerosa, o que chamamos aqui de épocas. Após começar com os pesos aleatórios e repetir a atualização de pesos por diversas épocas, garantidamente o Perceptron encontrará essa separação (se, e somente se, o dado em questão for linearmente separável).

O problema principal do Perceptron é sua baixíssima capacidade. Uma solução encontrada para isso é combinar múltiplos Perceptrons de modo a criar diversas camadas de Percetrons que, combinados, cria uma rede com capacidade maior. Essa rede neural tem o nome de Multi Layer Perceptrons (MLPs), uma rede totalmente conectada, que contém uma camada de entrada, uma camada escondida e uma camada de saída com tantas saídas quanto a dimensão da saída precisa ter. Quanto mais capacidade (camadas escondidas) essa rede tem, mais capacidade de decorar o dado de treino (*overfitting*) ela também terá. Encontrar esse balanço é justamente a arte nesse processo. Apesar de ter uma capacidade maior se comparada a um Perceptron, uma MLP também possui um resultado linear. No entanto, no meio do processo (nas camadas ocultas), o dado é linearizado, de forma que a uma separação linear agora passa a fazer mais sentido e ter uma capacidade maior.

Um problema histórico que as MLPs enfrentaram por décadas é que, desde sempre, sua quantidade de camadas vêm sendo aumentada. O aumento de sua profundidade significa que com mais Perceptrons, menos provável é que algum deles esteja sofrendo de *overfitting*. Com muitas camadas ocultas, algoritmos de atualização de peso como o *backpropagation* deixam de funcionar - afinal é muito mais difícil encontrar quais pesos devem ser atualizado. Por conta de sua natureza, o *backpropagation* tende a culpar muito mais os pesos mais próximos da saída do que os pesos mais próximaos da entrada. Este problema é conhecido como gradientes que explodem (ou gradientes que colapsam). Por causa disso, durante muitos anos não existiam bons modelos com mais de 2 camadas ocultas.


### *Softmax*
A forma de normalizar a saída de uma rede neural é usar uma função cujo nome é *Softmax*. A Softmax recebe k entradas, uma para cada classificação possível, e probabilidades (portanto, valores entre 0 e 1) associadas a cada uma dessas possíveis classificações. Dessa forma, a soma de todos esses k valores é 1.

### *Residual Connections*
As **residual connections** são um tipo de conexão que pula uma ou mais camadas em uma rede neural e adiciona o valor de entrada diretamente à saída. Elas são usadas para facilitar o treinamento de redes neurais profundas, permitindo que a rede aprenda “resíduos” (diferenças) em vez de aprender as transformações completas. Isso ajuda a evitar o problema de ***vanishing gradients***, onde os gradientes se tornam muito pequenos para atualizar os pesos adequadamente, tornando as redes profundas mais eficientes e precisas.

### *Layer Normalization*
**Layer Normalization** é usada para estabilizar e acelerar o treinamento de redes neurais. Ela normaliza as ativações de uma camada, ajustando os valores para que tenham uma média zero e uma variância constante. Ao contrário da **Batch Normalization**, que normaliza os dados ao longo de um mini-batch (grupo de exemplos), a **Layer Normalization** normaliza os dados dentro de uma única amostra, ao longo das unidades da camada.

Isso a torna especialmente útil para modelos que processam uma única amostra por vez, como nas redes recorrentes (RNNs) e em arquiteturas baseadas em *transformers*, pois não depende do tamanho do *batch* para funcionar bem.

### *Batches Normalization*
**Batch Normalization** é uma técnica usada para melhorar o desempenho e a estabilidade das redes neurais, especialmente em redes profundas. Ela funciona normalizando as ativações de cada camada em uma rede com base na média e variância dos valores dentro de cada mini-batch de dados durante o treinamento.

Ao normalizar as ativações, a *Batch Normalization* reduz o risco de explosão ou desaparecimento de gradientes, acelera o treinamento e permite usar taxas de aprendizado maiores. Além disso, ela também atua como uma forma de regularização, ajudando a rede a generalizar melhor e a prevenir *overfitting*.

No geral, a *Batch Normalization* é eficaz para redes que processam dados em mini-*batches*, como redes convolucionais e *feed-forward*.

### Regularização
Regularização é o melhor remédio que conhecemos para combater o *overfitting*. Queremos que os modelos tenham capacidade alta, mas essa capacidade está intrinsicamente atrelada ao conjunto de dados de treino que vamos utilizar. É o regularizador que permite que um modelo não tenha capacidade do que ele deveria ter - caso isso acontecesse com determinado dado de treino, inevitavelmente cairíamos em *overfitting*.

### *Dropout*
No contexto de Deep Learning, não existe uma função mágica de regularização. Uma heurística utilizada é o *Dropout*. O dropout evita que a rede neural decore um caminho único para fazer uma classificação. No dropout, alguns conjuntos aleatórios de nós são desativados ao longo do treinamento de modo a evitar que a rede neural decore atalhos e obriga a rede a encontrar diversos caminhos diferentes para fazer uma mesma classificação de modo a melhorar sua generalização.