[[2024-10-15]]

No contexto de NLP, problemas de classificação e de geração de texto tem comportamentos totalmente diferentes. Por isso, é importante destacar que a forma de avaliação desses modelos também precisam depender da aplicação de processamento de linguagem natural em questão.

Assim como em aplicações mais gerais de aprendizado de máquina, é importante destacar que para evitar erros de viés e de variância, a separação dos dados disponíveis para treino e teste é extremamente importante.
**Treino**: usado para treinar uma rede, isto é, determinar seus pesos. Determina os parâmetros de uma rede.
**Teste**: usado para avaliar a performance de um modelo.
**Validação**: muito importante para ajustar os hiperparâmetros de uma rede.
#### Validação cruzada (*k-fold cross validation*)
Consiste em:
1) dividir o dado de treino em *k* partições (partes dos dados sem *overlap*).
2) usar k-1 partes para treinar o modelo
3) usar a parte restante para validar o modelo.
Repetir o processo acima *k* vezes, variando as partes usadas para treino e para validação. A média dessa distribuição é importante para determinar o desvio-padrão e outras informações sobre a variação do desempenho do seu modelo. Isso produz um intervalo de confiança para assegurar um determinado desempenho do seu modelo quando ele estiver em produção.
### Matriz de Confusão
Aplicada em problemas com duas classes (normalmente uma positiva e uma negativa). As linhas correspondem a classe do dados e as colunas correspondem às previsões de classes dadas por um modelo. Existem, portanto, 4 possibilidades: verdadeiros negativos, verdadeiros positivos, falsos negativos e falsos positivos - sendo, as duas primeiras as classificações acertadamente feitas pelo modelo e as duas últimas as classificações erroneamente feitas pelo modelo. Partindo desses resultados, temos algumas métricas interessantes:
#### Acurácia
**Acurácia** = quantidade de acertos / # total de predições

Note que a quantidade de acertos é dada pela soma de verdadeiros negativos e verdadeiros positivos.

Acurácia é importante porque ela consegue resumir o quanto seu modelo acertou dentre todas as classificações que ele fez. No entanto, ela não é eficaz em estimar a qualidade do modelo quando seu dado não é balanceado - isto é, se uma das classes (positiva ou negativa) é muito mais predominante que a outra. Normalmente, inclusive, no contexto de NLP temos classes muito desbalanceadas.
#### Precisão (*precision*)
Precision (for class positive) = TP / (TP + FP)
A precisão de uma classe positiva é dada dividindo as classificações corretamente feitas para a aquela classe pela soma de todas as classificações feitas como verdadeiras.

#### Revocação (*recall*)
Recall (for class positive) = TP / (TP + FN)
Note que revocação não é o contrário de precisão. No entanto, há uma relação não linear entre as duas: aumentar uma normalmente diminui a outra.
#### F-1
F-1 score (for class positive) = 2PR / (P + R)
Média harmônica entre precisão e revocação. É uma medida muito mais dura que acurácia, já que é muito menos sensível ao balanceamento dos dados - isto é, é muito mais difícil ter um F-1 score bom do que uma acurácia boa. No entanto, modelos que possuem boa F-1 score tendem a ser considerado bons.

### Métricas que foram muito usadas no contexto de NLP
#### BLEU (*Bilingual Evaluation Understudy*)
Mede a precisão, comparando sequências de palavras geradas pelo modelo com uma ou mais referências humanas. Ele avalia quantos n-gramas da saída do modelo aparecem nas referências, focando em correspondências exatas e penalizando saídas muito curtas.
#### ROUGE (*Recall-Oriented Understudy for Gisting Evaluation*)
É mais orientado ao recall se comparado ao BLEU. Ele mede a sobreposição de n-gramas, subsequências e pares de palavras entre a saída do modelo e o texto de referência. ROUGE é especialmente popular em avaliações de resumo, pois captura quão bem o modelo abrange o conteúdo da referência.

### Dificuldades de *benchmarking* em NLP
Linguagem pode ser muito ambígua e, além disso, as diferentes vivências de pessoas que vão classificar um texto podem criar classificações muito distintas. "*Ground truth*" em NLP, portanto, seria teoricamente muito caro: seria necessário pedir classificações para milhares de pessoas para tentar determinar qual seria a verdadeira classificação de um dado. No entanto, vale ressaltar que, pela dinâmica de treinamento, precisamos de *ground truth* para gerar nossos modelos: precisamos medir o erro para poder treinar e avaliar nossos modelos por meio de ajustes nos parâmetros e hiperparâmetros do nosso modelo. É importante, portanto, determinar o viés de anotadores, por exemplo, em casos de classificação, justamente porque precisamos inerentemente das anotações, mas precisamos reconhecer suas possíveis limitações e vieses. Qualidade dos dados importa (e muito). Isso é central em NLP. Compreender a criação dos dados também é central para o sucesso de um modelo.

### Desafios em NLP
#### Ambiguidade
Lidar com linguagem humana é lidar com ambiguidade. “I ate pizza with friends” and “I ate pizza with olives” são frases com significados bastante diferentes, apesar das frases serem bastante parecidas. Além disso, a variabilidade da linguagem, isto é, as diferentes formas de se dizer a mesma coisa, torna tudo ainda mais complexo. E.g.: The core message of “I ate pizza with friends” can be expressed as “friends and I shared some pizza”. 
#### Linguagem é discreta, composicional e esparsa
Apesar da linguagem ser discreta, uma palavra pode significar muitas coisas. Inclusive, pode significar coisas que outras palavras também significam. Além disso, é possível compor expressões com várias palavras que criam um significados totalmente diferente. Para criar uma frase, é necessário apenas de uma quantidade ínfima de palavras (se levarmos em consideração todas as palavras existentes). Esses fatores combinados criam um desafio gigantesco para os modelos, que somente uma quantidade absurda de dados pode resolver. Felizmente, quando falamos em linguagem também estamos falando de algo que foi bastante produzido e difundido (principalmente se você fizer o scraping da internet inteira sem precisar pagar nenhum direito autoral pra isso).