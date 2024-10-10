2012 Election Poll and Donor Analysis
Overview

This project analyzes the 2012 U.S. General Election data, focusing on:

    Polling data between Mitt Romney and Barack Obama.
    Campaign donation data from different contributors.

The code performs data analysis and visualizations for both the polling and donor data, showcasing trends and insights.
Data Sources

    Poll Data: The 2012-general-election-romney-vs-obama.csv dataset contains polling information related to the 2012 presidential election.
    Donor Data: The Election_Donor_Data.csv dataset contains donation records for various candidates from the 2012 election.

Libraries Used

    numpy: Provides support for numerical calculations.
    pandas: Used for data manipulation and analysis.
    matplotlib: Used for data visualization.
    seaborn: Provides statistical graphics capabilities.
    datetime: Handles date-related data.

Code Breakdown
1. Polling Data Analysis
Step 1: Loading and Exploring Data

    The code loads the polling data using pandas and explores the structure and contents with functions like .info() and .head().

Step 2: Visualizing Poll Affiliation

    Bar Plots: The polling data is visualized using bar plots to display the number of respondents affiliated with each political party (Affiliation column). Additionally, the population type (Population) is also visualized.

python

sns.catplot(x='Affiliation', data=poll_df, kind='count')
sns.catplot(x='Affiliation', data=poll_df, kind='count', hue='Population')

Step 3: Poll Averages and Standard Deviation

    The code calculates the averages and standard deviations for poll results using .mean() and .std(), excluding the 'Number of Observations' column. These values are plotted as a bar plot with error bars.

python

avg.plot(yerr=std, kind='bar', legend=False)

Step 4: Tracking Differences Over Time

    The difference between Obama and Romney's polling percentages is calculated and plotted over time, particularly focusing on the crucial days leading to the election (October 2012).

python

poll_df['Difference'] = (poll_df.Obama - poll_df.Romney)/100
poll_df.plot('Start Date', 'Difference', figsize=(12, 4), marker='o', linestyle='-', color='purple')

    Vertical lines (plt.axvline) are used to mark significant dates within October 2012.

Step 5: Filtering and Zooming In on Key Dates

    The code isolates specific polling data from October 2012 by identifying the index of these dates and zooming in on this range.

2. Donor Data Analysis
Step 1: Loading and Exploring Donor Data

    The donation data is loaded, and basic exploration is done using .info() and .head().

Step 2: Donation Statistics

    The code calculates the mean and standard deviation for donation amounts, identifying typical donation trends.

Step 3: Filtering Top Donations

    Donations greater than $0 are filtered, and top donations are identified with a histogram displaying the distribution of common donations under $2500.

python

com_don.hist(bins=100)

Step 4: Party and Candidate Analysis

    Using a party_map dictionary, the party affiliation of each candidate is assigned. The total donations received by each candidate and party are computed and visualized as bar plots.

python

donor_df.groupby('cand_nm')['contb_receipt_amt'].sum().plot(kind='bar')
donor_df.groupby('Party')['contb_receipt_amt'].sum().plot(kind='bar')

Step 5: Occupation Analysis

    The donations are further analyzed by contributor occupation using a pivot table. Occupations contributing over $1,000,000 are isolated, and their contributions are plotted as horizontal bar charts.

python

occupation_df.plot(kind='barh', figsize=(10, 12), cmap='seismic')

Key Data Cleaning Steps

    Removal of certain redundant occupation entries such as "INFORMATION REQUESTED".
    Aggregation of occupation types (e.g., combining "CEO" and "C.E.O.").

Visualizations

    Bar plots for political affiliations in polling data.
    Line plots for poll trends over time.
    Histograms of donation amounts.
    Bar charts for total donations per candidate and per occupation.

Running the Code

    Install the required libraries using:

    bash

    pip install numpy pandas matplotlib seaborn

    Ensure that both 2012-general-election-romney-vs-obama.csv and Election_Donor_Data.csv are placed in the same directory as the script.
    Run the script in a Python environment.

Insights

    Polling Trends: Visualizing the difference between the two candidates' polling percentages gives insight into the race dynamics, especially in October 2012.
    Donations: Analysis of donation amounts by contributor occupations and parties provides a glimpse into the funding patterns that shaped the 2012 election.

Conclusion

This analysis provides an overview of both polling trends and financial contributions for the 2012 U.S. general election, with key visualizations offering insights into the election landscape.
