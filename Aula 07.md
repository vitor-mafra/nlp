[[2024-10-29]]

### Avaliando modelos clássicos de linguagem
#### Perplexidade
A perplexidade dá uma ideia sobre incerteza/dúvida sobre a próxima palavra prevista para um modelo clássico de linguagem. Uma perplexidade baixa significa que temos um grau elevado de certeza das previsão da próxima palavra.

### n-gram
Combinações de contrações consecutivas de palavras. Um problema desses modelos clássicos de linguagem (como é o n-grama) é o de contexto. Essa classe de modelos não é capaz de capturar uma grande sequência de *tokens*, já que grandes combinações são raramente encontradas nos dados de treino. Outro problema é que o n-gram não utiliza a similaridade entre tokens - ou seja, esse modelo não consegue entender construções semânticas similares se essas similaridades não se traduzirem em termos parecidos, isto é, duas frases que utilizam sinônimos e significam coisas parecidas não serão encaradas dessa forma já que utilizam termos diferentes.

### Modelos que usam redes neurais: um início
Input: k-gram de palavras dentro de um vocabulário.
Output: uma distribuição de probabilidades de predição da próxima palavra mais provável dado um vocabulário.

#### A camada de *embedding*
Utilizaremos também uma camada para lidar com a representação vetorial das palavras em um espaço contínuo. Essa camada transforma cada palavra do vocabulário em um vetor de características de tamanho fixo, permitindo que palavras semanticamente próximas tenham representações vetoriais também próximas no espaço de _embedding_. Dessa forma, expressões contextualmente similares ficam mais facilmente identificáveis pelo modelo, tornando o processo de aprendizado mais eficaz.

Essa camada possui uma dimensionalidade _d_, que define o número de características representadas para cada palavra. Quanto maior _d_, mais informações o modelo consegue capturar sobre relações entre palavras, mas com um custo computacional maior.
#### *Lookup table*

Na camada de _embedding_, utilizamos uma _lookup table_, uma tabela de busca que mapeia cada palavra do vocabulário para um vetor específico em um espaço de dimensionalidade _d_. Essa tabela armazena os vetores que representam as palavras em formato denso, de forma que, ao receber o índice de uma palavra, a _lookup table_ retorne diretamente o vetor correspondente. Isso elimina a necessidade de usar uma codificação _one-hot_ completa, o que seria ineficiente para vocabulários grandes.

Esse processo permite que o modelo acesse rapidamente a representação vetorial de uma palavra e, ao final da camada, passe essas representações para uma função de ativação *softmax*. Essa função gera a distribuição de probabilidades para a próxima palavra, possibilitando que o modelo preveja qual é a palavra mais provável de ocorrer em sequência.

#### Treino
Utilizamos exemplos de treinamento que consistem em k-gramas de palavras retirados de um corpus não rotulado. Esses exemplos são obtidos da seguinte forma:

- Os primeiros  k - 1  palavras de cada k-grama são usadas como *features* (ou entradas) para o modelo, representando o contexto.
- A última palavra do k-grama serve como o *target* ou rótulo de classificação, representando a palavra que o modelo deve prever.

Esse método transforma cada sequência no corpus em uma série de exemplos de previsão, permitindo que o modelo aprenda a prever a próxima palavra com base em um contexto anterior.

A função de custo usada para treinar o modelo é a *cross-entropy loss*, que mede a diferença entre a distribuição de probabilidade predita pelo modelo para a próxima palavra e a distribuição real. Durante o treinamento, o modelo ajusta seus pesos para minimizar essa perda, tornando as predições cada vez mais precisas.

