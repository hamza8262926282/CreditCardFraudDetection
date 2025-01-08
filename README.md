import pandas as pd 
import numpy as np 
import matplotlib.pyplot as plt 
import seaborn as sns
df=pd.read_csv("creditcard.csv")
rows,columns=df.shape
print(f"Rows = {rows}\nColumns = {columns} ")
missing_values=df.isnull().sum().sum()
print(f"Total missing value: {missing_values}")
class_counts=df['Class'].value_counts()
legitimate=class_counts[0]
fraudulent=class_counts[1]
print(f"legitimate values : {legitimate}")
print(f"fraudulent values : {fraudulent}")
fraudulent_percentage =(fraudulent / rows) * 100
print(f"Percentage of fraudulent values are {fraudulent_percentage:.2f}%")
min_value=df['Amount'].min()
max_value=df['Amount'].max()
mean_value=df['Amount'].mean()
median_value=df['Amount'].median()
print(f"Minimum: {min_value}\nMaximum: {max_value}\nMean: {mean_value:.2f}\nMedian: {median_value}")
max_transaction=df[df['Amount']==df['Amount'].max()]
is_fraudulent=max_transaction['Class'].values[0]

print(f"Maximum transaction amount: {max_transaction['Amount'].values[0]}")
print(f"Is the maximum transaction fraudulent ? {'Yes' if is_fraudulent==1 else 'No'}")
class_counts=df['Class'].value_counts()
class_counts
plt.Figure(figsize=(6,4))
sns.barplot(x=class_counts.index,y=class_counts.values,palette=['green','yellow'])
for idx, value in enumerate(class_counts):
    plt.text(idx, value + 500, str(value), ha='center', fontsize=12)
plt.xticks([0,1],['Legitimate(0)','fraudulent(1)'])
plt.title('Count of Legitimate VS Fraudulent Transactions')
plt.xlabel('Transaction class')
plt.ylabel('Number of transactions')
plt.show()
plt.Figure(figsize=(10,6))
sns.histplot(df['Amount'],bins=50,kde=True,color='blue')
plt.title("Distribution of transaction amount")
plt.xlabel("Transaction amount")
plt.ylabel("Frequency")
plt.show()
corr_matrix=df.corr()
plt.figure(figsize=(12,10))
sns.heatmap(corr_matrix,annot=False,cmap='coolwarm',linewidths=0.5)
plt.title('Correlation matrix of Numerical feaTURES')
plt.show()
