# Business Insights Report

This document outlines the calculated fields built within Tableau to drive the Executive Dashboard, alongside eight critical business insights extracted directly from the sales performance data.

---

## 1. Tableau Calculated Fields Reference

To enrich the raw dataset, the following 5 calculated fields were built into the Tableau Packaged Workbook (`executives_dashboard.twbx`):

1. **Profit Margin**
   * **Formula:** `SUM([Profit]) / SUM([Sales])`
   * **Purpose:** Measures the baseline profitability efficiency of categories, segments, and regions independent of absolute volume.
2. **Cost**
   * **Formula:** `[Sales] - [Profit]`
   * **Purpose:** Provides visibility into total cost of goods sold (COGS) and operational overhead to monitor margin erosion.
3. **Average Order Value (AOV)**
   * **Formula:** `SUM([Sales]) / COUNTD([Order Id])`
   * **Purpose:** Gauges customer spending depth per transaction to help evaluate marketing and bundling performance.
4. **Return Rate**
   * **Formula:** `SUM([Return Flag]) / COUNTD([Order Id])`
   * **Purpose:** Tracks the proportion of distinct orders that resulted in product returns, pinpointing operational bottlenecks.
5. **Shipping Delay Bucket**
   * **Formula:** 
   ```tableau
     IF [Delivery Days] <= 2 THEN "0-2 Days (Fast)"
     ELSEIF [Delivery Days] <= 5 THEN "3-5 Days (Standard)"
     ELSE "6+ Days (Delayed)"
     END
     ```
   * **Purpose:** Groups order cycle times into scannable operational brackets to evaluate shipping service levels.

---

## 2. Core Business Insights

### Insight 1: Sales Trend & Seasonality
* **Observation:** Sales volumes exhibit sharp cyclical surges peaking heavily in Q4 (specifically November and December), followed by an annual drop-off in Q1.
* **Data Evidence:** Q4 sales consistently account for more than 35% of annual revenue across both 2024 and 2025, while January sales see an average decline of 45% compared to December.
* **Business Interpretation:** The business is heavily reliant on holiday shopping seasons and year-end inventory clearances. Relying on a single quarter introduces structural cash-flow risks.
* **Recommended Action:** Develop targeted "New Year, New Workspace" campaigns in Q1 focusing on Home Office setups to flatten the seasonal valley.

### Insight 2: Regional Performance Disparities
* **Observation:** The West and South regions lead heavily in absolute sales, while the North region underperforms significantly in net profitability despite moderate volume.
* **Data Evidence:** The West region maintains a healthy profit margin (~14%), while the North region shows compressed profit margins sliding under 6% due to high average shipping distances and regional discounting.
* **Business Interpretation:** High supply chain logistics costs and aggressive localized discounting are eroding margins in northern states like Punjab and Rajasthan.
* **Recommended Action:** Review the North region's distribution network to optimize freight routes and place a temporary ceiling on maximum allowable discounts to 15%.

### Insight 3: Category & Sub-Category Profitability Leaks
* **Observation:** "Furniture" acts as a massive revenue generator but is severely dragging down overall corporate margins, specifically driven by the "Tables" sub-category.
* **Data Evidence:** While Tables generate high top-line revenue, their net profit margin is negative (-8.5%), heavily contrasting with "Office Supplies" (Binders and Storage) which maintain margins above 18%.
* **Business Interpretation:** Tables are being sold at a loss due to high initial manufacturing/procurement costs combined with heavy bulk-freight shipping fees.
* **Recommended Action:** Implement a minimum order quantity (MOQ) or a flat bulk-shipping surcharge on large Furniture items like Tables to offset logistics overhead.

### Insight 4: Customer Segment Behavior
* **Observation:** The "Corporate" and "Consumer" segments generate the bulk of revenue, but the "Home Office" segment has the highest Average Order Value (AOV) and customer satisfaction scores.
* **Data Evidence:** Home Office AOV is roughly 12% higher than individual Consumers, and their average customer rating sits at 4.3/5 vs. Consumer's 3.9/5.
* **Business Interpretation:** B2B professionals buying for remote work settings prioritize premium quality and reliability over bottom-dollar pricing, making them less discount-sensitive.
* **Recommended Action:** Create tailored B2B bundle packages (e.g., premium chairs paired with storage solutions) to maximize the high-margin Home Office market.

### Insight 5: The Destructive Impact of Compounded Discounts
* **Observation:** There is a clear inflection point where high discounts completely eradicate profitability.
* **Data Evidence:** A scatter plot analysis shows that orders with a `Discount` metric greater than 20% (0.20) result in an average loss per order, dropping profit margins into negative territory.
* **Business Interpretation:** Sales teams or automated markdown campaigns are relying too heavily on aggressive price cuts to close deals, mistakenly converting high revenue volume into structural net losses.
* **Recommended Action:** Configure an automated alert or approval gate in the CRM system blocking discounts above 20% unless approved by a regional finance manager.

### Insight 6: Shipping & Delivery Performance Bottlenecks
* **Observation:** "Standard Class" shipping experiences systemic delays, with a significant volume falling into the "6+ Days (Delayed)" bucket, triggering a direct drop in customer ratings.
* **Data Evidence:** Orders assigned to the "6+ Days" bucket show an average customer rating of 2.8/5, compared to a 4.6/5 rating for "First Class" or "Same Day" delivery.
* **Business Interpretation:** Logistics delays are directly damaging brand equity and customer retention.
* **Recommended Action:** Renegotiate Service Level Agreements (SLAs) with third-party logistics (3PL) providers handling Standard Class shipments, establishing financial penalties for deliveries exceeding 5 business days.

### Insight 7: Product Return Patterns & Capital Drainage
* **Observation:** The "Technology" and "Furniture" categories suffer from the highest volume of product returns, heavily eating into quarterly profits due to reverse logistics costs.
* **Data Evidence:** Return rates for Technology items (specifically high-end electronics) sit at a steep 7.2%, compared to less than 2% for Office Supplies.
* **Business Interpretation:** High return rates in tech suggest discrepancies between online product descriptions and physical expectations, or damage sustained during transit due to improper packaging.
* **Recommended Action:** Enhance product detail pages with accurate dimensions and setup videos, and evaluate packaging constraints for fragile items.

### Insight 8: Strategic Business Risk & Opportunity
* **Observation:** "Referral" and "Organic" marketing channels yield the most profitable, high-rating customers, while "Paid Search" campaigns bring in transactional, low-margin buyers.
* **Data Evidence:** Customer lifetime values derived from Organic channels show a 15% lower return rate and a 4.1 average rating compared to Paid acquisition channels.
* **Business Interpretation:** Paid advertising is attracting discount-seeking, low-loyalty customers who drive up operational return costs.
* **Recommended Action:** Reallocate 20% of the digital marketing budget away from broad paid acquisition campaigns into customer loyalty/referral incentives.