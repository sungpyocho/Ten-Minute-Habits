# Poisson Distribution

일정기간 동안 희귀하게 발생하는 사건 건수의 분포를 뜻한다. B(n, p)에서 p는 굉장히 작은데 n은 굉장히 크며, np=어떤 상수로 일정한 경우, 포아송 분포를 따르게 된다. 예를 들어 고속도로에서 하루 동안 발생하는 교통사고 사망자수, 희귀질병에 의한 사망자수, 책의 오탈자 수 등이 해당된다.

포아송 분포의 확률질량함수는 다음과 같다.

$$
P(X=x) = { \lambda^x \over x!} e^{-\lambda}, x=0,1,2,...
$$

이를 이항분포로 설명해 보자. np=어떤 상수에서 '어떤 상수'를 $$\lambda$$ 즉 $$np=\lambda$$라고 정의한다면

$$
\begin{align*} P(X=x) &= {}_{n} \textrm{C}_{x} p^x(1-p)^{n-x} = {n! \over {(n-x)!x!}}({\lambda \over n})^x {({1 - {\lambda \over n}})^n \over ({1 - {\lambda \over n}})^x} \\ &= {\lambda^x \over x!}{{n(n-1)...(n-x+1)} \over n^x}{({1 - {\lambda \over n}})^n \over ({1 - {\lambda \over n}})^x} \end{align*}
$$

이 때 n이 무한대로 발산한다면

$$
\begin{align*} {{n(n-1)...(n-x+1)} \over n^x} = 1 (1 - {1 \over n})... (1 - {{x-1} \over n}) &\longrightarrow 1 \\ ({1 - {\lambda \over n}})^n &\longrightarrow e^{-\lambda} \\ ({1 - {\lambda \over n}})^x &\longrightarrow 1 \end{align*}
$$

따라서 포아송분포는, 이항분포의 특수한 경우가 된다. 구체적으로는 이항분포가 $$np=\lambda, n \to \infty$$의 조건을 만족할 경우 포아송분포가 된다.

### **포아송분포의 기댓값과 분산**

$$
\begin{align*} E(X) &= \sum_{x=0}^{\infty}x{ \lambda^x \over x!} e^{-\lambda} \\ &= \lambda \sum_{x=1}^{\infty}{ \lambda^{x-1} \over (x-1)!} e^{-\lambda} \\ &= \lambda \sum_{y=0}^{\infty}{ \lambda^{y} \over y!} e^{-\lambda} \\ &= \lambda \\ Var(X) &= \sum_{x=0}^{\infty}x^2{ \lambda^x \over x!} e^{-\lambda} - \lambda^2 \\ &= \lambda \sum_{y=0}^{\infty}(y+1){ \lambda^{y} \over y!} e^{-\lambda} - \lambda^2 \\ &= \lambda (\sum_{y=0}^{\infty}y{ \lambda^{y} \over y!} + 1) - \lambda^2 \\ &= \lambda (\lambda - 1) - \lambda^2 \\ &= \lambda \end{align*}
$$

**예제문제**

> 폐암 사망 확률은 1년간 0.0001, 우연히 모인 10,000명 중 1년간 3명 이상 폐암으로 사망할 확률은?

n=10000, p=0.0001, np=1=람다이므로, 확률분포는

$$
P(X=x) = { \lambda^x \over x!} e^{-\lambda} = { e^{-1} \over x!}
$$

그렇다면 구해보자

$$
P(X \geq 3) = 1 - [P(X=0) + P(X=1) + P(X=2)] \\ = 1 - [e^{-1} + e^{-1} + { e^{-1} \over 2}] = 1 - {5 \over 2}e^{-1} = 0.08
$$

**예제문제**

> 1년 동안 규모 4 이상 지진이 평균 2회 발생

1. 1년동안 지진이 한번도 안 날 확률?

Poisson(2) -여기서 2는 람다이다- 를 따르고 있는 포아송 분포이므로 $$P(X=0) = {2^0 e^{-2}\over 0!} = e^{-2}$$

2. 1년동안 발생하는 규모 4 이상 지진 횟수의 기댓값과 분산은?

$$
E(X) = Var(X) = 2
$$

**예제문제**

> 어떤 책 10페이지 당 오타수가 1개인 경우, 한 페이지를 선택했을 때 오타가 하나도 없을 확률은?

10페이지당 오타수가 1이므로, 1페이지당 오타수는 1/10개라고 할 수 있으며, Poisson(0.1)으로 표현 가능하다. 따라서 한 페이지를 선택했을 때 오타가 하나도 없을 확률은

$$
P(X=0) = { \lambda^0 \over 0!} e^{-\lambda} = e^{-0.1}
$$

**예제문제**

* 확률변수를 2주일 동안에 발생하는 교통사고 건수로 변환해서 계산함에 주의하자. 기간을 1주일 단위로 잡게 되면 특정 1주일 동안에 교통사고 건수가 1.5건 이상 발생할 확률을 구하게 되고, 이는 2건 이상 발생할 확률을 구하게 되는 것이 된다. 따라서 구하고자 하는 확률이 달라진다.
