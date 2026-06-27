# Part 4: Tableau Executive Dashboard

## Business Problem Summary

The retail leadership team needs an executive dashboard to monitor sales performance, profitability, customer segments, category performance, shipping performance, discount impact, and return patterns. The goal is not to display random charts, but to help leadership identify where the business is performing well, where margin is leaking, and where action is needed.

## Repository Structure

```text
part4_tableau_dashboard/
|-- data/
|   `-- dashboard_sales_data.xlsx
|-- tableau/
|   `-- executive_dashboard.twbx
|-- outputs/
|   |-- business_insights.md
|   |-- chart_selection_justification.md
|   `-- dashboard_story.md
|-- screenshots/
|   |-- full_dashboard.png
|   |-- sales_trend_view.png
|   |-- regional_performance_view.png
|   |-- category_profitability_view.png
|   `-- filter_interaction_view.png
`-- README.md
```

## Dataset Description

Source file:

- `data/dashboard_sales_data.xlsx`

The dataset contains `4,200` retail transaction rows across `2024` and `2025`. It includes:

- date fields: `order_date`, `ship_date`
- geographic fields: `region`, `state`, `city`
- customer fields: `customer_id`, `customer_segment`
- product fields: `category`, `sub_category`, `product_name`
- operational fields: `ship_mode`, `delivery_days`, `return_flag`
- performance fields: `sales`, `profit`, `quantity`, `discount`, `customer_rating`
- marketing field: `campaign_channel`

## Tableau Workbook Description

The Tableau packaged workbook for this submission must be saved as:

- `tableau/executive_dashboard.twbx`

The workbook should include the required supporting sheets and one final executive dashboard built for a leadership audience. In this workspace, Tableau Desktop is not available, so the workbook file still needs to be created manually in Tableau before submission.

## Connect And Inspect Data

Load `data/dashboard_sales_data.xlsx` into Tableau and use the `dashboard_sales_data` sheet as the primary table.

### Data Inspection

The dataset was loaded into Tableau from `data/dashboard_sales_data.xlsx`.

Field types confirmed in Tableau:

#### Date fields

- `Order Date`
- `Ship Date`

#### Geographic fields

- `State`
- `City`

#### Categorical fields

- `Campaign Channel`
- `Category`
- `Customer Id`
- `Customer Segment`
- `Order Id`
- `Product Name`
- `Region`
- `Ship Mode`
- `Sub Category`

#### Numerical measures

- `Sales`
- `Profit`
- `Quantity`
- `Discount`
- `Delivery Days`
- `Customer Rating`

#### Binary / flag fields

- `Return Flag` where `0 = Not Returned` and `1 = Returned`

Field setup guidance:

- Convert `order_date` and `ship_date` to `Date`
- Treat `state` and `city` as geographic drill fields
- Keep `region` as a business grouping dimension
- Keep `category`, `sub_category`, `customer_segment`, `ship_mode`, and `campaign_channel` as dimensions
- Keep `sales`, `profit`, `discount`, `quantity`, `delivery_days`, and `customer_rating` as measures
- Treat `return_flag` as a binary field where `0 = Not Returned` and `1 = Returned`

## Calculated Fields Created

Required calculated fields:

### Profit Margin

```text
SUM([profit]) / SUM([sales])
```

### Cost

```text
[sales] - [profit]
```

### Average Order Value

```text
SUM([sales]) / COUNTD([order_id])
```

### Return Rate

```text
SUM([return_flag]) / COUNT([order_id])
```

Alternative Tableau-safe version:

```text
AVG([return_flag])
```

### Shipping Delay Bucket

```text
IF [delivery_days] <= 1 THEN "1 day or less"
ELSEIF [delivery_days] <= 3 THEN "2 to 3 days"
ELSEIF [delivery_days] <= 5 THEN "4 to 5 days"
ELSE "More than 5 days"
END
```

Useful optional fields:

```text
Returned Orders Label =
IF [return_flag] = 1 THEN "Returned"
ELSE "Not Returned"
END
```

```text
Order Month = DATETRUNC('month', [order_date])
```

## Dashboard Components

The final executive dashboard should include:

- a clear title
- at least `5` charts or views
- at least `3` KPI cards
- at least `3` interactive filters
- at least `1` dashboard action or filter interaction

Recommended major views:

1. `Sales Trend`
2. `Regional Performance`
3. `Category Profitability`
4. `Customer Segment`
5. `Shipping Performance`
6. `Discount vs Profit`
7. `Return Analysis`

Current workbook direction:

- `Sales Trend` uses a line chart
- `Regional Performance` uses a horizontal bar chart
- `Customer Segment` uses a horizontal bar chart
- `Shipping Performance` uses a horizontal stacked bar chart with `Shipping Delay Bucket` on color
- `Discount vs Profit` uses a scatter plot
- `Return Analysis` uses a horizontal bar chart

Recommended KPI cards:

1. `Total Sales`
2. `Total Profit`
3. `Profit Margin`
4. `Return Rate`
5. `Average Discount`
6. `Average Delivery Days`

Current dashboard build includes one KPI summary sheet showing:

- `Profit`
- `Return Rate`
- `Sales`

## Filters And Interactions Used

Suggested filters:

- `Region`
- `Category`
- `Customer Segment`
- `Order Date`
- `Ship Mode`
- `Campaign Channel`

Recommended dashboard action:

- selecting a region in `Regional Performance` filters `Sales Trend`, `Category Profitability`, and `Return Analysis`

Current workbook behavior confirmed:

- clicking a region updates the other dashboard views
- interactive filtering is already working in the dashboard

## Visualization Design Principles

The dashboard should demonstrate:

- correct chart selection
- clear hierarchy
- minimal clutter
- consistent color usage
- proper labels
- readable titles
- appropriate sorting
- useful filters
- avoidance of misleading scales
- focus on business interpretation

Recommended design choices:

- line chart for time trend
- bar charts for ranked comparisons
- scatter plot for discount versus profit
- warning colors for weak margin or high return risk
- descending sort for category and regional comparisons
- chronological sort for date-based charts

## Key Business Insights

Headline performance from the dataset:

- Total sales: `217.0M`
- Total profit: `33.3M`
- Overall margin: `15.35%`
- Return rate: `4.55%`
- Average discount: `13.73%`
- Average delivery time: `3.59 days`

Key findings:

1. Sales grew from `106.24M` in 2024 to `110.78M` in 2025, but margin softened from `15.51%` to `15.20%`.
2. `Technology` is the strongest category with `153.90M` in sales and `18.22%` margin.
3. `Furniture` is the weakest major category with only `6.89%` margin and `7.67%` return rate.
4. Discounts above `25%` sharply compress profitability, and `35%` discount orders are loss-making.
5. `South` leads sales, while `East` has the highest return rate among regions.
6. Customer segments are relatively balanced, with margins clustered between `15.18%` and `15.51%`.
7. `Same Day` shipping has the lowest return rate, while `First Class` has the highest.
8. The biggest recovery opportunity is to improve Furniture, discount discipline, and return-heavy fulfillment patterns.

Detailed write-up:

- `outputs/business_insights.md`

## Dashboard Story Summary

The dashboard tells one connected leadership story:

The business is healthy enough to grow, but not all growth is equally valuable. Strong performance in `Technology`, balanced customer segments, and solid overall profitability are being partially offset by concentrated weakness in `Furniture`, aggressive discounting, and elevated return risk. Leadership should protect profit quality by scaling the strongest categories and fixing the areas where revenue does not translate into durable value.

Detailed narrative:

- `outputs/dashboard_story.md`

## Chart Selection Explanation

Each major chart in the dashboard is justified in:

- `outputs/chart_selection_justification.md`

That file explains:

- what question each chart answers
- why the chart type is appropriate
- what fields are used for color, size, label, or filters
- what design principle was applied
- what mistake was avoided

## Assumptions And Limitations

Assumptions:

1. `order_date` and `ship_date` are stored as Excel serial dates and should be converted to true Tableau date fields.
2. `sales` and `profit` are assumed to be in one consistent currency across the dataset.
3. `discount` is stored as a decimal fraction such as `0.25`, which should be displayed as `25%`.
4. `return_flag` is assumed to be binary with `1 = Returned` and `0 = Not Returned`.
5. `delivery_days` is assumed to represent shipping delay or fulfillment time in days.
6. `customer_rating` is assumed to be a numeric score on a 1 to 5 scale.
7. Blank `campaign_channel` values should be treated as unknown rather than deleted.

Limitations:

1. The dashboard identifies patterns but does not fully explain root causes.
2. The dataset does not include supplier metrics, return reasons, marketing spend, or carrier-level operational details.
3. Tableau Desktop is not available in this workspace, so the real packaged workbook and final authentic screenshots must still be created manually in Tableau.

## Screenshots Included

The repository includes the required screenshot files:

- `screenshots/full_dashboard.png`
- `screenshots/sales_trend_view.png`
- `screenshots/regional_performance_view.png`
- `screenshots/category_profitability_view.png`
- `screenshots/filter_interaction_view.png`

These files are currently prepared preview assets for planning and structure. Before submission, replace them with actual readable screenshots exported from the final Tableau workbook.

## Final Manual Step

Before submission, complete these last Tableau-specific steps:

1. Build the dashboard in Tableau Desktop.
2. Save the real workbook as `tableau/executive_dashboard.twbx`.
3. Export and replace the screenshots with real Tableau views.
4. Commit and push the separate repository to GitHub using the required repository name.
"# kanhagupta_2511261_part4_tableau_dashboard" 
"# kanhagupta_2511261_part4_tableau_dashboard" 
"# kanhagupta_2511261_part4_tableau_dashboard" 
