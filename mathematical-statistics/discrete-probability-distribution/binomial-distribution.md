# Binomial Distribution

### 베르누이 시행

공장에서 만든 제품의 불량 여부는 정상, 불량의 두 가지로 판단한다. 제 3의 선택지는 없다. 이렇듯 오직 두 가지 서로 배반적인 사건을 가지는 실험을 '베르누이 시행(Bernuili Experiment)'라고 한다. 베르누이 시행은 '동전의 앞면이 위를 향하고 있는가?', '소비자가 물건을 구입하였는가'와 같은 가능한 결과가 두 가지 뿐이고, 배반적인 실험을 말한다. 결과는 TRUE와 FALSE 중 하나의 값을 가지며, 같은 확률이 아니어도 된다.

베르누이 분포의 확률질량함수는 다음과 같다.

$$
p(X=x)=p^x(1-p)^{1-x}; x=0,1
$$

이를 확률분포표로 나타내 보면 다음과 같다.

|        | 0   | 1 | 합 |
| ------ | --- | - | - |
| p(X=x) | 1-p | p | 1 |

확률분포표에 기반해 기댓값과 분산을 구해보자.

$$
\begin{align*} E(X) &= \sum_{x=0}^1xp^x(1-p)^{1-x} \\ &=p(1-p)^0 = p \\ V(X) &= E(X^2) - E(X)^2 \\ &= \sum_{x=0}^1x^2p^x(1-p)^{1-x} - p^2 = p - p^2 = p(1-p) \end{align*}
$$

### 베르누이 분포의 적률생성함수

베르누이 분포의 적률생성함수는 다음과 같이 구할 수 있다.

$$
M(t) = E(e^{tX}) = e^{t0}(1-p) + e^{t}p = (1-p) + e^tp
$$

적률생성함수로부터 베르누이 분포의 평균과 분산을 구할 수 있다. 이를 위해 우선 한 번 미분, 두 번 미분한 뒤 t=0을 대입한 값을 구해보자.

$$
E(X) = \frac{dM_X(t)}{dt} |_{t=0} = e^tp |_{t=0} = p
$$

$$
E(X^2) = \frac{d^2M_X(t)}{d^2t} |_{t=0} = e^tp |_{t=0} = p
$$

따라서 분산의 정의에 의해

$$
Var(x) = E(X^2) - [E(X)]^2 = p - p^2 = p(1-p)
$$

### 이항 분포의 개념

이항 분포(Binomial Probability Distribution)란, 베르누이 시행이 독립적으로 시행된 후 성공(실패) 횟수의 분포를 뜻한다. 독립적으로 시행되었다는 의미는 무엇일까? 확률에서 독립이란 다음과 같이 두 사건이 함께 일어날 확률이, 두 사건의 확률의 곱으로 표현될 수 있는 것을 뜻한다.

$$
P(A \cap B) = P(A)P(B)
$$

> 정의 1. 이항 실험(binomial experiment)는 베르누이 시행을 여러 번, 독립적으로 반복한 것이다, 특징은
>
> 1. 이 실험은 n개의 동일한 시행을 한다.
> 2. 각 시행의 결과는 성공, 혹은 실패 두 가지 밖에 없다.
> 3. 한 시행의 성공 확률은 p이고, 시행마다 이 값은 동일하다. 실패 확률은 q = (1 - p)이다.
> 4. 시행은 독립적이다.
> 5. 우리가 관심을 가지는 확률변수 X는, n번의 시행동안 성공한 횟수이다.

**예제 1.**

불량품이 5%인 제품을 3개 뽑아서 불량품이 1개일 확률은?

N을 정상품, M을 불량품이라고 하자. 그러면 P(N) = 0.95, P(M) = 0.05. 3개 뽑아서 1개일 가짓수는 세 가지, 즉 MNN NMN NNM이다. X=1, X=2, X=3으로 나눠서 정리하면

$$
X=1: {}_{3} \textrm{C}_{1} ({5 \over 100})({95 \over 100})^2 \\ X=2: {}_{3} \textrm{C}_{2} ({5 \over 100})^2({95 \over 100}) \\ X=3: {}_{3} \textrm{C}_{3} ({5 \over 100})^3
$$

이를 이항분포라고 하고, 일반화시켜보자. 불량률 p, 상품의 수를 n라고 하면 불량품 수 X의 확률분포는 다음과 같다. X \~ B(n, p)

$$
P(X=x) = {}_{n} \textrm{C}_{x} p^x(1-p)^{n-x} \\ x = 0, 1, ..., n
$$

**예제 2**

아들과 딸을 낳을 확률이 0.5이고 서로 독립이라고 하자. 아이 2명을 낳았는데 세 번째 아이가 딸일 확률은?

A가 2명의 딸을 낳은 사건이라고 하고, B가 세번째 딸을 낳는 사건이라고 하자. 위에서 구하는 확률은 조건부확률이므로

$$
P(B|A) = P(B) = 0.5
$$

A와 B 사건이 서로 독립이기 때문에(즉, 앞에 딸을 몇 명 낳든 이번에 낳을 자식이 딸일 확률에는 영향을 주지 않는다), 결과적으로 구하는 확률은 P(B)와 동일하게 되어 0.5가 된다.

### **이항분포의 기댓값과 분산**

이항분포의 기댓값을 계산해 보자.

$$
\begin{align*} E(X) &= \sum_{x=0}^{n}xP(X=x) = \sum_{x=0}^{n}x{}_{n} \textrm{C}_{x} p^x(1-p)^{n-x} \\ &= \sum_{x=0}^{n}x{n! \over {x!(n-x)!}} p^x(1-p)^{n-x} \\ &= \sum_{x=1}^{n}x{n! \over {x!(n-x)!}} p^x(1-p)^{n-x};\textnormal{ 첫째항 값이 0이 되므로 }\\ &= \sum_{x=1}^{n}{n(n-1)! \over {(x-1)!(n-x)!}} p^x(1-p)^{n-x} \\ &= np\sum_{x=1}^{n}{(n-1)! \over {(x-1)!(n-x)!}} p^{x-1}(1-p)^{n-x} \\ &= np\sum_{y=0}^{n-1}{(n-1)! \over {y!(n-(y+1))!}} p^y(1-p)^{n-(y+1)};y=x-1 \\ &= np\sum_{y=0}^{n-1}{(n-1)! \over {y!(n-1-y))!}} p^y(1-p)^{n-1-y)}\\ &= np\sum_{y=0}^{n-1}{{}_{n-1}\textrm{C}_{y}} p^y(1-p)^{n-1-y};\textnormal{ formula inside Sigma follows }B(n-1, p) \\ &= np \end{align*}
$$

다음으로는, 분산을 구해보자.

$$
\begin{align*} Var(X) &= E(X^2) - E(X)^2 \\ &= \sum_{x=0}^{n}x^2{}_{n} \textrm{C}_{x} p^x(1-p)^{n-x} - (np)^2 \\ &= \sum_{x=0}^{n}x{n(n-1)! \over {(x-1)!(n-x)!}} p^x(1-p)^{n-x} - (np)^2 \\ &= np\sum_{x=1}^{n}x{(n-1)! \over {(x-1)!(n-x)!}} p^{x-1}(1-p)^{n-x} - (np)^2 \\ &= np\sum_{y=0}^{n-1}(y+1){(n-1)! \over {y!(n-(y+1))!}} p^y(1-p)^{n-(y+1)} - (np)^2 \\ &= np(\sum_{y=0}^{n-1}y{}_{n-1} \textrm{C}_{y} p^y(1-p)^{n-1-y} + 1)- (np)^2 \\ &= np((n-1)p + 1) - (np)^2;\textnormal{ 시그마 항은 다음 이항분포의 평균 }B(n-1, p) \\ &= np(np - p + 1) - (np)^2 \\ &= np(1 - p) \end{align*}
$$

증명을 쉽게 하기 위해, $$p(y)$$가 확률 함수라면 $$\Sigma p(y) = 1$$ 을 만족한다는 성질을 이용했다. 참고로 분산을 구할 때에는 $$E[Y(Y-1)]=E[Y^2]-E[Y]$$의 성질을 활용해 구할 수도 있다.

**예제 3**

> 대기업에 다니는 20명을 추려, 회사의 복리후생 정책의 변경에 대한 선호 여부를 물었다. 그랬더니 20명 중 6명이 새로운 정책을 선호한다고 답했다. 이 때 새로운 정책을 선호하는 직원의 비율 p를 추정하여라.

먼저 확률변수를 정의하자. 확률변수 X는 20명 중에 새로운 정책을 선호하는 사람의 수라고 하자. 그렇다면 이 확률변수는 n=20에 어떤 값 p를 변수로 하는 이항분포라고 생각할 수 있다. p가 어떤 값이든, 20명 중에 선호 의견을 가진 6명을 관측할 확률은 다음과 같다.

$$
P(X=6) =  {}_{20} \textrm{C}_{6} p^6(1-p)^{14}
$$

우리는 실제 관측한 20명중의 6명이라는 수가 관측될 확률을 최대로 하는 p의 값을 구할 것이다. 즉, $$P(X=6)$$을 최대로 하는 p의 값을 어떻게 찾을 수 있을까?

$${}_{20} \textrm{C}_{6}$$이 상수이고 $$ln(w)$$는 $$w$$에 대한 증가함수이므로, $$P(X=6)$$을 최대로 하는 p의 값은 $$ln[p^6(1-p)^{14}] = 6ln(p) + 14ln(1-p)$$를 최대로 하는 p의 값과 동일하다. 만약 p에 대해 미분한다면,

$$
{d[6ln(p)+14ln(1-p)] \over {dp}} = {6 \over p} - {14 \over {1-p}}
$$

따라서 $$P(X=6)$$을 최대로 하는 p의 값은 $$6ln(p) + 14ln(1-p)$$그래프의 극점, 즉 미분값이 0이 되는 지점이다. &#x20;

$$
{6 \over p} - {14 \over {1-p}} = 0
$$

즉, p=6/20이라는 결과를 얻을 수 있다. 즉, 어떠한 시행의 성공 확률을 나타내는 p의 합리적인 추정값은 우리의 표본 안의 '성공'의 비율과 동일하다. 이렇게 얻은 추정값은 최대가능도추정량(maximum likelihood estimate)이다.

### 이항 분포의 적률생성함수

이항 분포 B(n,p)를 따르는 확률변수의 적률생성함수는 다음과 같이 구할 수 있다.

$$
\begin{align*}
M(t) = E(e^{tX}) &= \sum_{x=0}^{n}e^{tx}{}_{n} \textrm{C}_{x} p^x(1-p)^{n-x} \\
&= \sum_{x=0}^{n}e^{tx}{}_{n} \textrm{C}_{x} (e^tp)^x(1-p)^{n-x} \\
&= (e^tp + 1 - p)^n
\end{align*}
$$

### **초기하 분포와 이항분포의 관계**

초기하 분포는 모집단에서 표본을 비복원 추출(뽑고 다시 넣지 않을)할 때의 분포지만, 이항분포는 표본을 복원추출했을 때의 분포라는 점에서 차이가 있다. 초기하 분포는 표본수가 커지면서 이항분포로 근사하게 된다. 이항분포는 n이 커지면 대칭적인 분포, 결과적으로는 정규분포로 근사하게 된다.
