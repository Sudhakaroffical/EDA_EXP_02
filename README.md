# NAME: SUDHAKAR K
# REGISTER NUMBER: 212222240107

**Netflix Shows & Movies**

**Aim**

To analyze Netflix dataset and compare movies vs TV shows, top producing countries, and release year trends.

**Procedure / Algorithm**

  1)Load dataset (netflix_titles.csv).
  2)Count movies vs TV shows.
  3)Group by country → top contributors.
  4)Create pivot table (release year vs type).
  5)Visualize with bar & line charts.

**Program**
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
df=pd.read_csv(r'https://raw.githubusercontent.com/allenkong221/netflix-titles-dataset/main/netflix_titles.csv')
df

```
<img width="965" height="827" alt="image" src="https://github.com/user-attachments/assets/ccfa60c6-b8c5-49be-8593-979e0cf2c5f3" />

```
df.head()
```
<img width="950" height="367" alt="image" src="https://github.com/user-attachments/assets/664f4efb-6edd-45e8-9ef5-02cad9a573d4" />

```
df.tail()
```
<img width="956" height="357" alt="image" src="https://github.com/user-attachments/assets/b51eb723-6f59-4db8-953b-ffedcf920d37" />

```
df.info()

```
<img width="357" height="312" alt="image" src="https://github.com/user-attachments/assets/02a55a5d-de02-4bf2-be19-6dc0b856edac" />

```
df.shape
```
<img width="613" height="61" alt="image" src="https://github.com/user-attachments/assets/99dd3f56-e840-4ed8-830c-4ec48d1b5d27" />

```
df.describe()
```
<img width="853" height="282" alt="image" src="https://github.com/user-attachments/assets/2b7edf92-37f5-4614-b93d-4635c80b7bd1" />
```
type_counts=df['type'].value_counts()
```
<img width="748" height="154" alt="image" src="https://github.com/user-attachments/assets/2d7a8483-99b8-4853-9f0d-55b427077be8" />

```
df_country=df.dropna(subset=['country']).copy()
df_country['country_list']=df_country['country'].str.split(',\s*')
df_country['country_list']
```
<img width="802" height="301" alt="image" src="https://github.com/user-attachments/assets/6e766a81-4a57-4ada-9b20-fee9646aa9e3" />

```
df_exploded=df_country.explode('country_list')
df_exploded['country_list']=df_exploded['country_list'].str.strip()
country_counts=df_exploded['country_list'].value_counts().reset_index()
country_counts.columns=['country','count']
print('Top Contributing countries :\n',country_counts.head(10))
```

<img width="562" height="200" alt="image" src="https://github.com/user-attachments/assets/cca30655-6468-4f1e-8a38-6734606c91bf" />

```
pivot=pd.pivot_table(df,index='release_year',columns='type',values='show_id',aggfunc='count',fill_value=0)
pivot
```

<img width="597" height="380" alt="image" src="https://github.com/user-attachments/assets/cbd5a58d-7d55-4772-9db2-59d3ce1d34ee" />

```
plt.figure(figsize=(6,4))
sns.barplot(x=type_counts.index,y=type_counts.values,palette='pastel')
plt.title("Count of Movies vs TV shows")
plt.xlabel("Type")
plt.ylabel("Count")
plt.tight_layout()
plt.show()
```

<img width="785" height="359" alt="image" src="https://github.com/user-attachments/assets/7c5d4cff-f019-4e63-ac47-4d3066af8222" />

```
years_to_plot=pivot.loc[2000:2020] if 2000 in pivot.index else pivo.iloc[-20:]
years_to_plot.plot(kind='bar',figsize=(12,6))
plt.title("Count by Release year and Type")
plt.xlabel("Release Year")
plt.ylabel("Count")
plt.legend(title="Type")
plt.tight_layout()
plt.show()
```

<img width="911" height="451" alt="image" src="https://github.com/user-attachments/assets/012659a5-598e-461c-9208-be4220865c31" />

```
for t in pivot.columns:
    
    plt.plot(years_to_plot.index, years_to_plot[t], label=t)
plt.title("Trend of Movies vs TV Shows Over Years")
plt.xlabel("Release Year")
plt.ylabel("Count")
plt.legend()
plt.tight_layout()
plt.show()
```

<img width="568" height="427" alt="image" src="https://github.com/user-attachments/assets/3640b789-ff85-4870-a28d-149a15992127" />


**Result**
Helps Netflix in content planning & investments.
