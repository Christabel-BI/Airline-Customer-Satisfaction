# Airline Customer Satisfaction Analysis: Flight Delays Report.

### Project Overview

This report investigates the relationship between flight delays and customer satisfaction for an airline company, using Dplyr, Tidyr and ggplot2 in R to derive insights and recommendations. The focus is on departure time as a critical metric for customer satisfaction.

### Executive Summary

Flight delays are a significant challenge for the airline industry, directly impacting customer satisfaction and operational efficiency. This report provides an in-depth analysis of the factors influencing departure delays, leveraging a dataset with 25,574 observations across 9 variables. Key findings reveal that nearly half of all flights (47%) are delayed, with specific patterns emerging based on flight type, purpose, and category.

### Objective

Analyze flight departure data to:
- Identify patterns and factors contributing to delays
- Provide actionable recommendations to minimize flight delays

### Key Findings

- Current Performance:
Only 53% of flights meet the industry benchmark for on-time departures (≤15 minutes from the scheduled time).
![image](https://github.com/user-attachments/assets/898e112c-9eca-46c8-a9c4-bee4c1482eee)



- Connecting vs. Direct Flights:
Delayed departures are more prevalent in connecting flights (62.5%) than in direct flights (45%), highlighting operational inefficiencies in handling transit passengers and cargo.

- Business vs. Leisure Flights:
Business flights exhibit a higher proportion of delays (60%) compared to leisure flights (44%), possibly due to scheduling flexibilities catered to business travelers.

- Flight Categories:
"City Hopper" flights have the highest number of delays (~4,800), followed by intercontinental (~4,200) and holiday flights (~1,000), emphasizing route-specific challenges.

### Recommendations

- Chartered Planes for Business Travelers:
Introduce chartered planes to reduce delays for premium-paying business customers, without disrupting schedules for other passengers.
Operational Enhancements:

- Allocate additional aircraft for short-haul and intercontinental routes to address capacity constraints.
Process Optimization:
Streamline critical processes, including immigration, refueling, and maintenance, to minimize delays.

- Future Research:
Expand data collection to include external factors like weather, crew scheduling, and airport-specific issues that impact delays, enabling a more comprehensive analysis.

### Tools Used in the Analysis

- Dplyr and tidyr were used to clean the dataset of 25,574 observations, ensuring the data was accurate and ready for analysis.
- ggplot 2 was used for data visualization.

##### Industry Standards Reference:
IATA and Bureau of Transportation Statistics guidelines provided the benchmarks for on-time and delayed flights
