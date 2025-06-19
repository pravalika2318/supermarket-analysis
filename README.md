# supermarket-analysis
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
import pandas as pd
df=pd.read_csv(r"C:\Users\prava\Downloads\Supermart Grocery Sales - Retail Analytics Dataset.csv")
#display the first five rows of the data
print(df.head())

df.info()

display(df.describe())


Sales_category=df.groupby("Category")["Sales"].sum()
#we create a plot of sales by category
Sales_category.plot(kind='bar')
plt.title('Category by Sales', fontsize = 14)
plt.xlabel('Category')
plt.ylabel('Sales')
plt.show()

import pandas as pd
import matplotlib.pyplot as plt

# Load data from Excel file
# Replace 'your_file.xlsx' with the path to your Excel file
# and 'Sheet1' with the name of the sheet containing your data
df = pd.read_excel(r"C:\Users\prava\OneDrive\Desktop\Supermart Grocery Sales - Retail Analytics Dataset.xlsx", sheet_name='Supermart Grocery Sales - Retai')

# Ensure 'Order Date' is in datetime format
df['Order Date'] = pd.to_datetime(df['Order Date'])

# Extract month and year
df['Month'] = df['Order Date'].dt.strftime('%B')
df['year'] = df['Order Date'].dt.year

# Monthly Sales Calculation
monthly_sales = df.groupby('Month')['Sales'].sum().reset_index()

# Sort the data by month
months_order = ['January', 'February', 'March', 'April', 'May', 'June', 
                'July', 'August', 'September', 'October', 'November', 'December']
monthly_sales['Month'] = pd.Categorical(monthly_sales['Month'], categories=months_order, ordered=True)
monthly_sales_sorted = monthly_sales.sort_values(by='Month')

# Create the line chart for monthly sales
plt.figure(figsize=(10, 6))
plt.plot(monthly_sales_sorted['Month'], monthly_sales_sorted['Sales'], marker='o')
plt.title('Sales by Month')
plt.xlabel('Month')
plt.ylabel('Sales')
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()  # Adjust layout to prevent clipping
plt.show()

# Yearly Sales Calculation
yearly_sales = df.groupby("year")["Sales"].sum()

# Create a pie chart for yearly sales
plt.figure(figsize=(8, 8))
plt.pie(yearly_sales, labels=yearly_sales.index, autopct='%1.1f%%', startangle=90)
plt.title('Sales by Year')
plt.axis('equal')  # Equal aspect ratio ensures that pie chart is circular
plt.show()

city_sales = df[['City', 'Sales']]

total_sales = city_sales.groupby('City').sum()

sorted_cities = total_sales.sort_values(by='Sales',
ascending=False)

top_cities = sorted_cities.head(5)

plt.bar(top_cities.index, top_cities['Sales'])
plt.xlabel('City')
plt.ylabel('Sales')
plt.title('Top 5 Cities by Sales')
plt.xticks(rotation=45)
plt.show()
