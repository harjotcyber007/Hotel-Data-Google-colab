# Hotel-Data-Google-colab

Understanding the Business Problem

In Recent Year , City Hotel & Resort Hotel have seen High Cancellation Rates.Each Hotel is now Dealing with number of issue as result including Fewer revenue & Less than ideal Hotel room use.

Importing Libraries

import pandas as pd 
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
warnings.filterwarnings('ignore')


Loading the Dataset

df = pd.read_csv("C:\\Users\\hp\\Downloads\\hotel_bookings 2.csv")
Data Analysis and Visualization
cancelled_perc = df['is_canceled'].value_counts(normalize = True)
print(cancelled_perc)

![image](https://github.com/user-attachments/assets/569cfac0-0c17-435e-983d-7b36e91938bf)


plt.figure(figsize = (5,4))
plt.title('Reservation status count')
plt.bar(['Not canceled','canceled'],df['is_canceled'].value_counts(), edgecolor = 'k',width = 0.7)
plt.show()

![image](https://github.com/user-attachments/assets/b6ae71c1-ef00-456e-97c4-0fc963f8130b)


plt.figure(figsize = (8,4))
ax1= sns.countplot(x = 'hotel', hue = 'is_canceled',data = df, palette = 'Blues')
legend_labels,_ = ax1. get_legend_handles_labels()
plt.title('Reservation status in different hotels',size = 20)
plt.xlabel('hotel')
plt.ylabel('number of reservations')

df['month'] = pd.to_datetime(df['lead_time']).dt.month

plt.figure(figsize=(3,6))
plt.title('ADR per month', fontsize=30)
sns.barplot(x='month', y='adr', data=df[df['is_canceled'] == 1].groupby('month')[['adr']].sum().reset_index())
plt.legend(fontsize=20)
plt.show()


plt.figure(figsize = (15,8))
plt.title('ADR per month', fontsize = 30)
sns.barplot('month','adr', data = df[df['is_canceled'] == 1].groupby('month')[['adr']].sum().reset_index())
plt.legend(fontsize = 20)
plt.show()

![image](https://github.com/user-attachments/assets/926caf23-76ef-4ecc-b9ec-2d92438d309f)


cancelled_data = df[df['is_canceled'] == 1]
top_10_country = cancelled_data['country'].value_counts()[:10]
plt.figure(figsize = (8,8))
plt.title('Top 10 countries with reservation canceled')
plt.pie(top_10_country,autopct = '%.2f',labels = top_10_country.index)
plt.show()

![image](https://github.com/user-attachments/assets/8745e28f-411f-4659-96bb-d4a9cb0261bf)


Insights

More Cancellation occur when prices are higher
When there is Longer waiting list , Customer tend to Cancel more frequently
The majority of Clients are coming from a offline travel agents to make their reservations
