[[2024-10-17]]

### (Mais) Desafios em NLP
#### Linguagem é composicional
Interpretar e criar textos vai muito além dos níveis de letras e palavras. Para compreender (ou criar textos) é essencial ter **memória** e **contexto**. O significado de um texto vai muito além do significado de suas palavras ou até mesmo de uma frase.

#### Os dados são muito esparsos
A possível combinação de palavras tende ao infinito. A linguagem válida é uma parte ínfima deste todo. O nosso dado, em específico, é ainda mais específico e isso cria um desafio de representação dos dados que tende a ter soluções naturais que consomem muita memória e se baseiam em representações muito esparsas dos dados. Durante a evolução de NLP, representações mais densas dos dados surgiram, mas este ainda continua sendo um desafio.

### Algoritmos simples em NLP
#### Setup
Vector x is the input, matrix W and vector b are the parameters
Θ = W, b

Objetivo: minimizar um função de perda através da escolha dos pesos W e b (*bias*). Durante o treino, comparamos a saída que estamos obtendo com a saída desejada. À partir disso, invocamos o algoritmo de ajuste de pesos
#### Classificação Binária
A entrada tem a forma de um texto (que será transformado em um vetor) e a saída é binária, isto é, 0/1, negativa/positiva. Esse texto, portanto, é mapeado para uma saída binária (spam ou não spam, comentário tóxico ou comentário não tóxico, etc). 

- f(x) : Rd → R
-  f(x) = x · w + b

#### **Como transformar texto em um vetor?** 
Essa é uma pergunta crucial em NLP e isso movimentou toda a comunidade de NLP nos últimos anos, sendo um dos principais fatores para a evolução da área nos últimos anos. 

#### O que é uma palavra?
Não existe uma definição universal para palavra na linguística e nem sempre a definição em questão é clara. Para o nosso contexto, usaremos uma definição simples (e linguisticamente bastante errada):
- Palavras são sequências de caracteres que terminam com espaço (ou com alguma pontuação)

Note que essa definição simplista não leva em consideração a semântica. 

#### Tokenização
Esse processo de **definição** do que é uma palavra é chamado de *tokenização*. Existem formas diferentes de fazer tokenização e, nos melhores algoritmos, cada língua apresenta uma forma diferente de tokenização. Especificamente em LLMs, cada um desses modelos usa um modelo de tokenização diferente (o qual foi usado durante o treinamento).

Token não é sinônimo de palavra, mas muitas vezes usaremos essa aproximação por motivos de simplificação. Note também que quando falamos de tokenização estamos tentando definir o que é uma palavra e, para isso, fazemos pouco (ou nenhum) uso de sua semântica. Até então, a parte do processo que usa a semântica é deixada para a parte da aplicação.

#### Vocabulário
Nesse contexto, trataremos o vocabulário como um conjunto de tamanho finito e fixo. O vocabulário típico de um idioma tem entre 20k e 100k tokens. Cada palavra nesse vocabulário tem um índice fixo. O vocabulário é, portanto, um conjunto de palavras estruturado de uma determinada forma de modo que é possível recuperar uma palavra por meio de seu índice.

#### Bag of Words


$$
\text{Averaged BoW} = \frac{1}{n} \sum_{i=1}^{n} v_i
$$
onde:

	•	 n  é o número total de palavras no texto,
	•	 v_i  é o vetor de embedding da  i -ésima palavra no texto,
	•	A soma é feita sobre todos os vetores de palavras no texto

-> Densificar é o caminho

####  Out-of-vocabulary (UNK) tokens
Uma coisa prática que pode acontecer é se deparar com um dado que não faz parte do vocabulário. Para essas palavras, geralmente utilizamos um token especial UNK -*unkown*- (ou OOV -*out of vocabulary*-) para determinar que a palavra em questão não fazia parte do vocabulário determinado durante o treino.