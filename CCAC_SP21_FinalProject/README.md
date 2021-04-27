# Mapping Final Project

## Abstract: About 250 words summarizing your goal, analysis steps, and conclusions. Hint: Write this last (but put it first)

## Purpose/Inquiry Question: Develop an inquiry question concerning a topic of professional or personal interest which concerns the spatial distribution of data points.
What counties and colleges in the United States carry high potential for nursing recruitment?

## Background/Rationale and sources: Why is your inquiry question important? To Whom? What kinds of decisions are you conclusions informing? Also include a list of data sources and literature related to your topic. 2-5 sources is likely sufficient.

I decided on this inquiry question because at the time I was interviewing for a Project Analyst job at UPMC (which I unfortunately did not get).  The focus of the job would be working in Nursing Talent Strategies alongside Nurse Recruiters within the organization.  Some of the responsibilities would include using data analysis to find ways to create effeciency in the recruitment process.  I figured that if I get the job then I can already contribute by presenting something of value.  If I don't then I can still share the analysis with the hiring managers and be able to speak to this accomplishment in later job interviews.

The desired outcome of the analysis is to give a handful of counties along with the colleges that exist there as suggestions for areas to focus on recruiting from.  This focus on recruitment can manifest as building connections and relationship with colleges in the area and even physically going to job fairs.

Data Sources:
Civilian Job Industry Data: https://data.census.gov/cedsci/table?tid=ACSDT5Y2019.C24050
Colleges and Universities: https://hifld-geoplatform.opendata.arcgis.com/datasets/colleges-and-universities?geometry=25.806%2C-16.798%2C-25.171%2C72.130
USA Counties: https://hub.arcgis.com/datasets/esri::usa-counties?geometry=-166.940%2C28.847%2C167.571%2C67.171

## Analysis Steps: List your overall project sequence, including data acquisition and presentation preparation.

1. I gathered data sources from the above listed sites.  I needed a shapefile of the locations of colleges and universities in the United States.  When looking at census data to determine the general job industry of identified individuals, that which was available was at the county level.  Lastly, to align with the census data, I needed a shapefile of counties in the United States.

2. I cleaned the census data set by removing columns that contained data about job industries that weren't science or health care related.  I also removed the columns that broke down the numbers for occupation categories within each job industry.  The data was in a heirarcy of industry level category and then occupation category within the various industry level categories.  Put another way, I only looked at the total numbers at the industry level.  My decision to do this was based on the fact that I felt drilling into the data at the occupation level didn't necessarily help identify likely nurses anymore than the industry level data.  Upon further thought, I realize this could be an incorrect assumption and I feel it would be warranted to double check and compared the outcome when using the occupation level data.  This is probably something I will do once the industry level data is finished being analyzed and visualized.

3. I then pulled the shapefiles and cleaned data into QGIS.  I used ESRI World Topo as a backdrop for the layout I planned to make.

4. An important step for analysis included joining the job industry data to the counties shapefile that I had.  In order to join this I could use the FIPS column from the counties shapefile in along with part of the id column in the job industry data set.  In the job industry data set, each id (row) corresponds with a county in the United States.  However, I needed only part of the id, specifically only the last 5 digits.

5. Getting the last 5 digits actually proved to be a bit of a challenge.  In Excel, I would insert a new column titled GEOID right in between the id column and the county column.  I would then use the following formula to extract the last 5 digits from id: (=RIGHT([column that id is in], 5)).  What became an issue was when pulling this into QGIS, because the column data type was a number, the program would cut off any values that had leading zeros.  Counties in states like Alabama and California were impacted by this and when trying to join the job industry data their rows would come back null.

6. The solution to this was to avoid creating the GEOID column in Excel and instead create it in QGIS.  So I pulled the cleaned job industry data into QGIS and then created the GEOID column within QGIS itself using the field calculator and ensured that the data type of the column was a text (string) type.  Doing this prevented the GEOID leading zeros from being removed and the solved the issues of nulls when joining this job industry data to the US counties.

7. Having joined the job industry data into the US counties layer, I calculated a column ("TotalNurse") totaling the number of jobs from science and healthcare related job industries in each county.  The name of the column is due to the character limit in QGIS for column headers.

8. I then divided these values by the square mileage of each county to obtain the density of people in these job industries per square mile.  This column was called "NDensity".

9. The next step involved narrowing down counties to look at for high density of individuals in the science and health care job industries.  In order to do this I filtered the US Counties table on the NDensity column to only return rows with an NDensity greater than or equal to 250.  I exported these selected features to a layer called "HighestDensityAreas".

10. I then wished to only return about 20 or so counties in total.  In order to have an even more condense result set, I filtered further to only include counties with a NDensity greater than or equal to 850.  I exported these selected features and called this layer "AreasForPotentialRecruitment".

11. Within this newest result set, I calculated a column called "YouthPop", which consisted of the county totals of people aged 20 to 34.  This was obtained by adding together the values in columns "AGE_20_24" and "AGE_25_34". I wanted to factor in the size of the youth population when making my suggestion of counties and colleges to recruit from, so I thought these numbers would be useful.

12. I then displayed the polygon layer "AreasForPotentialRecruitment" as well as the layer "Colleges_and_Universities".

13. Within the attribute table for the "AreasForPotentialRecruitment" I looked at which counties remained relatively high in both density of workers and youth population.  Also keeping consideration of geographic location relative to UPMC in Pittsburgh, I chose to focus on counties surrounding Boston, Philadelphia, and New York City.

14. With these areas identified, I created my map layout displaying them along with the Eastern part of the United States.

## Results and Discussion: Export nicely arranged map layouts and include them in this overview document. Each figure should be accompanied by a caption describing the important information to be gleaned from each figure.

## Conclusions: State and support your conclusions based on the data presented in the results section.
Based on the data examined, the top three recommended areas in the United States for potential nurse recruitment would be Suffolk County, Massachusetts, Philadelphia County, Pennsylvania, and New York, Queens, and Kings counties, New York.

## Limitations: To what degree are the data and their associated conclusions valid in your project context? What data integrity/quality issues exist? Consider how the data was acquired, by whom, and for what purpose.
A limitation of the census data is that it doesn't specifically outline exactly what jobs fall into science and health care industries and occupations.  Additionally, these categories are grouped together with others such as Educational and Administrative services, so the numbers are not exclusively science and health care related.

Something I would want to do as part of a deeper dive would be to look at data from the colleges and universities in these areas to see numbers of students who graduate with degrees in Nursing.  This could help narrow even further where exactly would be worth spending time focusing on recruitment.



## Future research: How could your project be continued? What additional data sets would be useful in additional analysis? What could you not complete that you might have wanted to and why?
I could do another iteration of the analysis but this time at the occupation level of the census data rather than the industry level in order to see if recommended counties change.  Another deeper dive would include gathering data reported by colleges in the recommended areas on students who graduate with degress in nursing and job placement rates.  Using this we can narrow down specifically what colleges to target for partnership.

I am not certain if there is a dataset similar to the census data but specifically for nursing.  If this exists, it would help better inform the decision of areas to target.  Investigating data on nursing specifically in the recommended areas would also be another potential path to take.  Most of what I found when searching what at a state level and it didn't seem there was an obvious centralized place to go for county level data.  I suspect you may have to search for specific cities or schools, hence the purpose of this project to give an idea of where to look.

One other route of research would be to find the largest nursing programs in the country and see where these fall in relation to the county level metrics that were used to identify the potential counties for recruitment.