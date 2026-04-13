# 데이터

Olist CSV 파일을 이 폴더에 둡니다. 정리된 노트북은 `notebooks/` 기준 상대 경로로 이 폴더의 데이터를 불러옵니다.

## 출처

이 프로젝트의 원본 데이터는 Kaggle의 [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)에서 다운로드했습니다.

- Provider: Olist
- License: CC BY-NC-SA 4.0
- Use: 비상업적 분석 및 포트폴리오 목적

```python
DATA_DIR = Path("..") / "data"
```

필요한 파일 목록:

- `olist_customers_dataset.csv`
- `olist_geolocation_dataset.csv`
- `olist_orders_dataset.csv`
- `olist_order_items_dataset.csv`
- `olist_order_payments_dataset.csv`
- `olist_order_reviews_dataset.csv`
- `olist_products_dataset.csv`
- `olist_sellers_dataset.csv`
- `product_category_name_industry_translation.csv`
- `product_category_name_translation.csv`
