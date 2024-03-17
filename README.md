AtliQ Hotels Data Analysis Project 

Overview of Atliq Grands

AtliQ Grands is a reputable chain of upscale hotels catering to both luxury and business travelers, with locations in Bengaluru, Hyderabad, Delhi, and Mumbai in India.
Atliq grands has been a key player in the hospitality industry for the past twenty years

BUSINESS MODEL

![image](https://github.com/VineetPatyal/AtliQ-Hotels-Data-Analysis-Project-using-Python-Pandas-Library/assets/152878178/90549989-59d5-4eba-98dc-a2ccdd8aef32)

Category of Atliq Grands 
*Business
*luxury 

Business Hotels Name                                                                   Luxury Hotels Name 

Atliq City                                                                             Atliq Grands 

Atliq Palace                                                                           Atliq Exotica 

Atliq seasons                                                                          Atliq Blu 

                                                                                       Atliq Bay 

Type of Rooms 

1>> Standard
2>> Premium
3>> Elite
4>> Presidential

Problem Statement 

Lately, Atliq Grands team have observed a decrease in both market share and revenue within the luxury and business hotels sector, attributed to changes in competition and management strategies. To reverse this trend, the managing director has decided to use "Business and Data Intelligence" strategies. 

However, AtliQ lacks an internal team capable of analyzing their data for insights. Therefore, their revenue management team is considering hiring an external service provider to extract valuable insights from their historical data. 

Objective 

The goal is to figure out why and where there's been a drop in market share and revenue for the Atliq hotel chain. We'll delve into data to uncover insights into what's behind the decline and devise strategies to reverse the trend.

Project Steps 

Data Understanding & exploration 
Data Cleaning 
Data Transformation 
Insights Generation 

Data Understanding & exploration

In Datasets we received 5 csv files
dim_date.csv: Contains Date, month& year, week no., type of day (weekend or weekday) 
dim_hotels.csv: Contains hotel category a further subcategory in different cities 
dim_rooms.csv: Contains room class 
fact_aggregated_bookings.csv: contains successful bookings against capacity  
fact_bookings.csv: contains overall bookings

Data Cleaning  

Invalid guest records with negative values were removed, ensuring data accuracy and removing potential errors. 
Remove outliers from revenue generated and revenue realized columns with functions such as mean and std deviation.

Data Transformation 

Data Calculation: A new column has been added to derive occupancy percentage. 
Occupancy percentage is a key performance indicator in Hospitality domain. It reflects the utilization of hotel assets(rooms) aiding in strategic decisions such as Strategic pricing, Offers and resource optimization. 
Data merging: Merged data from different datasets to create comprehensive view of hotel performance

1. Create occupancy percentage column
df_agg_bookings['occ_pct'] = df_agg_bookings.apply(lambda row: row['successful_bookings']/row['capacity'], axis=1)

Convert it to a percentage value
df_agg_bookings['occ_pct'] = df_agg_bookings['occ_pct'].apply(lambda x: round(x*100, 2))
df_agg_bookings.head(3)

Insights

What is an average occupancy rate in each of the room categories?

Step 1 merge table df_agg_bookings & df_rooms

df = pd.merge(df_agg_bookings, df_rooms, left_on="room_category", right_on="room_id")
df.head(4)

Step 2 
df.groupby("room_class")["occ_pct"].mean()

Output : 
room_class
Elite           58.009756
Premium         58.028213
Presidential    59.277925
Standard        57.889643

2. Print average occupancy rate per city

df.groupby("city")["occ_pct"].mean()

output:
city
Bangalore    56.332376
Delhi        61.507341
Hyderabad    58.120652
Mumbai       57.909181

3. When was the occupancy better? Weekday or Weekend?

Step 1 : Merge 2 tables first df & df_date on date & check_in_date

Step 2 : df.groupby("day_type")["occ_pct"].mean().round(2)

Output:
day_type
weekeday    50.88
weekend     72.34

4: In the month of June, what is the occupancy for different cities

df_june_22.groupby('city')['occ_pct'].mean().round(2).sort_values(ascending=False)

output
city
Delhi        62.47
Hyderabad    58.46
Mumbai       58.38
Bangalore    56.44

5: We got new data for the month of august. Append that to existing data

latest_df = pd.concat([df, df_august], ignore_index = True, axis = 0)
latest_df.tail(10)

6. Print revenue realized per city

df_bookings_all.groupby("city")["revenue_realized"].sum()

Output:
city
Bangalore    420383550
Delhi        294404488
Hyderabad    325179310
Mumbai       668569251

7. Print month by month revenue

df_bookings_all.groupby("mmm yy")["revenue_realized"].sum()

Output: mmm yy
Jul 22    389940912
Jun 22    377191229
May 22    408375641

Recommendations

1. Weekdays Focus: Target weekdays   marketing to balance occupancy rate.
2. City Strategies: Invest in high-demand cities like Delhi.
3. Seasonal Adjustments: Align room tariff / pricing with seasonal demand.
4. Room Optimization: Adjust pricing for premium rooms.
5. Maximize City Revenue: Offer additional services, collaborate locally.
6. Monthly Revenue Analysis: Monitor trends for informed decisions.


>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>THANK YOU<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<

