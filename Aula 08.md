[[2024-11-05]]

#### CBOW (*continuous bag of words*)
É um tipo de arquitetura de rede neural usada para criar embeddings de palavras, especialmente no framework Word2Vec desenvolvido pelo Google. O CBOW soma as representações do contexto.

1. **Predição de Contexto**: O CBOW é projetado para prever uma palavra-alvo (a “palavra central”) com base em um contexto de palavras ao redor dela. Ou seja, o modelo recebe como entrada um conjunto de palavras de contexto (um número fixo de palavras que cercam a palavra-alvo em uma frase) e tenta prever a palavra central a partir desse contexto.

2. **Embeddings de Palavras**: Ao treinar essa predição, o modelo CBOW aprende representações densas, ou embeddings, para cada palavra no vocabulário. Essas representações capturam relações semânticas entre as palavras, ou seja, palavras que frequentemente aparecem em contextos semelhantes acabam tendo embeddings parecidos.

3. **Objetivo de Treinamento**: O objetivo do CBOW é maximizar a probabilidade da palavra-alvo dado o contexto. Isso é feito minimizando a perda entre a palavra prevista pelo modelo e a palavra real no centro do contexto.

4. **Eficiência**: O CBOW é geralmente mais rápido de treinar do que outros modelos como o Skip-Gram (uma outra arquitetura do Word2Vec que faz o contrário, prevendo as palavras de contexto a partir de uma palavra-alvo). No entanto, o CBOW pode ser um pouco menos eficaz para capturar palavras raras, ao passo que o Skip-Gram é melhor em aprender representações para palavras menos frequentes.

#### Skip-Gram
No Skip-gram, a tarefa é prever palavras de contexto (ou palavras ao redor) com base em uma palavra-alvo. Nesse contexto, o uso de amostragem negativa (*negative sampling*) é uma técnica fundamental para tornar o treinamento mais eficiente e focado. Para cada exemplo de par correto (ou seja, uma palavra-alvo e uma palavra de contexto real que aparece próxima a ela no texto), gera-se também uma quantidade de pares negativos. Esses pares negativos são combinações de palavras que não aparecem juntas e servem para ajudar o modelo a distinguir relações reais das falsas.

O hiperparâmetro k define quantos pares negativos devem ser gerados para cada par positivo (correto). Assim:

	•	Se temos um par correto para uma palavra-alvo, o modelo gerará k pares negativos para ele.
	•	Esses pares negativos são formados com palavras aleatórias, que não têm conexão contextual com a palavra-alvo.

Isso faz com que o conjunto de pares negativos  D^-  seja k vezes maior que o conjunto de pares positivos  D^+ .

O valor de _k_ é crítico:

• **Valores Baixos de k** (por exemplo, 2 a 5): Ajudam a treinar mais rapidamente, mas podem não fornecer contraste suficiente para dados muito grandes.

• **Valores Altos de k** (por exemplo, 10 a 20): Podem aumentar a precisão das representações, mas demandam mais recursos computacionais.

Em geral, valores entre **5 e 20** são comuns, e a escolha ideal depende do tamanho do corpus e da qualidade desejada das representações.

#### FastText
O **FastText** é um modelo de _word embedding_ que, diferentemente de modelos como Word2Vec, leva em conta a **morfologia das palavras**. Em vez de atribuir um vetor único para cada palavra, o FastText representa cada palavra como uma combinação de **n-gramas de caracteres** (subpalavras).

**Bag of character n-grams**: Cada palavra é decomposta em vários n-gramas (subsequências de caracteres) de um tamanho específico - geralmente usamos *n* entre 3 e 6.

**Representação como soma de n-gramas**: A representação final de uma palavra é a soma dos embeddings desses n-gramas.

 **Melhor para línguas com muitos vocábulos e palavras raras**: Com n-gramas, o modelo consegue representar palavras raras ou desconhecidas com base em suas partes, o que é especialmente útil em idiomas ricos morfologicamente.