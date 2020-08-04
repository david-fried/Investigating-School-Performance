# Using Pandas to Analyze Data:

### Investigating relationships between student math and reading scores and school performance


#### Code snippet for merging multiple dataframes simultaneously

        reading_avg_by_grade = reduce(lambda left, right: pd.merge(left, right, on=['School Name'], how='left'), dfr_list)
        reading_avg_by_grade.reset_index(drop=True, inplace=True)
        

#### Code snippet of scores by school spending

        df.rename(columns={'school_name': 'School Name', 'math_score': 'Average Math Score', 'reading_score': 'Average Reading Score', 'type': 'School Type', 'size':                       'Total Students', 'budget': 'Total School Budget'}, inplace=True)
        df['Per Student Budget'] = df['Total School Budget']/df['Total Students']
        df['% Passing Math'] = df['Average Math Score'].apply(lambda x: 100 if x >= 70 else 0)
        df['% Passing Reading'] = df['Average Reading Score'].apply(lambda x: 100 if x >= 70 else 0)
        df['% Overall Passing'] = df.apply(lambda row: 100 if (row['Average Math Score'] >= 70) & (row['Average Reading Score'] >= 70) else 0, axis=1)
        max = df['Per Student Budget'].max()
        df['Spending Ranges (Per Student)'] = pd.cut(df['Per Student Budget'], bins, labels=labels , include_lowest=True)
        df.set_index('Spending Ranges (Per Student)', inplace=True)
        spending_corrected = pd.DataFrame(df[['Average Math Score', 'Average Reading Score', '% Passing Math', '% Passing Reading', '% Overall Passing']])
        spending_corrected = spending_corrected.groupby(['Spending Ranges (Per Student)']).mean()
        for column in spending_corrected.columns:
            spending_corrected[str(column)] =  spending_corrected[str(column)].map("{:.2f}".format)
        spending_corrected


#### Code snippet of scores by school size

        #Scores by School Size
        size = pd.DataFrame(school_summary[['Total Students', 'Average Math Score', 'Average Reading Score', '% Passing Math', '% Passing Reading', '% Overall Passing']])
        size.reset_index(inplace=True, drop=True)
        labels = ['Small (<1000)', 'Medium (1000-2000)', 'Large (2000-5000)']
        bins = [0, 1000, 2000, 5000]
        size['School Size'] = pd.cut(size['Total Students'], bins, labels=labels , include_lowest=True)
        size.set_index('School Size', inplace=True)
        size = size.groupby('School Size').mean()
        for column in size.columns:
            size[str(column)] =  size[str(column)].map("{:.2f}".format)
        size.drop(columns='Total Students', inplace=True)
        size
