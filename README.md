### Melbourne Public Transport - Dashboard 

#### Introduction

In this project I aimed to create a useful dashboard that users could interact with. My goal is to make something which users find easy to engage with and enjoy using.
This dashboard aims to provide an analysis of daily passenger trends across different transport modes over time. By aggregating and visualising key metrics, such as total passengers, average monthly ridership and mode-specific trends, this dashboard offers valuable insights into passenger flow patterns. Users can filter data by date and time, transport mode, and day type to visualise and uncover trends. 

The dataset was provided by the [Department of Transport and Planning](https://www.vic.gov.au/department-transport-and-planning) and I sourced the data from [DataVic](https://discover.data.vic.gov.au/).

Dashboard:

![train_default-1](https://github.com/user-attachments/assets/9eb60ec9-a71d-4a44-887f-d3173a331505)

#### Key Insights

Using my own dashboard I was able to gather some clear insights:

- Metro Train was the most used form of public transport at 249 million total passengers, the second most was Tram at 214 million.
- The quietest month for each mode of transport were the same, August 2020.
- The major drops of passenger numbers aligned with the Victorian lockdown periods throughout 2020 - 2021.
- Post lockdown passenger counts have not recovered to pre-lockdown levels for every mode of transport except for Regional Bus. 
- Normal weekdays were the busiest types of day, followed by school holiday weekdays and then weekends.

These insights were derived very quickly so are mostly surface level, the idea being that they could be easily investigated further if there was a need.

---

#### Line Graph Visual

The visual that stands out as it is the largest and most prominent is the line graph for the number of passengers over time. It shows the fluctuation in the number of passengers clearly which guide users to areas to investigate further to derive key insights. It can also show more than one mode of transport at once depending on the user's selection on the slicers. Below I selected Metro Bus and Regional Bus to compare them both.

![image](https://github.com/user-attachments/assets/473a4366-514c-4e20-a75d-f967ee2aabfa)

![image-2](https://github.com/user-attachments/assets/4daebcd4-1b98-4618-bdfa-297457e9ce43)

---

#### Pie Graph Visual

![image-5](https://github.com/user-attachments/assets/e1d037a6-5210-4a73-bda6-41bdd046ae77)

Type of day was another variable inside the dataset. I chose to display it through this pie chart with proportions. Each section of the Piechart can be clicked and interacted with which filters the entire dashboard with that type of day just like the slicer. It greys out the other non-selected sections of the pie chart when this occurs. In future this variable and visual could be explored further if need be. 

![image-4](https://github.com/user-attachments/assets/8891ac69-73d7-4139-bcc4-c98721dbfe01)

---

#### Headline Metrics & Measures

![key_metrics-1](https://github.com/user-attachments/assets/b85277bd-ce58-49cd-84f3-2813b1fc407a)

At the top of the dashboard, I have put six metrics which change based on the selections on the page. 

Whilst they appear as simple measures, DAX code was required to produce them and produce them accurately. Due to the way the dataset was structured, I first needed to summarise the data to get the monthly totals. 

See the DAX code below to determine the busiest month accurately:

```Javascript
Busiest Month and Year = 
VAR MonthlyTotals =
    SUMMARIZE(
        'monthly_average_patronage_by_day_type_and_by_mode', 
        'monthly_average_patronage_by_day_type_and_by_mode'[Year], 
        'monthly_average_patronage_by_day_type_and_by_mode'[Month_name], 
        "TotalPax", SUM('monthly_average_patronage_by_day_type_and_by_mode'[Pax_daily])
    )

VAR MaxPax = 
    MAXX(MonthlyTotals, [TotalPax])  -- Gets the max monthly total passengers

VAR BusiestMonth =
    FILTER(MonthlyTotals, [TotalPax] = MaxPax)

RETURN 
    CONCATENATEX(BusiestMonth, 
        'monthly_average_patronage_by_day_type_and_by_mode'[Month_name] & " " & 
        'monthly_average_patronage_by_day_type_and_by_mode'[Year], 
        ", "
    )
```

Even though the dataset contained a month and year column, in order for the date and time to display correctly and chronologically, I needed to add a new column with the following code based on those two columns:

```Javascript
YearMonth = FORMAT(DATE([Year], [Month], 1), "YYYY-MM")
```

---

#### Slicers

Slicers are the key to user interactivity. I added three slicers, one for mode of transport, date selection and type of day. The reasoning for this is that it allows users to drill down further themselves and gather their own insights. I believe that this is a key strength of dashboards and PowerBI generally seems to handle them very well. 

![slicers2-1](https://github.com/user-attachments/assets/d658d72f-15b6-4aa5-a631-a04c8d0c20cc)

---

#### Conclusion

![image-1](https://github.com/user-attachments/assets/7f2afb41-9c15-4d14-ae29-08c7c12fe082)

I had a great time with this dashboard. I felt this project struck the right balance between utility and accessibility.
I learnt a lot more about PowerBI and its nuances. I ran into data aggregation issues, DAX syntax and measure errors. 
In future I could definitely improve this dashboard. I could allow for more intricate drill downs of the data, and even experiment with highlighting the dates on the graph for each of the COVID lockdowns with an on/off toggle button. I could also use icons as the slicer filters for mode of transport. There are always ways to improve and iterate over time as needed.

Thank you for taking the time to view my dashboard, I hope you got something out of it. 
If you have any questions or want to connect, feel free to reach out to me LinkedIn or GitHub.

--- 

Links:

- [Department of Transport and Planning](https://www.vic.gov.au/department-transport-and-planning) 
- [DataVic](https://discover.data.vic.gov.au/)
