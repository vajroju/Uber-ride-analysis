# Uber-ride-analysis
📌 Uber Ride Data Analysis 🚖 A data analytics project using Python, SQL, and Power BI to analyze Uber ride patterns and predict demand trends. Features data cleaning, visualization, and predictive modeling with Pandas, Matplotlib, and SQL. 🔹 Technologies: Python, SQL, Power BI, Pandas, Seaborn.  
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load Uber ride dataset (Replace 'uber_data.csv' with your file path)
df = pd.read_csv('uber_data.csv')

# Display basic information and first few rows
print(df.info())
print(df.head())

# Convert date columns to datetime format
df['pickup_datetime'] = pd.to_datetime(df['pickup_datetime'])
df['dropoff_datetime'] = pd.to_datetime(df['dropoff_datetime'])

# Extract hour, day, and month for analysis
df['pickup_hour'] = df['pickup_datetime'].dt.hour
df['pickup_day'] = df['pickup_datetime'].dt.day
df['pickup_month'] = df['pickup_datetime'].dt.month

# Calculate ride duration in minutes
df['ride_duration'] = (df['dropoff_datetime'] - df['pickup_datetime']).dt.total_seconds() / 60

# Plot ride duration distribution
plt.figure(figsize=(10, 5))
sns.histplot(df['ride_duration'], bins=50, kde=True)
plt.xlabel('Ride Duration (minutes)')
plt.ylabel('Frequency')
plt.title('Distribution of Uber Ride Duration')
plt.show()

# Analyze peak hours for Uber rides
plt.figure(figsize=(10, 5))
sns.countplot(x='pickup_hour', data=df, palette='coolwarm')
plt.xlabel('Hour of the Day')
plt.ylabel('Number of Rides')
plt.title('Uber Rides by Hour of the Day')
plt.show()

# Analyze demand by day of the month
plt.figure(figsize=(10, 5))
sns.countplot(x='pickup_day', data=df, palette='viridis')
plt.xlabel('Day of the Month')
plt.ylabel('Number of Rides')
plt.title('Uber Rides by Day of the Month')
plt.show()

# Save processed data
df.to_csv('processed_uber_data.csv', index=False)

print('Uber Data Analysis Completed!')
