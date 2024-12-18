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
![image](https://github.com/user-attachments/assets/0271b8ec-f777-47a6-acba-ad27ad51fde3)

- Connecting vs. Direct Flights:
Delayed departures are more prevalent in connecting flights (62.5%) than in direct flights (45%),
highlighting operational inefficiencies in handling transit passengers and cargo.

   ![image](https://github.com/user-attachments/assets/f33bcc15-9817-4d9d-b07c-d33e4df8e06d)

- Business vs. Leisure Flights:
Business flights exhibit a higher proportion of delays (60%) compared to leisure flights (44%), possibly due to scheduling flexibilities catered to business travelers.

![image](https://github.com/user-attachments/assets/c3dea119-6f86-44b0-8079-a802b23d0240)

- Flight Categories:
"City Hopper" flights have the highest number of delays (4,800), followed by intercontinental (4,200) and holiday flights (1,000), emphasizing route-specific challenges.

![image](https://github.com/user-attachments/assets/c9b4fcd9-5149-43e8-9f18-bb35ab20e594)

### Recommendations

- Chartered Planes for Business Travelers:
Introduce chartered planes to reduce delays for premium-paying business customers, without disrupting schedules for other passengers.

- Operational Enhancements:
Allocate additional aircraft for short-haul and intercontinental routes to address capacity constraints.

- Process Optimization:
Streamline critical processes, including immigration, refueling, and maintenance, to minimize delays.

- Future Research:
Expand data collection to include external factors like weather, crew scheduling, and airport-specific issues that impact delays, enabling a more comprehensive analysis.

### Tools Used in the Analysis

- Dplyr and tidyr were used to clean, explore and manipulate the dataset of 25,574 observations, ensuring the data was accurate and ready for analysis.
- ggplot 2 was used for data visualization.

#### Industry Standards Reference:
IATA and Bureau of Transportation Statistics guidelines provided the benchmarks for on-time and delayed flights

### R codes used for Data Analysis

R```
#### call library ####

library(readxl)
library(tidyr)
library(ggplot2)
library(dplyr)  
library(skimr)
library(RColorBrewer)

#### set working directory ####
setwd("C:/Users/david/OneDrive/Documents/Airline")

#### load data ####
airline <- read_excel("airline-12.xlsx")

#### Inspect data/data preparation ####
# 27345 observations and 10 variables
str(airline)
summary(airline)

airline<- airline %>% filter(route !="NA")

airline<- airline %>% filter(departure !="NA")

airline<- airline %>% filter(kids !="error", kids !=".")

airline<- airline %>% filter(business !="NA")

#### Data manipulation ####
table(airline$departure)

airline$departure <- ifelse(airline$departure == "delay < 30min", "delay", airline$departure)
airline$departure <- ifelse(airline$departure == "delay < 90min", "delay", airline$departure)
airline$departure <- ifelse(airline$departure == "delay > 90min", "delay", airline$departure)

airline <- airline %>% mutate(ontime = ifelse(departure =="delay",1,0))

table(airline$gender)
airline$gender <- ifelse(airline$gender == "diverse", "others", airline$gender)
airline$gender <- ifelse(airline$gender == "unknown/ don't want to say", "others", airline$gender)

table(airline$connection)
airline$connection <- ifelse(airline$connection == "connecting flight", "connection", airline$connection)

summary(airline)
skim(airline)

#### Data visualization ####

#### figure 1 (Distribution of departure) ####
       airline%>%group_by(departure)%>%count(departure)

      ggplot(airline%>%group_by(departure)%>%count(departure))+
      geom_col(aes(departure, n, fill=departure))+
      geom_text(aes(departure, n, label = paste(n), vjust = -0.3, fontface ="bold"))+ 
      geom_text(aes(departure, n,label = paste(scales::percent(round(n/sum(n), digits = 2))),
      group=departure), position = position_dodge(width = .9),vjust = 1.5, size=4, color="white", fontface ="bold") +
      labs(title = "Delay and ontime flight departure", x = " ", y = "Number of flight departure") +
      scale_fill_manual(values = c("darkred", "darkgreen")) +
      theme(legend.title = element_blank(), legend.position = "bottom") +
      theme_minimal() 

#### figure 2  (Departure with connection)
       ggplot(airline, aes(x = connection, fill = departure)) + 
       geom_bar(position = "fill", width = 0.8) +
       labs(title = "Effect of connecting flights", subtitle = "on departure" , x = "connection", y = "Proportion of departure flights") +
       scale_fill_manual(values = c("darkred", "darkgreen"))+
       theme(legend.title = element_blank()) +
       theme_minimal()

#### figure 3 (Departure with Business)
      ggplot(airline, aes(x = business, fill = departure)) + 
      geom_bar(position = "fill", width = 0.8) +
      scale_fill_manual(values = c("darkred", "darkgreen")) +
      labs(title = "Departure flights", subtitle = "by business and leisure" , x = "flight", y = "Proportion of departure flights") +
      theme(legend.title = element_blank()) +
      theme_minimal() 
      
#### figure 4 (Departure with type)
      ggplot(airline, aes(x = type, fill = departure)) + 
      geom_bar(width = 0.7, position = position_dodge(0.9)) +
      scale_fill_manual(values = c("darkred", "darkgreen")) +
      labs(title = "Departure", subtitle = "by business and leisure flights", x = "flight", y = "Number of flights") +
      theme(legend.title = element_blank()) + 
      theme_minimal()
      
    

    


