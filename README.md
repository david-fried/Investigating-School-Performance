# Using Pandas to Analyze Data:

## Investigating relationships between student math and reading scores and school performance

        reading_avg_by_grade = reduce(lambda left, right: pd.merge(left, right, on=['School Name'], how='left'), dfr_list)
        reading_avg_by_grade.reset_index(drop=True, inplace=True)
