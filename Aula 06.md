[[2024-10-22]]

#### Modelos log-lineares

Modelos em que aplicamos uma função linear e depois passamos isso por uma sigmóide. Com isso, criamos um mapeamento não-linear para [0, 1].
- Each example’s label is y ∈ {0, 1}

Regra de decisão em um modelo log-linear:
- Predição == 1 se ŷ > 0.5
- Predição == 0 caso contrário
Outra forma de interpretar isso é encarar isso como uma probabilidade condicional 

Isso é (era) tipicamente usado em classificação de texto, especialmente em classificações binárias de texto. 

Perda binária na entropia-cruzada (*logistic loss*)
L logistic = −y log ŷ − (1 − y) log(1 − ŷ)

É muito importante escolher qual função de perda você vai usar para um determinado problema. Isso inclui tanto características do problema como também características do modelo escolhido.

#### *Stochastic Gradient Descent* (SGD)
1: function SGD(f(x; Θ), (x1, . . . , xn), (y1, . . . , yn), L)
	2: while stopping criteria not met do
		3: Sample a training example xi, yi
		4: Compute the loss L(f(xi ; Θ), yi)
		5: ĝ ← gradient of L(f(xi ; Θ), yi) wrt. Θ
		6: Θ ← Θ − ηĝ
	7: return Θ

O critério de parada pode ser um número máximo de iterações ou uma perda mínima aceitável.

#### Minibatch Stochastic Gradient Descent
1: function mbSGD(f(x; Θ), (x1, . . . , xn), (y1, . . . , yn), L)
	2: while stopping criteria not met do
		3: Sample m examples {(x1, y1), . . .(xm, ym)}
		4: ĝ ← 0
		5: for i = 1 to m do
			6: Compute the loss L(f(xi ; Θ), yi)
			7: ĝ ← ĝ + gradient of 1/m L(f(xi ; Θ), yi) wrt. Θ
		8: Θ ← Θ − ηĝ
9: return Θ

O tamanho do minibatch pode variar entre m=1 até m=n. No caso extremo de m=1, teríamos o próprio SGD. Valores menores permitem updates mais frequentes e uma convergência mais rápida. Valores maiores significam updates maiores (na direção da minimização) porém uma convergência mais demorada. Idealmente devemos buscar algo como 1 < m <<< n