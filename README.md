# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here:
[Jobs_Demanded_Skills.ipynb](3_Project/Jobs_Demanded_Skills.ipynb)

## Visualiza Data 
```python
fig , ax = plt.subplots(len(job_title),1)

sns.set_theme(style='ticks')

for i ,job_titles in enumerate(job_title):
    df_plot = df_skill_perc[df_skill_perc['job_title_short'] == job_titles].head(5)
    sns.barplot(data=df_plot ,x='skill_percent',y='job_skills' ,ax=ax[i] ,palette='dark:b_r' ) 
    ax[i].set_title(job_titles)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].set_xlim(0,80)
    # ax[i].legend().set_visible(False) there is a comment when you do ploting using sns it doesnt take ax[i].legend
    for n , v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n ,f'{v:.0f}%' ,va='center')
    if i != len(job_title) -1:
        ax[i].set_xticks([])

fig.suptitle('The Percentage of Skills in Job Postings',fontsize=15)
plt.tight_layout(h_pad=.5)
plt.show()

```
![Result](3_Project/images/output1.png)



### Insights

- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 68% of job postings.

- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).
- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).

## 2. How are in-demand skills trending for Data Analysts?
### To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the job postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.

View my notebook with detailed steps here: [Skills_Trend](3_Project/Skills_Trend.ipynb)

## Visualize Data
``` python
df_plot= df_UK_perc.iloc[: , :5]

sns.lineplot(data=df_plot ,dashes=False , palette='plasma')
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills for Data Analyst for UK')
plt.ylabel('Likelihood in Job Postings')
plt.xlabel('')
plt.legend().remove()
plt.tight_layout()

from matplotlib.ticker import PercentFormatter
ay= plt.gca()
ay.yaxis.set_major_formatter(PercentFormatter(decimals=0))

for i in range(5):
    plt.text(11.2 , df_plot.iloc[-2,i] ,df_plot.columns[i])

```

![Result](3_Project/images/output2.png)

## Insights
- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.
- Excel experienced a significant increase in demand starting around September, surpassing both Python and Tableau by the end of the year.
 - Both Python and Tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for data analysts. Power BI, while less demanded compared to the others, shows a slight upward trend towards the year's end.


## 3. How well do jobs and skills pay for Data Analysts?
### To identify the highest-paying roles and skills, I only got jobs in the United States and looked at their median salary. But first I looked at the salary distributions of common data jobs like Data Scientist, Data Engineer, and Data Analyst, to get an idea of which jobs are paid the most.

View my notebook with detailed steps here:[Salary_analysis](3_Project/Salary_analysis.ipynb)

### Visualize Data 

``` Python
sns.boxplot(data=df_US_top6 , x='salary_year_avg',y='job_title_short' , order=job_order)
sns.set_theme(style='ticks')

plt.title('Salary Year AVG on Data Jobs')
plt.xlabel('Yearly Salary (USD)')
plt.ylabel('')
plt.xlim(0,600000)
ticks_x = plt.FuncFormatter(lambda y, pos :f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```
![Boxplot](3_Project/images/output3.png)