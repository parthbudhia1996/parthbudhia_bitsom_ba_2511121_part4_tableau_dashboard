# Chart Selection & Justification Document

This document outlines the architectural and design decisions applied to the Executive Dashboard, illustrating why specific visualization frameworks were selected to answer core business questions.

---

## 1. Sales Trend over Time
* **Question Answered:** How are sales changing over time and are we experiencing predictable structural seasonality?
* **Chart Type Selected:** **Dual-Axis Line Chart with Trend Line** (Sales as Lines and Trend Line, Profit as an overlaid line).
* **Justification:** Continuous line charts are the gold standard for recognizing time-series trends and seasonal patterns. It allows leadership to immediately contrast revenue velocity against profit health over months and quarters.
* **Encodings Used:** 
  * *Columns:* `Order Date` (Truncated to Month/Year continuous)
  * *Rows:* `SUM(Sales)` and `SUM(Profit)`
  * *Color:* Orange for Sales, Blue for Profit.
* **Design Principles Applied:** Maintained continuous axes and added clean tooltips to eliminate data point clutter.
* **Mistakes Avoided:** Avoided using a 3D bar chart or a jagged area chart which obscures month-on-month variance.

## 2. Regional Performance View
* **Question Answered:** Which geographic territories and states are driving our profit margins, and where are the underperforming regions?
* **Chart Type Selected:** **Filled Map (Choropleth Map)**.
* **Justification:** A geographical map quickly directs executive focus to major physical territories.
* **Encodings Used:**
  * *Detail:* `State`, `Region`
  * *Color:* Diverging color palette (Red for less profit, Green for high profit).
  * *Label:* `State Name` and `Profit Margin`.
* **Design Principles Applied:** Used a clean, minimal map background layer to keep the data prominent.
* **Mistakes Avoided:** Avoided using pie charts over states, which creates massive visual noise and renders data impossible to compare.

## 3. Category Profitability View
* **Question Answered:** Which product categories and sub-categories drive the highest sales volume, and how does their top-line scale correlate with their bottom-line profit margins?
* **Chart Type Selected:** **TreeMap**.
* **Justification:** It is highly effective here because it allows leadership to nest a two-level categorical hierarchy (`Category` and `Sub-Category`) into a single, compact view.
* **Encodings Used:**
  * *Label:* `Category` -> `Sub-Category`
  * *Size:* `SUM(Sales)`
  * *Color:* `Profit Margin` (Diverging Color Palette)
* **Design Principles Applied:** By separating volume (Size) from efficiency (Color), the dashboard maximizes data density without inducing cognitive overload. The clear color boundary quickly isolates high-revenue but low-margin product categories (like Furniture) from highly efficient categories (like Technology).
* **Mistakes Avoided:** Avoided standard text tables, which hide critical negative variances in a wall of raw numbers.

## 4. Customer Segment Performance
* **Question Answered:** How does purchasing power and baseline satisfaction vary across Consumer, Corporate, and Home Office buyers?
* **Chart Type Selected:** **Side-by-Side Grouped Bar Chart**.
* **Justification:** It allows immediate comparison of multiple metrics (Sales, Profit) across three distinct categorical buckets on a single uniform scale.
* **Encodings Used:**
  * *Rows:* `SUM(Sales)`, `SUM(Profit)`
  * *Color:* Segment Category`Customer Segment`
* **Design Principles Applied:** Kept the layout highly scannable by applying clean whitespace buffers between the segment groups.
* **Mistakes Avoided:** Avoided using a stacked 100% bar chart, which makes reading absolute financial impacts difficult.

## 5. Shipping & Delivery Performance
* **Question Answered:** How do delivery transit delays impact customer sentiment across different shipping methods?
* **Chart Type Selected:** **Highlight Table (Heat Matrix)**.
* **Justification:** Cross-referencing `Ship Mode` against `Shipping Delay Buckets` using color intensity allows operational managers to spot severe bottlenecks instantly.
* **Encodings Used:**
  * *Rows:* `Ship Mode`
  * *Columns:* `Shipping Delay Bucket`
  * *Color:* `AVG(Customer Rating)` (Sequential Blue-to-Green alert scale)
* **Design Principles Applied:** Formatted cell values clearly to display both the count of orders and the resulting rating.
* **Mistakes Avoided:** Avoided using a standard line chart since shipping delay classes are discrete buckets, not continuous timelines.

## 6. Discount vs. Profitability Impact
* **Question Answered:** At what specific threshold does discounting behavior start destroying our profit margins?
* **Chart Type Selected:** **Scatter Plot with a Trend Line**.
* **Justification:** Scatter plots excel at showing correlations and distribution patterns across thousands of operational data points.
* **Encodings Used:**
  * *X-Axis (Columns):* `Discount` (Continuous)
  * *Y-Axis (Rows):* `Profit` (Continuous)
  * *Detail:* `Order ID`
  * *Color:* `Profit` (Orange-Blue Diverging Color Palette)
* **Design Principles Applied:** Placed a linear trend line across the distribution to instantly prove the inverse relationship between aggressive markdowns and net profit.
* **Mistakes Avoided:** Avoided grouping discounts into a pie chart, which would entirely erase the granular transaction distribution.