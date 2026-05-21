# Metric & Loss Function: 관점(Viewpoint)의 설계

> **핵심 명제:** Loss function은 단순한 오차 측정 도구가 아니라,
> **모델이 어떤 통계량을 학습할지 결정하는 "관점(viewpoint)"의 설계**다.

---

## 1. Metric = "무엇을 중요하게 볼지 설계하는 함수"

수학적으로 metric $d(x, y)$는 다음 4가지 공리만 만족하면 된다.

| 공리 | 수식 | 의미 |
|---|---|---|
| Non-negativity | $d(x, y) \geq 0$ | 거리는 음수일 수 없다 |
| Identity | $d(x, y) = 0 \iff x = y$ | 같은 점일 때만 0 |
| Symmetry | $d(x, y) = d(y, x)$ | 방향에 무관 |
| Triangle inequality | $d(x, z) \leq d(x, y) + d(y, z)$ | 우회 경로는 더 멀다 |

### 💡 핵심 포인트

> Metric 자체는 **"진리"가 아니라 "관점(viewpoint)"** 이다.
>
> 즉, **어떤 metric을 쓰느냐 = 무엇을 중요하게 보느냐**

---

## 2. Loss Function = Metric을 Prediction Space에 적용한 것

예측 문제에서:

- 실제값: $y$
- 예측값: $\hat{y}$
- 거리(= loss): $L(y, \hat{y}) = d(y, \hat{y})$

어떤 $d(\cdot, \cdot)$를 선택하느냐에 따라 모델의 **성격 자체가 달라진다.**

---

### L2 Loss (MSE / RMSE)

$$
L_2(y, \hat{y}) = (y - \hat{y})^2
$$

**성질**
- 큰 오차에 매우 민감 (quadratic penalty)
- Outlier 영향이 크다

**모델 성격**
> "큰 실수는 절대 허용하지 않는다"
>
> → **평균(mean) 중심**으로 수렴

---

### L1 Loss (MAE)

$$
L_1(y, \hat{y}) = |y - \hat{y}|
$$

**성질**
- Outlier에 robust
- Linear penalty

**모델 성격**
> "대부분만 잘 맞추면 된다"
>
> → **중앙값(median) 중심**으로 수렴

---

## 3. 핵심 연결: "Loss = Metric Design"

| Loss 선택 | 최적해가 수렴하는 통계량 | 모델의 관점 |
|---|---|---|
| **L2** (MSE) | 평균 $\mathbb{E}[Y \mid X]$ | "큰 실수 = 치명적" |
| **L1** (MAE) | 중앙값 $\mathrm{median}(Y \mid X)$ | "전체적으로 잘 맞으면 OK" |
| **Quantile loss** | 분위수 $Q_\tau(Y \mid X)$ | "$\tau$-분위수 추정" |
| **Huber loss** | 평균과 중앙값의 절충 | "Robust한 평균" |

### 최종 명제

> Loss function은 단순한 **"틀린 정도의 측정"** 이 아니라,
>
> **"모델이 어떤 통계를 대표값으로 학습할지 결정하는 설계 도구"** 다.

수식으로 정리하면, 모델은 다음을 푼다:

$$
\hat{f}(x) = \arg\min_{f} \; \mathbb{E}\!\left[\, L(Y, f(X)) \,\right]
$$

이때 $L$의 선택이 곧 $\hat{f}(x)$가 무엇이 될지를 결정한다.

- $L = L_2 \;\Longrightarrow\; \hat{f}(x) = \mathbb{E}[Y \mid X=x]$
- $L = L_1 \;\Longrightarrow\; \hat{f}(x) = \mathrm{median}(Y \mid X=x)$

---

**TL;DR**
> Loss function을 고른다 = **세상을 어떤 렌즈로 볼지** 고른다.
