# LOOKER E-Commerce

## Executive Summary  
This project uses Looker E-Commerce Dataset, publicly available on Kaggle. 
The dataset is based on a modern retail e-commerce store which has multiple interconnected tables that reflect real-world business operations. For this analysis, the data files which include Orders, Products, Users, Inventory items, Order Items, Events and distribution centers were used to explore customer behavior, product performance, and operational efficiency.

#### Data Limitations  
The dataset is artificially generated, thus not representing real customer behaviors or trends.

#### Objectives  
Uncover sales trends across regions and analyze customer behavior.

#### Data Sets
- Open-Source Looker E-Commerce dataset from Kaggle which includes data on:  
  - Orders: _125,226 rows_
  - Products: _29,120 rows_
  - Users: _100,000 rows_
  - Inventory items: _490,705 rows_
  - Order items: _181,759 rows_
  - Events: _2,431,963 rows_
  - Distribution Centers: _10 rows_

#### Analysis Criteria and Methods Used
- Data cleaning using Python _(Jupyter notebooks)_.
- Relevant data sets merged into **A single data set**.
- Linear Regression in **Python** and relevant libraries _(scikit-learn)._
- Clustering in Python Using k-Means
- Time-Series analysis and Stationarity testing _(Dickey-Fuller test)_
- Visualizing important data using python and Tableau.

## Analysis
Top 2 countries with most revenues are China and the USA.  
![Screenshot 2025-06-09 092051](https://github.com/user-attachments/assets/d2254c1b-58a9-49b2-9176-37c5b55bb00f)  

###### tableau visuals  
There seems to be little to no difference in the delivery time and processing based on different Locations.  
![average processing and delivery](https://github.com/user-attachments/assets/e07bb424-6791-46bf-b906-ccf22b948d3b)  

###### Python Code:
```
# creating heatmap data
order_heatmap_data = df_orders9.pivot_table(
    index='distribution_center',
    values=['processing_time', 'delivery_time'],
    aggfunc='mean'
).reindex(['Memphis TN', 'Chicago IL', 'Houston TX', 'Mobile AL', 'Los Angeles CA', 'Charleston SC', 'Philadelphia PA', 'Port Authority of New York/New Jersey NY/NJ',
          'New Orleans LA', 'Savannah GA'])

# visualizing the heatmap
plt.figure(figsize=(8, 5))
sns.heatmap(order_heatmap_data, annot=True, fmt=".1f", cmap='Greens')
plt.title('Average Processing and Delivery Time by Location')
plt.tight_layout()
plt.savefig(os.path.join(path, '04 Analysis', 'visualizations', 'average processing and delivery.png'), dpi=300, bbox_inches='tight')
plt.show()
```
The return rate of products are around 10%.  
![Order status](https://github.com/user-attachments/assets/490ab046-fb42-4041-b83b-049fe2536345)  

###### Python Code:
```
order_status = df_orders9['status'].value_counts().reset_index()

# Visualizing order status
green_colors = ['#186a3b', '#239b56', '#2ecc71', '#82e0aa', '#d5f5e3', '#eafaf1']
fig = px.pie(order_status, values='count', names='status', title='Order Status Percentage', color_discrete_sequence= green_colors)
fig.update_layout(title={'x': 0.5, 'xanchor': 'center'},)
fig.show()
```
Most popular browser choice among customers: Chrome  
![Popular browser choice](https://github.com/user-attachments/assets/bd41b172-1376-4989-b45e-2e2164030040)  
###### Python Code:
```
browser_choice = df_events['browser'].value_counts().reset_index()

# Visualizing browser choice
fig = px.pie(browser_choice, values='count', names='browser', color='browser',
             color_discrete_map={'Chrome':'#f1c40f',
                                 'Firefox':'#e67e22',
                                 'Safari':'#00bcd4',
                                 'IE':'#2196f3',
                                'Other':'#bdbdbd'})
fig.update_traces(textposition='inside', textinfo='percent+label')
fig.show()
```
![Successful traffic sources](https://github.com/user-attachments/assets/8b46def5-c24a-4fe6-a0a8-df8605fee325)

###### Python Code:
```
# filter traffic that made a purchase based on the country
traffic_purchase1 = (df_events[df_events['event_type'] == 'purchase']
    .groupby(['traffic_source', 'country'])
    .size()
    .reset_index(name='count'))

# Count the filtered traffic in each country
country_totals = (traffic_purchase1.groupby('country')['count']
    .sum()
    .reset_index(name='total_country_count'))

# Merge traffic_purchase1 with country_totals
traffic_purchase = traffic_purchase1.merge(country_totals, on='country')

# Sort based on total DESC
traffic_purchase_sorted = traffic_purchase.sort_values(
    by=['total_country_count', 'count'],
    ascending=[True, True])

# Visualize
custom_colors = ['#186a3b', '#239b56', '#2ecc71', '#82e0aa', '#a9dfbf']
fig = px.bar(
    traffic_purchase_sorted,
    x='count',
    y='country',
    color='traffic_source',
    title='Successful Purchases by Country and Traffic Source',
    color_discrete_sequence=custom_colors
)

fig.update_layout(
    xaxis_title='Successful Purchases',
    yaxis_title='Country',
    barmode='stack',
    legend_title='Traffic Source',
    height=800
)
fig.show()
```
Interactive revenue over-time chart
![Revenue Over-time](https://github.com/user-attachments/assets/f020f1d5-2a66-479b-99a0-9a75b11a9b42)
###### Python Code:
```
# pick columns
df_orders9[['sale_price', 'order_date']]

# Aggregate sum of revenue
df_revenue_time = df_orders9.groupby(['order_date']).agg(
    revenue=('sale_price', 'sum')).reset_index().sort_values(
    by='revenue', ascending= False)

# converting order date back to dateframe
df_revenue_time['order_date'] = pd.to_datetime(df_revenue_time['order_date'])

# Visualize
fig = px.line(df_revenue_time, x='order_date', y='revenue',
              title='Monthly Revenue Over-Time',
              labels={'order_date': 'Month', 'revenue': 'Revenue'},
              template='plotly_white',
              color_discrete_sequence=['#2ecc71']
             )

fig.update_traces(mode='lines+markers')
fig.update_layout(xaxis_title='Date', yaxis_title='Revenue',
                  xaxis_rangeslider_visible=True,
                    height=600,
                    width=1000 
)
fig.show()
```

## Recommendations
- Focus marketing campaigns on returning customers, especially those with higher order values.
- Create loyalty programs for existing customers. eg. loyalty credit that accrues after every purchase and can be used in the next order.
- Create personalized product recommendation based on previous purchase history.
- Increase campaigns in top performing countries like China and USA.
- Allocate more budget to SEO and email promotions.

## Next Steps
- Build prediction model for produt performance.
- Promote best performing products to more customers.
- Use insights to personalize website content and personal recommendations.
- Collect customer reviews for better understanding of customer needs.

#### Project Folders
- 01 Project Management
  - Looker Ecommerce - Project Brief: Project brief including objectives, key questions, analysis criteria, tasks and deliverables.
- 03 Scripts
  - includes python scripts used to uncover Looker E-commerce insights.
- 04 Analysis/Visualizations
  - Visualization: includes visualizations derived using python.
- 05 Sent To Client
  - looker ecommerce project: Brief Excel file including steps taken to derive the insights and changes made to cleanup the data sets.

## Sources and Links
[Looker E-commerce Data Set](https://www.kaggle.com/datasets/mustafakeser4/looker-ecommerce-bigquery-dataset/data?select=order_items.csv)  
[Tableau Dashboard](https://public.tableau.com/app/profile/faisal.malekzada/viz/LookerECommerce/LookerECommerce)  

Source: Looker Ecommerce BigQuery Dataset Accessed through [Kaggle](https://www.kaggle.com/datasets/mustafakeser4/looker-ecommerce-bigquery-dataset/data)
