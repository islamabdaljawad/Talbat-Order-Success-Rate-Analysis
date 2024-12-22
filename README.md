# Talbat Order Success Rate Analysis

This project focuses on analyzing and improving the success rate of orders placed on the Talbat platform. It explores various factors contributing to the success or failure of orders, such as payment methods, customer mistakes, fraud, geographic regions, and time-based patterns. Based on the findings, the project provides actionable recommendations to enhance order success rates, improve operational efficiency, and offer a better user experience.

## Table of Contents
- [Project Overview](#project-overview)
- [Data Analysis](#data-analysis)
- [SQL Queries](#sql-queries)
- [Recommendations](#recommendations)
- [Conclusion](#conclusion)
- [Technologies Used](#technologies-used)

## Project Overview

This project leverages data collected from the Talbat platform to examine the various factors that affect order success rates. By analyzing customer behavior, order reasons, and logistical patterns, the goal is to identify key areas for improvement in both the platform's functionality and its operational processes.

## Data Analysis

The project performs several types of analyses:
1. **Success Rate Analysis**: Calculation of success rates based on order status (successful or failed) and different factors (e.g., payment method, city, platform).
2. **Time-Based Analysis**: Examination of success rates by hour and month to identify peak times and potential operational challenges.
3. **Reason Analysis**: Analyzing reasons for unsuccessful orders and proposing solutions.

### SQL Queries

Here are a few SQL queries used in the project to extract insights from the Talbat order data:

#### 1. **Order Success Rate by Month and Hour**
This query calculates the success rate of orders based on the month and hour of the day.

```sql
SELECT
    MONTH(order_time) AS month,
    HOUR(order_time) AS hour,
    COUNT(*) AS total_orders,
    AVG(is_successful) * 100 AS success_rate
FROM
    orders
GROUP BY
    month, hour
ORDER BY
    month, hour;
```

This query groups orders by month and hour, calculates the total orders, and computes the average success rate for each group.

#### 2. **Success Rate by Payment Method**
To analyze the success rate based on payment methods, use the following query:

```sql
SELECT
    payment_method,
    AVG(is_successful) * 100 AS success_rate
FROM
    orders
GROUP BY
    payment_method
ORDER BY
    success_rate DESC;
```

This will give you the success rate of orders grouped by the payment method, allowing for insights into which payment types are more reliable.

#### 3. **Failure Reasons**
Understanding the reasons behind unsuccessful orders is critical for improvement. Here's a query to group orders by their failure reasons:

```sql
SELECT
    failure_reason,
    COUNT(*) AS count,
    (COUNT(*) / (SELECT COUNT(*) FROM orders) * 100) AS failure_percentage
FROM
    orders
WHERE
    is_successful = 0
GROUP BY
    failure_reason
ORDER BY
    count DESC;
```

This query identifies the most common failure reasons and calculates their percentage share of the total orders.

## Recommendations

Based on the data analysis, several recommendations have been made to improve the success rate of Talbat orders:

1. **Improve Payment Methods**: Focus on enhancing the payment process, especially online payment failures, by introducing alternative methods and improving the user interface (UI).
2. **Operational Efficiency**: Address challenges during late-night hours by improving logistics and vendor availability.
3. **Fraud Prevention**: Strengthen fraud detection mechanisms to reduce the number of fraudulent orders.
4. **Geographic Optimization**: Improve order success rates in cities with lower performance by enhancing logistics and vendor support.

## Conclusion

This project provides valuable insights into the factors that affect order success rates on the Talbat platform. By analyzing success rates across different dimensions and providing targeted recommendations, we aim to improve operational efficiency, reduce failures, and enhance the customer experience on Talbat.

## Technologies Used
- Python (Pandas, Matplotlib, NumPy)
- SQL
- Jupyter Notebooks
- Talbat Order Data

---

Feel free to customize or add more details to suit your project further!
