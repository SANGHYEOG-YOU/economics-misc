# Modern Portfolio Theory (MPT)

Harry Markowitz(1952)에 의해 제안된 이론으로, 개별 자산의 위험보다는 여러 자산이 결합된 **포트폴리오 전체의 위험과 수익의 관계**에 집중합니다.

## 1. 핵심 개념
- **리스크-수익 상충 관계 (Risk-Return Trade-off)**: 높은 수익을 기대하려면 필연적으로 높은 위험을 감수해야 함을 수학적으로 정의합니다.
- **분산 효과 (Diversification)**: 자산 간의 상관계수가 1보다 작을 때, 포트폴리오의 전체 위험(변동성)이 개별 자산 위험의 가중 평균보다 낮아지는 현상입니다.
- **효율적 투자선 (Efficient Frontier)**: 동일한 리스크 수준에서 최대 수익을 제공하는 최적 포트폴리오들의 집합입니다.

## 2. 수식 체계 (Mathematical Framework)

자산이 $n$개인 포트폴리오에서 자산 $i$의 비중을 $w_i$, 기대수익률을 $E(R_i)$, 표준편차를 $\sigma_i$라고 할 때:

### 포트폴리오 기대수익률
$$E(R_p) = \sum_{i=1}^{n} w_i E(R_i)$$

### 포트폴리오 분산 (Risk)
$$\sigma_p^2 = \sum_{i=1}^{n} \sum_{j=1}^{n} w_i w_j \sigma_i \sigma_j \rho_{ij}$$
*(여기서 $$\rho_{ij}$$ 는 자산 $i$ 와 $j$ 의 상관계수)*

## 3. 최적 포트폴리오 선정
- **Minimum Variance Portfolio (MVP)**: 리스크를 최소화하는 지점입니다.
- **Sharpe Ratio Maximize**: 무위험 자산이 존재할 때, 자산 배분의 효율성을 나타내는 샤프 지수($\frac{E(R_p) - R_f}{\sigma_p}$)가 최대가 되는 접점 포트폴리오(Tangency Portfolio)를 찾습니다.

## 4. 한계점 및 확장
- **정규분포 가정**: 실제 금융 데이터는 'Fat-tail'(두꺼운 꼬리) 분포를 보이는 경우가 많아, VaR(Value at Risk)나 QRF(Quantile Regression Forest) 등을 통한 정교한 리스크 관리가 추가로 요구됩니다.
- **매개변수 민감도**: 기대수익률과 공분산 추정치에 따라 최적 비중이 크게 변하는 단점이 있습니다.
