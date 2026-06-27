# parthbudhia_bitsom_ba_2511121_part4_tableau_dashboard

# Executive Sales Performance & Data Storytelling Dashboard

## 1. Business Problem Summary
This project addresses a critical strategic milestone for corporate retail leadership: shifting organizational focus from top-line sales volume to optimized bottom-line profitability. While cumulative sales maintain steady expansion, structural margins are actively compressed by unmonitored discounting strategies, category-specific operational deficits (specifically high reverse-logistics overhead and oversized freight within the Furniture lines), and fulfillment delays that degrade customer satisfaction. 

This Tableau dashboard translates distributed data into an integrated analytical framework, enabling leadership to quickly identify market opportunities, contain fiscal risks, and audit third-party logistics agreements.

---

## 2. Dataset Description & Field Mapping
The dashboard is driven by `dashboard_sales_data.xlsx` containing structural data records across operational sales windows, containing comprehensive historical transactions across 2024 and 2025.

### Dimension & Measure Classification:
* **Primary Key:** `order_id` (Unique identifier for transactions)
* **Temporal Dimensions:** `order_date`, `ship_date` (Used for continuous seasonality and timeline cycle tracking)
* **Geographic Dimensions:** `region`, `state`, `city` (Mapped hierarchically for territorial density audits)
* **Categorical Contexts:** `customer_segment`, `category`, `sub_category`, `product_name`, `ship_mode`, `campaign_channel`
* **Financial Metrics (Raw):** `sales` (Gross revenue generated), `profit` (Net operating yield), `discount` (Promotional reduction decimal marker)
* **Operational Flags & Scales:** `quantity` (Units sold), `return_flag` (Binary indicator where `1` = product returned), `delivery_days` (Fulfillment cycle window length), `customer_rating` (1–5 performance score scale)

### Critical Data Assumptions:
1. `return_flag` is a binary field where `1` indicates an item was formally returned, and `0` indicates a completed purchase.
2. The `discount` field is stored as a decimal value (e.g., `0.15` represents a 15% promotional markdown).
3. Delivery timelines (`delivery_days`) represent calendar days elapsed between `order_date` and `ship_date`.

---

## 3. Tableau Workbook Description
The packaged workbook (`tableau/executive_dashboard.twbx`) contains an enterprise-level visualization suite designed for high scannability. It functions as a cohesive single-screen executive workspace that unifies operational supply chain visibility with core financial tracking. The sheets are explicitly structured to scale smoothly across different device sizes, prioritizing visual hierarchy so executives can isolate operational metrics at a single glance.

---

## 4. Tableau Calculated Fields Reference
Five core analytical dimensions were built natively inside Tableau to empower advanced transactional slicing:

1.  **Profit Margin**
    * *Formula:* `SUM([Profit]) / SUM([Sales])`
    * *Application:* Evaluates bottom-line structural efficiency across categories independent of sheer revenue volume.
2.  **Cost**
    * *Formula:* `[Sales] - [Profit]`
    * *Application:* Establishes total cost of goods sold (COGS) and delivery baseline expenditure.
3.  **Average Order Value (AOV)**
    * *Formula:* `SUM([Sales]) / COUNTD([Order Id])`
    * *Application:* Measures absolute ticket depth per unique transaction group to test grouping behaviors.
4.  **Return Rate**
    * *Formula:* `SUM([Return Flag]) / COUNTD([Order Id])`
    * *Application:* Tracks the proportional rate of discrete returned orders to isolate processing points.
5.  **Shipping Delay Bucket**
    * *Formula:* 
      ```tableau
      IF [Delivery Days] <= 2 THEN "0-2 Days (Fast)"
      ELSEIF [Delivery Days] <= 5 THEN "3-5 Days (Standard)"
      ELSE "6+ Days (Delayed)"
      END
      ```
    * *Application:* Segments operational transit times into clean categorical windows for service level evaluation.

---

## 5. Main Dashboard Components
The production layout integrates complex cross-filtering and high-density performance visualizations:
* **High-Level KPI Summary Grid:** Interactive headline cards tracking Total Revenue ($217.0M), Total Profit ($33.3M), and Baseline Profit Margin (15.3%).
* **Sales & Profit Trend View:** Continuous dual-axis charting displaying cyclical peaks during Q4 holiday sales windows and low Q1 valleys.
* **Territorial Performance Map:** Geographically encoded choropleth dashboard charting localized state performance, tracking structural leakage across margins.
* **Category Profitability Treemap:** Hierarchical nested block maps indexing `Category` and `Sub-Category` records. Size signifies gross volume (`Sales`), while color intensity charts profitability (`Profit Margin`), immediately spotlighting high-revenue/negative-margin loss leaders like Tables.
* **Fulfillment Heat Matrix:** Cross-tabulates `Ship Mode` against `Shipping Delay Buckets` using sequential color paths to map structural drops in `Customer Rating`.
* **Discount Optimization Scatter:** Plotted transaction distributions mapping `Discount` rates against `Profit` margins, revealing the exact 20% inflection point where price reductions eliminate transaction yields.

---

## 6. Filters and Interactions Used
* **Global Structural Filters:** Drop-down filter pickers for `Region`, `Product Category`, and an `Ship Mode` range slider are configured to uniformly control all underlying dashboard worksheets cleanly.
* **Dashboard Target Action:** Selection of any specific point on the Sales Trend View Line Chart calls a localized filtering action that isolates structural metrics in the Time Series, Treemap, and Scatter plots.

---

## 7. Key Business Insights
1. **The Discount Inflection:** Promotional discounts exceeding **20%** cause absolute margins to turn negative across all business divisions. 
2. **The Tables Freight Leak:** The Tables line acts as a heavy cash-flow drain, recording a negative net profit margin due to absorbed freight delivery overhead on oversized physical items.
3. **Transit Impact on Retention:** Logistics transit windows extending beyond 5 days cause user review matrices to drop from 4.6 down to 2.8 stars, threatening regional customer retention metrics.
4. **High-Yield Segments:** Home Office buyers maintain maximum organic baseline stability, strong average ticket size, and low product return frequencies.

---

## 8. Dashboard Story Summary
The overarching narrative shows robust corporate revenue momentum that is ultimately limited by severe hidden profit erosion points. Executive focus needs to pivot decisively away from top-line revenue metrics toward micro-efficiency targets. By executing a strict 20% discount cap, implementing dynamic freight handling fees on bulk furniture items, and renegotiating shipping carrier SLAs to clear up Standard Class backlogs, the enterprise can quickly reclaim lost margins without relying heavily on expensive marketing acquisition programs.

---

## 9. Operational Assumptions & Analytic Limitations
* **Historical Base:** Analysis relies entirely on historical data records without live data links to real-time inventory management networks or direct freight fuel surcharges.
* **Fixed Margin Models:** Profit numbers assume rigid base cost structures without dynamically fluctuating raw materials metrics.
* **Future Scope Recommendation:** Phase II research should integrate customer acquisition cost (CAC) frameworks into the marketing campaign columns to map true operational channel margins.

---

## 10. Captured Documentation Artifacts
The following image verifications are archived in the root `/screenshots/` workspace to confirm layout alignment:
* `full_dashboard.png`: Complete interactive grid configuration.
* `sales_trend_view.png`: Continuous dual-axis time-series visualization.
* `regional_performance_view.png`: State-level choropleth structural visualization.
* `category_profitability_view.png`: Nested volumetric treemap chart.
* `filter_interaction_view.png`: Visual verification of interactive active filters.
