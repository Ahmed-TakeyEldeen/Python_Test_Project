# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here:
[2_Skill_Demand.ipynb](3_Project\2_Skill_Demand.ipynb)

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

### Results
![Visualization of The Top Skills](3_Project\images\output1.png)

### Insights

- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half the job postings for both roles. For Data Engineers, Python is the most sought-after skill, appearing in 68% of job postings.

- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).
- Python is a versatile skill, highly demanded across all three roles, but most prominently for Data Scientists (72%) and Data Engineers (65%).