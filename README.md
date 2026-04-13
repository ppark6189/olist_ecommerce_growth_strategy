# 하우스 오브 브라질: Olist 홈앤리빙 성장 전략

브라질 Olist 이커머스 데이터를 기반으로 홈앤리빙 카테고리의 성장 전략을 분석한 프로젝트입니다. 주문, 상품, 셀러, 고객, 리뷰, 결제, 위치 데이터를 결합해 어떤 셀러 행동과 고객 행동이 매출 성장과 연결되는지 확인했습니다.

## 핵심 질문

> Olist 홈앤리빙 매출 성장을 위해 어떤 셀러와 고객 행동에 집중해야 하는가?

## 프로젝트 요약

홈앤리빙은 Olist에서 주문, 셀러, 매출 관점에서 중요한 카테고리입니다. 이 프로젝트는 홈앤리빙 카테고리의 셀러 SKU 폭, 매출 집중도, 고객 반복 구매 행동을 분석하고, 이를 바탕으로 실행 가능한 성장 전략을 제안합니다.

주요 결론은 다음과 같습니다.

- 매출은 일부 상위 셀러에게 집중되어 있습니다.
- 셀러의 SKU 수는 매출 성장과 연결되는 핵심 신호입니다.
- 프로젝트 분석에서는 18개 SKU를 셀러 성장의 실무적 기준점으로 봅니다.
- 3회 이상 구매한 고객은 리텐션 가능성이 높은 핵심 고객군입니다.
- 셀러 SKU 확장과 충성 고객 리텐션 캠페인을 함께 설계하는 것이 효과적입니다.

## 저장소 구조

```text
house_of_brazil/
|-- data/          # Olist 원본 CSV 데이터
|-- notebooks/     # 깃허브 업로드용 정리 노트북
|-- reports/       # 최종 보고서 요약
|-- src/           # 재사용 가능한 유틸리티 코드
|-- README.md      # 프로젝트 소개 문서
`-- requirements.txt
```

## 데이터

`data/` 폴더에는 Olist 공개 이커머스 데이터가 들어갑니다.

데이터 출처:

- Source: [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- Provider: Olist
- License: CC BY-NC-SA 4.0
- Use: 비상업적 분석 및 포트폴리오 목적

- `olist_orders_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_order_payments_dataset.csv`
- `olist_order_reviews_dataset.csv`
- `olist_products_dataset.csv`
- `olist_customers_dataset.csv`
- `olist_sellers_dataset.csv`
- `olist_geolocation_dataset.csv`
- `product_category_name_translation.csv`
- `product_category_name_industry_translation.csv`

## 노트북 실행 순서

정리된 노트북은 `notebooks/` 폴더에 있습니다.

1. `01_preprocess_all.ipynb`
   - 원본 CSV 로드
   - 리뷰 중복 제거
   - 주문 날짜 이상치 처리
   - 상품 카테고리 및 결제 데이터 정리
   - 위치 데이터 집계

2. `02_home_living_analysis_summary.ipynb`
   - 홈앤리빙 분석용 테이블 생성
   - 카테고리별 주문, 매출, 고객 수 집계
   - 셀러별 SKU 수와 매출 분석
   - 성장 후보 셀러 세그먼트 확인

3. `03_growth_strategy_summary.ipynb`
   - 브라질 이커머스 배송/배송비 구조 분석
   - 홈데코 카테고리 적합도 평가
   - 리텐션 전환 분석
   - 신뢰 기반 성장 전략 제안

## 실행 방법

필요한 패키지를 설치합니다.

```bash
pip install -r requirements.txt
```

노트북은 상대 경로로 데이터를 불러옵니다. `notebooks/`에서 실행할 때는 상위 폴더의 `data/`를 참조합니다.

```python
from pathlib import Path
import pandas as pd

DATA_DIR = Path("../data")

def load_csv(filename: str) -> pd.DataFrame:
    return pd.read_csv(DATA_DIR / filename)
```

현재 작업 위치가 프로젝트 루트라면 `Path("data")`를 사용하면 됩니다.

## 주요 분석 내용

### 1. 데이터 정리

- 주문 날짜를 날짜 형식으로 변환하고 비정상 순서를 보정했습니다.
- 동일 주문에서 리뷰 점수, 제목, 내용이 모두 같은 경우 중복 리뷰로 처리했습니다.
- 결제 금액이 0 이하인 비정상 결제 데이터를 점검했습니다.
- 우편번호 앞자리 기준으로 위치 데이터를 집계했습니다.

### 2. 홈앤리빙 카테고리 분석

홈앤리빙 분석에서는 다음 카테고리를 핵심 그룹으로 봅니다.

- `housewares`
- `furniture_decor`
- `bed_bath_table`

카테고리별 주문 수, 매출, 고객 수, 배송비 비중, 리뷰 점수, 반복 구매 가능성을 확인했습니다.

### 3. 셀러 성장 분석

셀러별로 다음 지표를 집계했습니다.

- 매출
- 주문 수
- SKU 수
- 판매 상품 수
- 평균 상품 가격
- 배송비 합계

분석 결과, 성장 가능성이 있는 셀러에게 SKU 확장을 유도하는 전략이 중요하다고 보았습니다. 특히 SKU 10~17개 셀러를 18개 이상으로 끌어올리는 점프업 프로그램을 추천합니다.

### 4. 고객 리텐션 분석

고객 구매 횟수별 전환을 확인해 3회 이상 구매 고객을 핵심 리텐션 대상으로 봅니다. 홈앤리빙은 교체 주기가 길기 때문에 단기 재구매율만으로 고객 이탈을 판단하기 어렵습니다.

## 전략 제안

### 셀러 전략

- SKU 10~17개 셀러를 우선 지원합니다.
- 상위 판매 상품을 기준으로 옵션, 세트 상품, 인접 상품을 확장합니다.
- 18개 이상 SKU를 목표 기준으로 설정합니다.
- 상위 셀러의 매출 집중도를 관리 지표로 추적합니다.

### 고객 전략

- 3회 이상 구매 고객을 별도 세그먼트로 관리합니다.
- 홈앤리빙 카테고리 내 인접 상품 추천을 강화합니다.
- 셀러 상품 구색 확장과 고객 프로모션을 연결합니다.
- 배송비 부담을 줄이는 혜택을 우선 검토합니다.

## 최종 산출물

- `reports/final_report_summary.md`: 최종 비즈니스 보고서 요약
- `src/utils/data_paths.py`: 재사용 가능한 데이터 로더

## 사용 기술

- Python
- pandas
- numpy
- matplotlib
- seaborn
- plotly
- Jupyter Notebook
