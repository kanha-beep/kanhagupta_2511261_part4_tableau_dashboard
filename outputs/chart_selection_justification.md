# Chart Selection Justification

This document explains the major charts used in the executive dashboard and how each visual supports leadership decision-making.

## 1. KPI Cards

**What question the chart answers**  
What is the overall health of the business right now?

**Why the chart type is appropriate**  
KPI cards are the fastest way to communicate headline metrics such as sales, profit, margin, returns, discount level, and delivery speed. Executives can absorb these values in a few seconds before moving into detailed charts.

**What field is used for color, size, label, or filter**  
- Values: `SUM([sales])`, `SUM([profit])`, `Profit Margin`, `Return Rate`, `AVG([discount])`, `AVG([delivery_days])`
- Color: positive or healthy metrics in teal, risk metrics in orange or red
- Filters applied: region, category, customer segment, date, ship mode, campaign channel

**What design principle you applied**  
Clear hierarchy. KPI cards are placed at the top because the dashboard should begin with a summary before moving into diagnosis.

**What mistake you avoided**  
Avoided decorative gauge-style KPI visuals that hide exact values and waste dashboard space.

## 2. Sales Trend View

**What question the chart answers**  
How are sales and profit changing over time?

**Why the chart type is appropriate**  
A line chart is the best choice for time-series analysis because it shows direction, continuity, and turning points clearly. It helps leadership see growth patterns, seasonality, and periods of weakness or recovery.

**What field is used for color, size, label, or filter**  
- Columns: `Order Month`
- Rows: `SUM([sales])`
- Optional secondary measure: `SUM([profit])`
- Color: sales in teal, profit in a contrasting but compatible tone if shown together
- Filters: date, region, category, customer segment

**What design principle you applied**  
Chronological structure. Time stays on the horizontal axis in proper order so the story of growth is easy to follow.

**What mistake you avoided**  
Avoided using bars for long time-series analysis and avoided unordered date categories that would distort trend reading.

## 3. Regional Performance View

**What question the chart answers**  
Which regions or states contribute the most sales and profit, and where are risks concentrated?

**Why the chart type is appropriate**  
A horizontal bar chart is ideal because it allows easy ranking and precise comparison across a small set of regions. This matches the current workbook design and is clearer than a map for direct executive comparison.

**What field is used for color, size, label, or filter**  
- Dimension: `region` or `state`
- Measures: `SUM([sales])`, `SUM([profit])`, `Profit Margin`
- Optional color: `Return Rate`
- Labels: sales or profit values
- Filters: date, category, customer segment, ship mode

**What design principle you applied**  
Appropriate sorting. Regions should be sorted descending by sales or profit so the ranking is immediately visible.

**What mistake you avoided**  
Avoided cluttered maps when the purpose is ranking rather than geographic exploration, and avoided unsorted bars that weaken comparison.

## 4. Category Profitability View

**What question the chart answers**  
Which categories and sub-categories create profit, and which ones drag performance down?

**Why the chart type is appropriate**  
A bar chart is appropriate because category and sub-category performance depends on magnitude comparison. Leaders need to see which groups are materially stronger or weaker, and bars make those differences easy to read.

**What field is used for color, size, label, or filter**  
- Dimensions: `category`, `sub_category`
- Measures: `SUM([sales])`, `SUM([profit])`, `Profit Margin`
- Optional detail: `Return Rate`, `AVG([discount])`
- Color: stronger margin in teal, weak or risky performance in orange or red
- Filters: region, customer segment, date

**What design principle you applied**  
Consistent color meaning. Strong categories use positive colors, while risk areas use warning colors.

**What mistake you avoided**  
Avoided pie charts and 3D category charts, which would make precise comparison much harder.

## 5. Customer Segment View

**What question the chart answers**  
How does performance differ across customer segments?

**Why the chart type is appropriate**  
A horizontal bar chart is appropriate because the number of segments is small and comparison across them needs to be direct and precise.

**What field is used for color, size, label, or filter**  
- Dimension: `customer_segment`
- Measures: `SUM([sales])`, `SUM([profit])`, `Average Order Value`, `Profit Margin`
- Labels: sales, margin, or average order value
- Filters: region, category, date, ship mode

**What design principle you applied**  
Minimal clutter. Since the segment list is short, a simple grouped comparison is more readable than a more complex visual.

**What mistake you avoided**  
Avoided overcomplicating the segment view with unnecessary extra encodings that do not improve interpretation.

## 6. Shipping Performance View

**What question the chart answers**  
Which shipping modes and delivery delays are associated with better or worse outcomes?

**Why the chart type is appropriate**  
A stacked horizontal bar chart works well because ship modes are categorical and limited in number. It helps compare average delivery time while using color to show the shipping delay buckets.

**What field is used for color, size, label, or filter**  
- Dimension: `Ship Mode`
- Measure: `AVG([Delivery Days])`
- Color: `Shipping Delay Bucket`
- Filters: region, category, date

**What design principle you applied**  
Business interpretation first. The chart groups delivery outcomes into understandable business buckets instead of forcing leaders to interpret raw row-level detail.

**What mistake you avoided**  
Avoided overly technical logistics tables that are accurate but too dense for an executive dashboard.

## 7. Discount vs Profit View

**What question the chart answers**  
How does discounting affect profit?

**Why the chart type is appropriate**  
A scatter plot is the best choice because it shows the relationship between two numeric variables, discount and profit, directly. It helps executives see whether deeper discounts are associated with weaker economic outcomes.

**What field is used for color, size, label, or filter**  
- X-axis: `Discount`
- Y-axis: `Profit`
- Color: `Category`
- Filters: region, category, customer segment, date

**Important workbook note**  
The `Discount` field should not be left as a large summed value on the axis. It should be adjusted to a meaningful numeric scale such as average discount or discount bucket so the scatter plot reflects the real relationship clearly.

**What design principle you applied**  
Avoidance of misleading scales. The plot should preserve the true relationship between discount depth and profitability without decorative distortion.

**What mistake you avoided**  
Avoided using a pie chart or basic summary table, which would hide the relationship the business is trying to understand.

## 8. Return Analysis View

**What question the chart answers**  
Where are returns concentrated, and which business areas face the highest return risk?

**Why the chart type is appropriate**  
A horizontal bar chart is appropriate because return rate needs to be compared clearly across categories, segments, or regions.

**What field is used for color, size, label, or filter**  
- Dimension: `category`, `customer_segment`, or `region`
- Measure: `Return Rate`
- Optional supporting measure: `SUM([sales])` or `SUM([profit])`
- Color: higher return rate in stronger warning colors
- Filters: date, region, category, ship mode

**What design principle you applied**  
Risk visibility. The design makes high-return areas easy to identify immediately through ranking and color contrast.

**What mistake you avoided**  
Avoided hiding return issues inside tooltips or secondary labels where executives might miss them.

## 9. Filters And Interaction Design

**What question the chart answers**  
How can leadership move from summary to root-cause analysis without leaving the dashboard?

**Why the chart type is appropriate**  
Interactive filters and dashboard actions are not decorative features; they are functional design elements that allow users to test business questions dynamically.

**What field is used for color, size, label, or filter**  
- Filters: `Region`, `Category`, `Customer Segment`, `Order Date`, `Ship Mode`, `Campaign Channel`
- Dashboard action: selecting a region filters `Sales Trend`, `Category Profitability`, and `Return Analysis`

**What design principle you applied**  
Useful interactivity. Filters are chosen based on business decision needs rather than technical convenience.

**What mistake you avoided**  
Avoided adding too many low-value controls that would clutter the layout and slow executive use.

**Current workbook note**  
The dashboard already uses one connected action pattern where selecting a region changes the other views, which satisfies the interaction requirement for the assignment.

## Final Design Principle Summary

Across the dashboard, the design consistently applies:

- correct chart selection
- clear hierarchy
- minimal clutter
- consistent color logic
- readable titles and labels
- appropriate sorting
- useful filters and interactions
- avoidance of misleading scales
- focus on business interpretation rather than decoration
