# International Students' Mental Health Analysis

## Project Overview
This project analyzes various factors that influence the **mental health**, **social connectedness**, and **acculturative stress** of international students. The dataset includes information on student demographics, length of stay, and mental health diagnostics such as **PHQ-9** (depression), **SCS** (social connectedness), and **ASISS** (acculturative stress). 

The goal is to identify patterns and correlations that reveal how different factors affect the mental well-being of international students.

## Dataset Features
- **Social Connectedness (tosc)**: A score reflecting how socially connected a student feels.
- **Depression Score (todep)**: A score from the **PHQ-9 test** indicating levels of depression.
- **Acculturative Stress (toas)**: A score measuring stress related to adapting to a new culture.
- **Language Proficiency**: Categories for Japanese and English proficiency (Low, Average, High).
- **Demographics**: Includes academic level, gender, age, and length of stay.

## Key Queries and Findings

### 1. Social Connectedness vs. Depression
- **Finding**: Higher social connectedness correlates with lower depression scores, suggesting that students who feel more connected socially are less likely to experience depression.
- **Query**:
    ```sql
    SELECT tosc AS social_connections, AVG(todep) AS average_phq
    FROM students
    WHERE inter_dom = 'Inter'
    GROUP BY tosc;
    ```
- **Insight**: Social integration plays a crucial role in reducing depression.

### 2. Academic Level vs. Mental Health
- **Finding**: Undergraduate students showed higher depression scores than graduate students, with lower social connectedness and higher acculturative stress.
- **Query**:
    ```sql
    SELECT academic, AVG(todep) AS average_phq, AVG(tosc) AS average_scs, AVG(toas) AS average_as
    FROM students
    WHERE inter_dom = 'Inter'
    GROUP BY academic;
    ```
- **Insight**: Graduate students may have more coping mechanisms and support, reducing stress and improving social connections.

### 3. Age and Mental Health
- **Finding**: Younger students (aged 15-25) showed higher depression and acculturative stress compared to older students.
- **Query**:
    ```sql
    SELECT 
        CASE 
            WHEN age >= 15 AND age < 20 THEN '15-20'
            WHEN age >= 20 AND age < 25 THEN '20-25'
            WHEN age >= 25 AND age < 30 THEN '25-30'
            WHEN age >= 30 AND age < 35 THEN '30-35'
            ELSE 'Others'
        END AS age_range, COUNT(*) AS count_students, AVG(todep) AS average_phq, 
        AVG(tosc) AS average_scs, AVG(toas) AS average_as
    FROM students
    WHERE inter_dom = 'Inter'
    GROUP BY age_range;
    ```
- **Insight**: Younger students face more challenges in adapting to new environments, affecting their mental health.

### 4. Language Proficiency Impact
- **Finding**: Students with higher proficiency in Japanese tend to stay longer and have lower depression scores.
- **Query**:
    ```sql
    SELECT japanese_cate, AVG(stay) AS avg_length_of_stay, AVG(todep) AS avg_depression_score
    FROM students
    WHERE inter_dom = 'Inter'
    GROUP BY japanese_cate;
    ```
- **Insight**: Mastering the local language helps international students feel more comfortable and less stressed.

### 5. Gender Differences in Mental Health
- **Finding**: Female students showed higher depression and acculturative stress than male students, while males had slightly higher social connectedness scores.
- **Query**:
    ```sql
    SELECT gender, AVG(todep) AS average_phq, AVG(tosc) AS average_scs, AVG(toas) AS average_as
    FROM students
    WHERE inter_dom = 'Inter'
    GROUP BY gender;
    ```
- **Insight**: Gender impacts how students cope with stress and form social connections.

### 6. Acculturative Stress and Depression
- **Finding**: High acculturative stress is strongly correlated with increased depression levels.
- **Query**:
    ```sql
    SELECT toas AS acculturative_stress, AVG(todep) AS average_phq
    FROM students
    WHERE inter_dom = 'Inter'
    GROUP BY toas;
    ```
- **Insight**: Students facing higher levels of stress due to cultural adaptation experience worse mental health outcomes.

### 7. Length of Stay and Social Connectedness
- **Finding**: Social connectedness increases with length of stay, suggesting that students become more integrated over time.
- **Query**:
    ```sql
    SELECT stay, AVG(tosc) AS average_scs
    FROM students
    WHERE inter_dom = 'Inter'
    GROUP BY stay;
    ```
- **Insight**: Longer stays allow students more opportunities to form meaningful social bonds.

## Conclusions
- **Social integration**, **language proficiency**, and **cultural adaptation** are critical factors that affect the mental health and well-being of international students.
- **Targeted interventions**, such as language programs and social support networks, could significantly improve their mental health outcomes.

## Next Steps
- **Develop support programs** for students with low social connectedness.
- **Focus on younger and female students**, who are more vulnerable to depression and acculturative stress.
- **Enhance language learning programs** to improve proficiency and help students adapt to the local environment.

This analysis provides key insights into the mental health challenges faced by international students and offers recommendations for improving their well-being.

