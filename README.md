# Demographic-data-analyzer


In this challenge you must analyze demographic data using Pandas. You are given a dataset of demographic data that was extracted from the 1994 Census database. Here is a sample of what the data looks like:

You must use Pandas to answer the following questions:

    How many people of each race are represented in this dataset? This should be a Pandas series with race names as the index labels. (column)
    What is the average age of men?
    What is the percentage of people who have a Bachelor's degree?
    What percentage of people with advanced education (Bachelors, Masters, or Doctorate) make more than 50K?
    What percentage of people without advanced education make more than 50K?
    What is the minimum number of hours a person works per week?
    What percentage of the people who work the minimum number of hours per week have a salary of more than 50K?
    What country has the highest percentage of people that earn >50K and what is that percentage?
    Identify the most popular occupation for those who earn >50K in India.

Use the starter code in the file demographic_data_analyzer. Update the code so all variables set to "None" are set to the appropriate calculation or code. Round all decimals to the nearest tenth.

Unit tests are written for you under test_module.py.
Development

For development, you can use main.py to test your functions. Click the "run" button and main.py will run.
Testing

We imported the tests from test_module.py to main.py for your convenience. The tests will run automatically whenever you hit the "run" button.
Submitting

Copy your project's URL and submit it to freeCodeCamp.
Dataset Source

Dua, D. and Graff, C. (2019). UCI Machine Learning Repository [http://archive.ics.uci.edu/ml]. Irvine, CA: University of California, School of Information and Computer Science.

```Python
import pandas as pd


def calculate_demographic_data(print_data=True):
    # Read data from file
    df = pd.read_csv("adult.data.csv")

    # How many of each race are represented in this dataset? This should be a Pandas series with race names as the index labels.
    race_count = df['race'].value_counts()

    # What is the average age of men?
    average_age_men = df[df['sex']=='Male']['age'].mean().round(1)

    # What is the percentage of people who have a Bachelor's degree?
    num_bachelors = len(df[df['education']=='Bachelors'])
    total_num = len(df)

    percentage_bachelors = round(num_bachelors / total_num * 100, 1)

    # What percentage of people with advanced education (`Bachelors`, `Masters`, or `Doctorate`) make more than 50K?
    # What percentage of people without advanced education make more than 50K?

    # with and without `Bachelors`, `Masters`, or `Doctorate`
    higher_education = df[df['education'].isin(['Bachelors','Masters','Doctorate'])]
    lower_education = df[~df['education'].isin(['Bachelors','Masters','Doctorate'])]

    # percentage with salary >50K
    non_percentage_higher = len(higher_education[higher_education.salary == '>50K'])
    
    higher_education_rich = round(non_percentage_higher / len(higher_education)*100,1 )
    
    non_percentage_lower = len(lower_education[lower_education.salary == '>50K'])
    
    lower_education_rich = round(non_percentage_lower / len(lower_education)*100,1 )
    
    # What is the minimum number of hours a person works per week (hours-per-week feature)?
    min_work_hours = df['hours-per-week'].min()

    # What percentage of the people who work the minimum number of hours per week have a salary of >50K?
    num_min_workers = df[df['hours-per-week'] == min_work_hours]

    rich_percentage = round(len(num_min_workers[num_min_workers.salary == '>50K']) / len(num_min_workers) * 100, 1)

    # What country has the highest percentage of people that earn >50K?
    country_count = df['native-country'].value_counts()

    country_rich_count = df[df['salary'] == '>50K']['native-country'].value_counts()
    
    highest_earning_country = (country_rich_count/country_count * 100).idxmax()
    highest_earning_country_percentage = round((country_rich_count/country_count * 100).max(), 1)

    # Identify the most popular occupation for those who earn >50K in India.
    people_of_india = df[(df['native-country'] == 'India') & (df['salary'] == '>50K')]
    
    occupation_counts = people_of_india['occupation'].value_counts()
    
    top_IN_occupation = occupation_counts.idxmax()

    # DO NOT MODIFY BELOW THIS LINE

    if print_data:
        print("Number of each race:\n", race_count) 
        print("Average age of men:", average_age_men)
        print(f"Percentage with Bachelors degrees: {percentage_bachelors}%")
        print(f"Percentage with higher education that earn >50K: {higher_education_rich}%")
        print(f"Percentage without higher education that earn >50K: {lower_education_rich}%")
        print(f"Min work time: {min_work_hours} hours/week")
        print(f"Percentage of rich among those who work fewest hours: {rich_percentage}%")
        print("Country with highest percentage of rich:", highest_earning_country)
        print(f"Highest percentage of rich people in country: {highest_earning_country_percentage}%")
        print("Top occupations in India:", top_IN_occupation)

    return {
        'race_count': race_count,
        'average_age_men': average_age_men,
        'percentage_bachelors': percentage_bachelors,
        'higher_education_rich': higher_education_rich,
        'lower_education_rich': lower_education_rich,
        'min_work_hours': min_work_hours,
        'rich_percentage': rich_percentage,
        'highest_earning_country': highest_earning_country,
        'highest_earning_country_percentage':
        highest_earning_country_percentage,
        'top_IN_occupation': top_IN_occupation
    }
```

<img width="800" alt="Screenshot 2023-09-01 015126" src="https://github.com/Marvykeys/Demographic-data-analyzer/assets/130637591/45a95fca-be77-4a6d-9e5f-d5c3f119cf05">
