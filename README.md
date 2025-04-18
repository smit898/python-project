import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

# Load a sample dataset from seaborn
df = sns.load_dataset("titanic")

# Preview the dataset
print(df.head())

# Clean the data: fill missing age values with the median
df['age'].fillna(df['age'].median(), inplace=True)

# Create a new column for age group
df['age_group'] = pd.cut(df['age'], bins=[0, 12, 18, 35, 60, 100], 
                         labels=['Child', 'Teen', 'Young Adult', 'Adult', 'Senior'])

# Plot: survival rate by age group and gender
plt.figure(figsize=(10, 6))
sns.barplot(data=df, x='age_group', y='survived', hue='sex')
plt.title("Survival Rate by Age Group and Gender")
plt.ylabel("Survival Rate")
plt.xlabel("Age Group")
plt.tight_layout()
plt.show()

