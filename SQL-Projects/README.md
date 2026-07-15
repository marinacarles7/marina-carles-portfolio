# Amazon E-Commerce Analytics — SQL Portfolio Project

## Overview
This project analyzes 1 million Amazon e-commerce transactions from India to uncover patterns in product returns, revenue, customer behavior, and delivery performance. All analysis was done using SQL in Google BigQuery.

**Dataset:** Amazon E-Commerce 1M Dataset (Kaggle): https://www.kaggle.com/datasets/sharmajicoder/amazon-e-commerce               
**Tool:** Google BigQuery  
**Skills demonstrated:** Aggregations, GROUP BY, COUNTIF, CASE WHEN, SUM, AVG, bucketing, business insight write-up

---

## Dataset
The dataset contains 1,000,000 rows and 20 columns including:

| Column | Description |
|---|---|
| user_id | Unique customer identifier |
| product_id | Unique product identifier |
| category | Product category (Electronics, Beauty, Clothing, Sports, Home) |
| subcategory | Product subcategory |
| brand | Product brand |
| price | Original price |
| discount | Discount percentage |
| final_price | Price after discount |
| rating | Customer rating (1-5) |
| seller_rating | Seller rating (1-5) |
| shipping_time_days | Days taken to ship |
| location | City (Delhi, Mumbai, Bangalore, Chennai, Hyderabad) |
| device | Purchase device (Mobile App, Web, Tablet) |
| payment_method | Payment method used |
| is_returned | Whether the order was returned (TRUE/FALSE) |
| delivery_status | Delivery status (Delivered, Delayed, In Transit, Returned) |

---

## Business Questions & Findings

### Q1. At what shipping time does return rate spike?
Return rate stays flat at ~10.5% for orders delivered in 1-5 days, then nearly doubles to 20.67% at day 6. Orders taking 6+ days to ship are twice as likely to be returned.

**Recommendation:** Prioritize logistics improvements for orders at risk of exceeding 5-day delivery windows.

### Q2. Which product has the most purchases and highest return rate?
Demand is highly distributed across tens of thousands of unique products — the top product (P96731) had only 28 purchases. Product P96698 had the highest return rate at 26.92% among top products.

### Q3. Do products from low-rated sellers get returned more?
Seller rating showed almost no impact on return rate — 11.55% for sellers rated below 3 vs 11.61% above 3. Seller quality as measured by rating is not a meaningful return predictor in this dataset.

### Q4. Do low customer-rated products get returned more?
Yes — this is the strongest finding in the dataset. Products rated below 3 by customers have a 31.25% return rate compared to 10.99% for products rated 3 and above. That is nearly 3x higher.

**Recommendation:** Flag products with customer ratings below 3 for quality review. Proactively improving or delisting low-rated products could significantly reduce return volume.

### Q5. Which product category has the highest return rate?
Beauty (11.76%) and Clothing (11.74%) lead in return rate, while Electronics has the lowest at 11.27%. Differences across categories are relatively small (under 0.5 percentage points).

### Q6. Which product category drives the most revenue?
Electronics generates $6.58B in revenue — over 4x more than the next category (Home at $1.53B) — despite all categories having roughly equal order counts (~200K orders each). The difference is driven entirely by higher average price points in Electronics.

**Recommendation:** Electronics is the highest-value category and should be prioritized for inventory, marketing, and seller quality efforts.

### Q7. Which cities have the most purchases and highest return rates?
Delhi leads in total purchases (200,649) but has the lowest return rate (10.6%). Hyderabad has the fewest purchases (199,305) but the highest return rate (12.23%). Chennai and Bangalore also show elevated return rates above 12%.

**Recommendation:** Investigate fulfillment or product mix differences in Hyderabad and Chennai to understand the higher return rates.

### Q8. Does higher discount correlate with higher return rate?
No. Return rate is virtually identical across all discount buckets — 11.64% for 0-20%, 11.55% for 20-40%, and 11.64% for 40%+. Discount level does not predict returns.

### Q9. Which payment method has the highest return rate?
Return rates are nearly identical across all payment methods (11.54% to 11.65%). Payment method has no meaningful relationship with returns.

### Q10. Which device drives the most purchases and highest spend?
All three devices are almost perfectly even — Mobile App leads slightly with 333,636 purchases and $3.32B in spend, followed closely by Web and Tablet. No device stands out as a growth opportunity.

### Q11. Are delayed deliveries more likely to result in returns?
This question could not be meaningfully answered with this dataset — the `delivery_status` and `is_returned` columns are redundant. Orders marked "Returned" in delivery_status have a 100% return rate by definition, while all other statuses show 0%.

### Q12. Which brand has the worst gap between seller rating and customer rating?
All brands show a small negative gap (customer ratings slightly exceed seller ratings) ranging from -0.17 to -0.18. The gap is consistent across brands with no notable outliers.

---

## Key Takeaways

1. **Shipping time is a return risk trigger.** Return rate doubles when delivery exceeds 5 days. Keeping orders within a 5-day window should be a logistics priority.

2. **Customer rating is the strongest return predictor.** Products rated below 3 stars are returned at nearly 3x the rate of higher-rated products. Low ratings are an early warning signal worth acting on.

3. **Electronics drives outsized revenue.** Despite equal order volumes across categories, Electronics generates 4x more revenue than any other category due to higher price points — making it the most strategically important category in the catalog.

---



## Tools Used
- Google BigQuery (SQL)
- Google Cloud Storage (data upload)
- Dataset source: [Kaggle](https://www.kaggle.com)
