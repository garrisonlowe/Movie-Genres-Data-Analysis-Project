# Movie Genres Data Analysis Project
#### Here are some things I want to look at:

#### Research Questions (Q):
- Which genres are the most common (number of movies made)?
- Which genres have high avg. budget and revenue?
- Which genres have high avg. profit?
- Which genres have high avg. popularity?
- Which genres have highest number of movies with a voting avg. >=8?
#### Research Hypotheses (H):
- The best movies according to vote avg. return high profits and revenue.
- The best movies according to popularity return high profit and revenue.
- Highly budgeted movies return high profit.
- Highly budgeted movies have a high popularity.


# Answers and Findings

### Research Question 1
Which genres are the most common (Number of movies made)?

```python
# Creating a Bar Chart to show the number of movies per genre.

genres_count['original_title'].plot.bar(title= 'Movies Per Genre', color= 'DarkBlue')
```

![Movie RQ1](https://github.com/user-attachments/assets/b8b300a7-03d6-442a-81f0-78bf16bac908)


### Research Question 2
Which genres have high avg. budget and revenue?

```python
# Creating a bar chart to show the budget and revenues by Genre, ordered by Revenue.

genres_avg_budget[['budget', 'revenue']].plot.bar(title= 'Budget and Revenue by Genre', color= ('DarkBlue', 'c'))
```

![Movie RQ2](https://github.com/user-attachments/assets/539369b1-56ef-40b4-933d-cd2d900ad346)

### Research Question 3
Which genres have high avg. profit?

```python
# Changing the sort values parameter to the 'profit' column.
genres_avg_profit = genres_avg_budget.sort_values('profit', ascending= True, inplace= True)

# Creating a bar chart to display average profit per genre type.
genres_avg_budget['profit'].plot.bar(title= 'Average Profit by Genre', color= ('DarkBlue'))
```

![Movie RQ3](https://github.com/user-attachments/assets/cfaafcd1-99e6-4536-b027-ff2ee8d241ed)

### Research Question 4
Which genres have high avg. popularity?

```python
# Creating a bar chart to display average popularity per genre type.
genres_avg_budget['popularity'].plot.bar(title= 'Average Popularity by Genre', color= ('DarkBlue'))
```

![Movie RQ4](https://github.com/user-attachments/assets/c87c6a71-6139-4104-9223-62ee98229577)


### Research Question 5
Which genres have the highest number of movies with a voting avg. >= 8?

```python
# Creating a DataFrame to display the number of movies with a vote average over 8 per genre.

genres_vote = pd.DataFrame(vote_fifty.groupby('genres_split').vote_average.nunique()).sort_values('vote_average', ascending= False)
genres_vote

# Creating a bar chart for the above DF.

genres_vote['vote_average'].plot.bar(title= 'Vote Average Above 8 by Genre', color= ('DarkBlue'))
```

![Movie RQ5](https://github.com/user-attachments/assets/01726c36-0034-4aa2-98bc-a283bd111e8f)

### Hypothesis Question 1
The best movies according to vote avg. return high profits and revenue.

```python
# Using Seaborn to create a regression line plot to see the correlation between vote average and profit.

sns.regplot(data= movies_counted, x= 'vote_average', y= 'profit', line_kws= {'color': 'red'})
```
From this figure, we can determine that there is only a small correlation (if any) between the vote average and movie profit. However, there is a lot more outliers in profit as you move up in vote_average, which is to be expected.
![Movie HQ1](https://github.com/user-attachments/assets/033755fc-fdaa-4770-96c8-884757ea2d3c)

```python
# Using Seaborn to create a regression line plot to see the correlation between vote average and revenue.

sns.regplot(data= movies_counted, x= 'vote_average', y= 'revenue', line_kws= {'color': 'red'})
```
Again, there is only a small correlation between vote average and revenue with more high outliers as you move up in vote average.

![Movie HQ1 1](https://github.com/user-attachments/assets/8797840d-b2ba-462c-830f-3bfac3d2dd60)


### Hypothesis Question 2
The best movies according to popularity return high profit and revenue.

```python
#Creating a regression plot to analyze the correlation between Popularity and Revenue
sns.regplot(data= movies_counted, x= 'popularity', y= 'revenue', line_kws= {'color': 'red'})
plt.figure(figsize= (20,10))
plt.show()
```
From this figure, we can determine that the Popularity and Revenue are highly correlated. With Revenue generally going up as Revenue goes up.
![Movie HQ2](https://github.com/user-attachments/assets/14210c40-581d-4d86-a602-4d4a5c0c5328)

### Hypothesis Question 3
Highly budgeted movies return high profit.

```python
#Creating a regression plot to analyze the correlation between Budget and Profit
sns.regplot(data= movies_counted, x= 'budget', y= 'profit', line_kws= {'color': 'red'})
plt.figure(figsize= (20,10))
plt.show()
```
From this figure, we can determine that the Budget and Profit are positively correlated. Movies with higher budgets tend to make higher profits as well.
![Movie HQ3](https://github.com/user-attachments/assets/c30ab0ef-d6f9-4c1e-98fe-a0f03a1ca314)

### Hypothesis Question 4
Highly budgeted movies have a high popularity.

```python
#Creating a regression plot to analyze the correlation between Budget and Popularity.
sns.regplot(data= movies_counted, x= 'budget', y= 'popularity', line_kws= {'color': 'red'})
plt.figure(figsize= (20,10))
plt.show()
```
From this figure, we can determine that the Budget and Profit are slightly positively correlated. Movies with higher budgets tend to be more popular.
![Movie HQ4](https://github.com/user-attachments/assets/d6692c84-58c1-4bb1-b00d-8e3004fc6adf)
