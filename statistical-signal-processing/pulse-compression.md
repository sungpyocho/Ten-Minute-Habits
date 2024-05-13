# Pulse Compression



#### 송신 신호의 세기를 키우면 안되나?

짧은 CW 펄스는 유지한 채, 센서 마이크가 보내는 신호의 세기를 크게 하면 되지 않을까? 사실 신호의 세기를 무작정 크게 할 수는 없다. 컴퓨터 스피커를 생각해보자. 컴퓨터 스피커의 볼륨을 올려 지속적으로 큰 소리를 낸다면, 전력 소모도 클 것이고 스피커의 내구성에 문제가 생길 수도 있다. 애초에 큰 소리를 내기 위해 컴퓨터 스피커의 하드웨어 스팩도 좋아야 한다.

센서도 마찬가지다. 신호 세기를 키우기 위해서는, 큰 전력 소모를 버틸 수 있는 고전압의 전원과 마이크가 필요하다. 큰 소리를 내기 위해 마이크는 비싸지고, 커져야 하고, 추가적인 내구성 테스트도 필요하다. 그래서 사실 무작정 신호 세기를 키워서 SNR을 확보하겠다는 방안은 현실적이지 않다.

### 선형 주파수 변조를 통한 펄스 압축

***

#### 기본 원리

그렇다면 SNR을 확보할 수 있도록 펄스를 충분히 길게 하면서도, 거리 해상도를 희생하지 않는 방법은 없을까? 여기서 바로 펄스 압축이 등장한다. 펄스 압축의 기본 원리는 다음 두 가지이다.

* 신호의 에너지가 충분히 보존되도록, 신호를 긴 시간동안 송신
* 매치 필터(matched filtering) 후에, 상관 신호의 길이가 일반적인 CW 사인파의 신호 길이보다 작도록 신호를 설계

자동차의 ADAS 센서, 특히 레이다와 초음파에서는 펄스 압축을 위해 주로 선형 챠프(linear chirp, 주파수가 시간에 따라 일정하게 변조되는 신호)가 사용된다. 먼저 송신 신호의 길이가 T라고 하자. t=0에서 시작하고 t=T에서 끝나는 이 신호의 주파수가 캐리어 주파수 $$f_c$$를 중심으로 $$\Delta f$$만큼 선형적으로 변화한다면, 신호 $$s_c(t)$$의 식은 다음과 같이 쓸 수 있다.

$$
s_c(t) = \left\{ \begin{array}{ll} e^{i 2 \pi \left( \left( f_c \,-\, \frac{\Delta f}{2}\right) t \, + \, \frac{\Delta f}{2T}t^2 \, \right)} &\mbox{if} \; 0 \leq t < T \\ 0 &\mbox{otherwise}\end{array}\right.
$$

<details>

<summary>식의 도출 과정</summary>

신호의 주파수는 캐리어 주파수 $$f_c$$를 중심으로 $$\Delta f$$만큼 선형적으로 변화한다. 즉, 주파수는 $$f_c - \Delta f/ 2$$ (t=0)부터 $$f_c + \Delta f/ 2$$(t=T)까지 변한다. 따라서 이를 시간에 대한 함수로 나타낸다면, t 시점의 순간 주파수를 정의할 수 있다.

$$f(t) = f_c - \Delta f/2  + (\Delta f/T)t$$

순간 주파수를 시간에 대해 적분한다면, 다음과 같이 위상도 구할 수 있다.

$$\phi(t) = 2\pi\int_0^t f(t')dt' = 2\pi\int_0^t (f_c - \Delta f/2  + (\Delta f/T)t')dt' = 2\pi(f_c - \Delta f/2  + (\Delta f/{2T})t)t$$

따라서 복소수 신호 표현 $$s_c(t) = e^{i\phi(t)}$$에, 위에서 구한 위상의 식을 넣으면 신호의 식을 구할 수 있다.

참고로, 복소수 표현은 신호의 위상과 진폭을 분리해 분석할 수 있다는 이점이 있다. 또한 이 표현은 오일러 공식 $$e^{i\phi(t)} = cos(\phi(t)) + isin(\phi(t))$$에 기반한다.

</details>

위 식이 선형 주파수 변조가 된 신호로, 보통 영어로는 챠프(chirp)라고 한다. 이 챠프 신호의 위상은

$$
\phi(t) = 2\pi \left( \left( f_c \,-\, \frac{\Delta f}{2}\right) t \, + \, \frac{\Delta f}{2T}t^2 \, \right)
$$

따라서 순간 주파수(instantaneous frequency)는 정의에 따라 다음과 같이 계산된다. '잠깐, 순간 주파수는 왜 위상을 시간에 대해 미분하는거지?'라는 의문이 든다면, 별도의 글 [instantaneous-phase-and-frequency.md](instantaneous-phase-and-frequency.md "mention")을 읽어보자.&#x20;

$$
f(t) = \frac{1}{2\pi}\left[\frac{d\phi}{dt}\right ]_t = f_c-\frac{\Delta f}{2}+\frac{\Delta f}{T}t
$$

주파수가 어떻게 변하는지 보려면, 신호의 처음과 마지막의 주파수를 확인하면 된다. 신호는 t=0에 시작해 t=T에 끝나므로, 주파수는 $$f(0) = f_c - \Delta f/ 2$$ 부터 $$f(T) = f_c + \Delta f/ 2$$까지 변화한다는 것을 알 수 있다.

송신 신호 $$s_c(t)$$를 어떻게 표현할지는 알았으니, 이제는 수신 신호 $$r(t)$$를 표현해 보자. 센서의 신호는 물체에 반사되면서, 온도 및 습도 등의 다양한 영향을 받아 그 진폭이 변해 센서의 마이크로 다시 돌아오게 된다. 그렇다면 수신 신호는 송신 신호가 반사된 시간만큼 느려지고, 진폭이 변한 신호로 표현할 수 있을 것이다. 그러나 이게 끝이 아니다. 노이즈가 추가된다. 이 노이즈는 $$[f_c -\Delta f/2,f_c +\Delta f/2 ]$$ 영역에서 일정한 에너지(정확히는 power spectral density)를 갖고,  다른 영역에서는 0의 에너지를 가진다. 이를 식으로 표현해 보자.

$$
r(t) = \left\{ \begin{array}{ll} Ae^{i 2 \pi \left( \left( f_c \,-\, \frac{\Delta f}{2}\right) (t-t_r) \, + \, \frac{\Delta f}{2T}(t-t_r)^2 \, \right)} +N(t)&\mbox{if} \; t_r \leq t < t_r+T \\ N(t) &\mbox{otherwise}\end{array}\right.
$$

#### 송신 신호와 수신 신호 사이의 상호상관cross-correlation

송신 신호와 수신 신호을 수학적으로 어떻게 표현할지 알았으니, 두 신호 사이의 상관관계를 구하면 된다.&#x20;

$$
r'(t) = \begin{cases}
 A e^{2 i \pi \left (f_c \,+\, \frac{\Delta f}{2T}t\right) t} +N(t) &\mbox{if}\; -\frac{T}{2} \leq t < \frac{T}{2} \\
 N(t) &\mbox{otherwise}
\end{cases}
$$

$$
s_c'(t) = \begin{cases}
 \rho e^{2 i \pi \left (f_c \,+\, \frac{\Delta f}{2T}t\right) t} &\mbox{if}\; -\frac{T}{2} \leq t < \frac{T}{2} \\
0 &\mbox{otherwise}
\end{cases}
$$

$$
\langle s_c', r'\rangle(t) = \rho A\sqrt{T} \Lambda \left(\frac{t}{T} \right) \mathrm{sinc} \left[ \Delta f t \Lambda \left( \frac{t}{T}\right) \right] e^{2 i \pi f_c t}+N'(t)
$$

