### Project Overview

Cohort analysis is a powerful technique used to understand user behavior over time by grouping users based on shared characteristics.
This project analyzes user engagement trends by grouping users into weekly cohorts and evaluating retention and activity patterns.

### Project Objectives
- Analyze trends of new and returning users over time
- Evaluate user engagement using duration metrics
- Identify patterns in user retention across cohorts
- Perform weekly cohort analysis to track behavioral changes
- Visualize relationships between user activity and engagement

### Dataset Description

The dataset contains daily user activity data including:

- New users acquired per day
- Returning users per day
- Engagement duration on Day 1 and Day 7

Each row represents activity for a specific date.

📖 Data Dictionary
| Column Name        | Data Type | Description |
|-------------------|----------|------------|
| Date              | Date     | Activity date |
| New users         | INT      | Number of new users acquired |
| Returning users   | INT      | Number of returning users |
| Duration Day 1    | FLOAT    | Average engagement duration on Day 1 |
| Duration Day 7    | FLOAT    | Average engagement duration on Day 7 |

🛠️ Tools Used
- Python — Data analysis
- Pandas — Data manipulation
- Plotly — Interactive visualization
- Seaborn — Heatmaps
- Matplotlib — Plotting

### Analysis & Key Insights
## 1. Trend Analysis (Users)
```python
import plotly.graph_objects as go
import plotly.express as px

import plotly.io as pio
pio.templates.default = "plotly_white"

# Trend analysis for New and Returning Users
fig = go.Figure()

# New Users
fig.add_trace(go.Scatter(x=data['Date'], y=data['New users'], mode='lines+markers', name='New Users'))

# Returning Users
fig.add_trace(go.Scatter(x=data['Date'], y=data['Returning users'], mode='lines+markers', name='Returning Users'))

# Update layout
fig.update_layout(title='Trend of New and Returning Users Over Time',
                  xaxis_title='Date',
                  yaxis_title='Number of Users')

fig.show()
```
**Output:**
<img width="1102" height="360" alt="Trend Analysis (Users)" src="https://github.com/user-attachments/assets/3121534c-c8f8-41a8-8087-f473025be85c" />

💡 Insight

New and returning users follow similar trends → indicates user conversion behavior.

## 2. Engagement Trend Analysis
```python
fig = px.line(data_frame=data, x='Date', y=['Duration Day 1', 'Duration Day 7'], markers=True, labels={'value': 'Duration'})
fig.update_layout(title='Trend of Duration (Day 1 and Day 7) Over Time', xaxis_title='Date', yaxis_title='Duration', xaxis=dict(tickangle=-45))
fig.show()
```
**Output:**
<img width="1102" height="360" alt="Engagement Trend Analysis" src="https://github.com/user-attachments/assets/4462d788-a347-4099-8a86-a0c7b43426c6" />

💡 Insight

Day 1 engagement is consistently higher than Day 7 → user retention drops over time.

## 3. Correlation Analysis
```python
import seaborn as sns
import matplotlib.pyplot as plt

# Correlation matrix
correlation_matrix = data.corr()

# Plotting the correlation matrix
plt.figure(figsize=(10, 8))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', fmt=".2f")
plt.title('Correlation Matrix of Variables')
plt.savefig("Correlation Matrix of Variables.png", dpi=300, bbox_inches='tight')
plt.show()
```
**Output:**
<img width="2616" height="2328" alt="Correlation Matrix of Variables" src="https://github.com/user-attachments/assets/e818091a-5369-49e1-a428-f20a0cf0cda6" />


💡 Insight 

Strong correlation between new users and returning users → effective user retention funnel.

## 4. Cohort Creation (Weekly)
```python
fig1 = px.line(weekly_averages, x='Week', y=['New users', 'Returning users'], markers=True,
               labels={'value': 'Average Number of Users'}, title='Weekly Average of New vs. Returning Users')
fig1.update_xaxes(title='Week of the Year')
fig1.update_yaxes(title='Average Number of Users')

fig2 = px.line(weekly_averages, x='Week', y=['Duration Day 1', 'Duration Day 7'], markers=True,
               labels={'value': 'Average Duration'}, title='Weekly Average of Duration (Day 1 vs. Day 7)')
fig2.update_xaxes(title='Week of the Year')
fig2.update_yaxes(title='Average Duration')

fig1.show()
fig2.show()
```
**Output:**
<img width="1102" height="360" alt="Cohort Creation (Weekly)1" src="https://github.com/user-attachments/assets/adfa873e-8273-49a1-aeba-b73b6a91733b" />
<img width="1102" height="360" alt="Cohort Creation (Weekly)2" src="https://github.com/user-attachments/assets/d3fd40b9-3881-4749-b883-3ebb4f86119a" />

💡 Insight 

Weekly cohort grouping enables comparison of user engagement across different time periods, highlighting variations in user behavior over time.

## 5. Cohort Visualization
```python
# Creating a cohort matrix
cohort_matrix = weekly_averages.set_index('Week')

# Plotting the cohort matrix
plt.figure(figsize=(12, 8))

sns.heatmap(cohort_matrix, annot=True, cmap='coolwarm', fmt=".1f")
plt.title('Cohort Matrix of Weekly Averages')
plt.ylabel('Week of the Year')
plt.savefig("Cohort Matrix of Weekly Averages.png", dpi=300, bbox_inches='tight')
plt.show()
```

**Output:**
<img width="2784" height="2040" alt="Cohort Matrix of Weekly Averages" src="https://github.com/user-attachments/assets/f1280b37-ce40-4a51-9968-dd6bd0156d7c" />

💡 Insight 
- User activity fluctuates weekly
- Significant spike observed in Week 47
- Engagement patterns are inconsistent across cohorts

### Key Findings
- New users and returning users show strong correlation
- Engagement significantly drops from Day 1 to Day 7
- Weekly cohorts reveal fluctuations in user behavior
- No consistent pattern between user growth and engagement
- Retention behavior varies across different time periods

### 🚀 Business Recommendations
- Improve retention strategies after Day 1
- Investigate factors causing engagement drop by Day 7
- Analyze spikes (e.g., Week 47) for marketing insights
- Focus on converting new users into returning users

### Final Note

This project demonstrates how cohort analysis can be used to track user retention, engagement, and behavioral trends over time, enabling data-driven decision-making for growth strategies.


