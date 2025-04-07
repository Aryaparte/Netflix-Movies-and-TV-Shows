# Netflix-Movies-and-TV-Shows
data cleaning
This project involves cleaning and preprocessing the Netflix Titles dataset (netflix_titles.csv) available at /kaggle/input/netflix-shows/. The goal is to prepare the data for analysis or modeling by handling missing values, standardizing formats, and ensuring consistency.

#Dataset Information
Source: Kaggle - Netflix Movies and TV Shows

File Name: netflix_titles.csv

Fields:

show_id, type, title, director, cast, country, date_added, release_year, rating, duration, listed_in, description

#Data Cleaning Steps

1.  Load the Dataset
python
Copy
Edit
df = pd.read_csv('/kaggle/input/netflix-shows/netflix_titles.csv')

3.  Identify and Handle Missing Values
Used .isnull().sum() to check the number of missing values per column.

Replaced missing values in less critical columns:

director, cast → filled with "Unknown"

Removed rows with missing values in critical columns:

title, date_added

python
Copy
Edit
df['director'].fillna('Unknown', inplace=True)
df['cast'].fillna('Unknown', inplace=True)
df.dropna(subset=['title', 'date_added'], inplace=True)

3. Remove Duplicate Rows
Ensured that duplicate entries were removed using:

python
Copy
Edit
df.drop_duplicates(inplace=True)

4. Standardize Text Fields
Cleaned and formatted the country column:

Filled missing values with "Unknown"

Standardized case to title case (e.g., "united states" → "United States")

python
Copy
Edit
df['country'] = df['country'].fillna('Unknown').str.strip().str.title()

5.Convert Date Formats
Converted date_added to datetime type for uniformity using:

python
Copy
Edit
df['date_added'] = pd.to_datetime(df['date_added'], format='%B %d, %Y', errors='coerce')

6.Rename Columns
Made all column headers lowercase and replaced spaces with underscores for consistency and code readability:

python
Copy
Edit
df.columns = [col.strip().lower().replace(' ', '_') for col in df.columns]

7.Fix and Check Data Types
Ensured columns like release_year are integers and date_added is a datetime object:

python
Copy
Edit
print(df.dtypes)


✅ Final Remarks
The dataset is now clean and ready for:

Exploratory Data Analysis (EDA)

Visualization

Machine Learning tasks

Dashboards and Reports

