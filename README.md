# 📊 Data Analysis Project With Python
A data analysis project built with Python, showcasing real-world data cleaning, exploration, visualization, and insights generation for decision-making.


## 📁 Project Overview
This project explores the landscape of data-related jobs and required skills. By leveraging Python-based data analysis techniques, this project provides actionable insights for aspiring data professionals, recruiters, and educators looking to align skill development with current industry needs in India’s growing data ecosystem.


## Tools I Used
For my deep dive into the data analyst job market, I harnessed the power of several key tools:

- Python: The backbone of my analysis, allowing me to analyze the data and find critical insights.I also used the following Python libraries:
- Pandas Library: This was used to analyze the data.
- Matplotlib Library: I visualized the data.
- Seaborn Library: Helped me create more advanced visuals.
- Jupyter Notebooks: The tool I used to run my Python scripts which let me easily include my notes and analysis.
- Visual Studio Code: My go-to for executing my Python scripts.
- Git & GitHub: Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.
Data Preparation and Cleanup
## The Analysis 

## 1. What are the most demanded skills for the top 3 most popular data role ?

To identify the most in-demand skills for the top three most popular data-related job roles. I began by filtering job postings to determine the roles with the highest frequency. For each of these top three roles, I then extracted the five most commonly required skills. This analysis highlights the most sought-after job titles along with their associated skill sets, providing valuable insights into which skills to prioritize based on the specific role.

View my notebook with detailed steps here:
[2_Skills_Count.ipynb](https://github.com/Dhruv-gif-hub/Advanced/blob/main/Project/2_Skills_Count_.ipynb)

### Visualize Data

```python
fig,ax = plt.subplots(len(job_titles),1)
sns.set_theme(style='ticks')
for i,job_title in enumerate(job_titles):
    df_plot = df_skilled_perc[df_skilled_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent',y='job_skills',ax=ax[i],hue='skill_count',palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].legend().set_visible(False)
    ax[i].set_xlim(0,78)
    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v+1,n,f'{v:.0f}%',va='center')
    if i == (len(job_titles) - 1):
        pass
    else:
        ax[i].set_xticks([])

fig.suptitle('Skills Requested in Indian Jobs Postings', fontsize=15)
fig.tight_layout(h_pad=0.5) # Fixing the overlap
plt.show()

```

### Results

![Visualization for Top Skills in Data Science Jobs](
https://github.com/Dhruv-gif-hub/Advanced/blob/main/Skill_Demand.png)

### Insights 

- Python is a highly versatile and in-demand programming language across all three roles, with particularly strong demand among Data Scientists (70%) and Data Engineers (61%).

- SQL emerges as the most frequently requested skill for both Data Analysts and Data Engineers, appearing in over half of all job postings for each. Among Data Scientists, SQL is also highly valued, featuring in 68% of listings, making it one of the top required skills across the board.

- Data Engineers are expected to possess more specialized technical expertise in tools and platforms such as AWS, Spark, and Azure. In contrast, Data Analysts and Data Scientists are typically required to be proficient in broader data management and analysis tools, including Excel and Tableau.

-----------------------------------------------------------------

# The Analysis

## 2. How are in-demand skills trending for Data Analysts ?

```python
from matplotlib.ticker import PercentFormatter
df_plot = df_DA_India_percent.iloc[:,:5]
sns.lineplot(data=df_plot,dashes=False,palette='tab10')
sns.set_theme(style='ticks')
sns.despine()
plt.title('Trending Top Skills for Data Analysts in India')
plt.ylabel('Job Posting')
plt.xlabel('2025')
plt.legend().remove()
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))
for i in range(5):
    plt.text(11.2,df_plot.iloc[-1,i],df_plot.columns[i])
plt.show()

``` 
### Results 

![Trending Top Skills for Data Analysis in India](https://github.com/Dhruv-gif-hub/Advanced/blob/main/Skill_Trend.png)

### Insights:
- SQL remains the most consistently demanded skill throughout the year, although it shows some high and low phases in demand.
- Excel experienced a significantly increase in demand starting around April, surpassing Python, but by the end of the year Python regained its pace.
- Both Python and Tableau show relatively stable demand throughtout the year with some fluctuations but remain essential skills for data analysis.
- Power Bi, while less demanded compared to the others, shows a slight upward trend towards the year's end.

------------------------------------------------------------------

# The Analysis
## 3. How well do jobs and skills pay for Data Analysts ? 

### Salary Analysis fo Data Jobs.

#### Visualize Data
```python
sns.boxplot(data=df_India_top6, x='salary_year_avg', y='job_title_short', order=job_order)
sns.set_theme(style='ticks')
plt.title('Salary Distribution in India')
plt.xlabel('Yearly Salary ($USD)')
plt.ylabel('')
plt.xlim(0,350000)
ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```
#### Results 
![Salary Distribution of Data Jobs in India](https://github.com/Dhruv-gif-hub/Advanced/blob/main/Salary_boxplots.png)

### Insights
Here are some concise professional insights based on the salary distribution data:

Here’s a concise summary in four points:

- **Data Engineers and Scientists**: Salaries have grown steadily, with Data Engineers earning $80,000–$120,000 and Data Scientists $90,000–$120,000 annually due to increasing demand.  
- **Senior Data Engineers**: Highly skilled professionals now command over $150,000 annually as companies prioritize advanced data management.  
- **Machine Learning Engineers**: A sharp rise in demand has led to salaries ranging from $150,000 to $250,000 for their specialized expertise.  
- **Data Analysts and Software Engineers**: Salaries remain lower, at $60,000–$90,000 for Data Analysts and up to $50,000 for Software Engineers, reflecting less specialization compared to other roles.  

------------------------------------------------------------------

# The Analysis

## 3. How will do jobs and skills pay for Data 
### Highest Paid & Most Demanded Skills for Data Analysts
 
```python
fig,ax = plt.subplots(2,1)
sns.set_theme(style='ticks')

sns.barplot(data=df_DA_top_pay,x='median',y= df_DA_top_pay.index, hue='median',ax=ax[0], palette='dark:b_r')
ax[0].legend().remove()
ax[0].set_title('Top 10 Highest paid skills for Data Analysts')
ax[0].set_ylabel('')
ax[0].set_xlabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x,_: f'${int(x/1000)}K'))
sns.barplot(data=df_DA_skills,x='median', y=df_DA_skills.index, hue='median',ax=ax[1],palette='light:b')
ax[1].legend().remove()
ax[1].set_title('Top 10 Most In-Demand skills for Data Analysts')
ax[1].set_ylabel('')
ax[1].set_xlabel('')
ax[1].set_xlim(ax[0].get_xlim())
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x,_: f'${int(x/1000)}K'))
plt.tight_layout()
```
#### Results 
In-demand skills for data analysis in the India:

![The Highest Paid & Most In-Demand Skills for Data Analysts in India](https://github.com/Dhruv-gif-hub/Advanced/blob/main/The_Highest_Paid_skills.png)
#### Insights:

- PostgreSQL leads as the highest paid skill for data analysts, with salaries reaching up to $160K, indicating its high market value.  
- Power BI is the most sought-after skill for data analysts, aligning with its widespread use in business intelligence, and offers salaries up to $100K.  
- A notable gap exists between highly paid skills like PostgreSQL and most in-demand skills like Power BI, reflecting differing priorities in compensation and workforce needs.  

------------------------------------------------------------------

# The Analysis
## 4. What is the most optimal skill to learn for Data Analysis ? 
#### Visulize Data
````python
from adjustText import adjust_text
sns.scatterplot(data=df_plot,x='skill_percent',y='median_salary',hue='technology')
sns.despine()
sns.set_theme(style='ticks')

texts=[]
for i, txt in enumerate(df_DA_skills_high_demand.index):
    texts.append(plt.text(df_DA_skills_high_demand['skill_percent'].iloc[i],df_DA_skills_high_demand['median_salary'].iloc[i],txt))

adjust_text(texts,arrowprops=dict(arrowstyle ='->',color='gray'))
plt.xlabel('Percent of Job')
plt.ylabel('Median Yearly Salary')
plt.title('Most Optional skills for Data Analysis in India')
from matplotlib.ticker import PercentFormatter
ax=plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y,pos:f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))
plt.tight_layout()
plt.show()
````
![Most Optional Skills for Data Analysts in India](https://github.com/Dhruv-gif-hub/Advanced/blob/main/Most_optimal_skills.png)

#### Insights
- The analysis highlights that MongoDB stands out as the most lucrative skill in terms of median yearly salary, offering approximately $160K, even though it is required in only a small percentage of job postings. This suggests that expertise in niche database technologies can command premium pay.

- SQL dominates the demand landscape, being required by nearly half the job postings, with a median salary of around $100K. Similarly, Python holds significant demand with higher salaries ($110K), showing the strong value of foundational programming skills in the data analytics market.

- Skills related to Analyst tools like Power BI and Tableau, though not the most sought-after in terms of job postings, offer competitive salaries around $120K, making them a strategic choice for professionals looking to balance versatility with salary growth.

- Cloud technologies like AWS and Azure demonstrate stable demand and offer a respectable median salary ($100K), underscoring their importance for professionals dealing with modern data infrastructure.

------------------------------------------------------------------

# Challenges I Faced
- Data Inconsistencies: Handling missing or inconsistent data entries requires careful consideration and thorough data-cleaning techniques to ensure the integrity of the analysis.
- Complex Data Visualization: Designing effective visual representations of complex datasets was challenging but critical for conveying insights clearly and compellingly.
- Balancing Breadth and Depth: Deciding how deeply to dive into each analysis while maintaining a broad overview of the data landscape required constant balancing to ensure comprehensive coverage without getting lost in details.

