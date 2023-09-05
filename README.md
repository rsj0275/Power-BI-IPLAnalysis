# Power-BI-IPLAnalysis


**STEP IN PROJECT**


	Requirement Gathering

	Data Overview

	Connecting Data with Power bi

	Data Cleaning

	Data Modeling

	Background Design in Power Point

	Data Visualization and Charts Designs

	Dashboard Building

	Insights


**REQUIREMENT**


	Primary KPI – IPL Winner

	Primary KPI – Purple and Orange cap holder

	Secondary KPI – Total Sixes and fours of the season

	Secondary KPI – Stats by player(Batter/Bowler)

	Total Wins by teams.

	Total Wins by Venue.

	Toss Decision


**POWER BI FUNCTIONALITES: -**

Data Cleaning in power query: - 

-	Found Spell mistake under Team1, Team2, Winning Team, Toss winner, Location column
  
    •	Rising Pune Supergiants and Rising Pune Supergiant) – corrected.
    •	Bangalore and Bengaluru

-	Split the Venue column by city (Some venues have city and some or not)
  
-	Merge Venue and City column.
  
-	Checked quality of all the columns – no issues found.
  
**Data Processing: -**

-	Create a calendar/Date table by using time intelligence function – Calendar/CalendarAuto function
  
	**DIMDATE** = CALENDAR(MIN(ipl_matches_2008_2022[match_date]), MAX(ipl_matches_2008_2022[match_date]))

-	Created new calculated columns like – YEAR, MONTH, WEEKDAY, FORMAT, CONCATENATE, QUARTER, WEEKEND....

  
**Data Modeling (Relationship b/w Multiple tables): -**

-	We have created relationship between DIMDATE and IPL able. (ONE -TO- MANY)
  
**KPI and Advance KPI generation: -**

**-	Find out title winner:**
  
    **Title Winner** = 
    Var Max_date = CALCULATE(MAX(DIMDATE[Date]), ALLSELECTED(ipl_matches_2008_2022), VALUES(ipl_matches_2008_2022))
    Var Winner = CALCULATE(SELECTEDVALUE(ipl_matches_2008_2022[winning_team]), DIMDATE[Date] = Max_date)
                return Winner

**-	Find out Orange Cap Holder:**
  
    **Batters Run** = CONCATENATE(SUM(ipl_ball_by_ball_2008_2022[batsman_run]), " Runs")

**-	Find out Purple Cap Holder:**
  
    **Bowler Wickets** = CONCATENATE(SUM(ipl_ball_by_ball_2008_2022[iswicket_delivery]), " Wickets")

-	**Find out Bowler Economy rate**: (dividing the number of runs conceded by a bowler by the number of overs bowled.)
  
   **Economy rate** = DIVIDE(SUMX(FILTER(ipl_ball_by_ball_2008_2022, ipl_ball_by_ball_2008_2022[extra_type] <> "Legbyes" &&   ipl_ball_by_ball_2008_2022[extra_type]<> "Byes"), ipl_ball_by_ball_2008_2022[total_run]),(COUNT(ipl_ball_by_ball_2008_2022[overs]))/6)

-	**Find out Bowler Average rate:** (dividing the numbers of runs conceded by a bowler by the number of wickets they have taken)
  
  **Average** = 
    DIVIDE(SUMX(FILTER(ipl_ball_by_ball_2008_2022, ipl_ball_by_ball_2008_2022[extra_type] <> "Legbyes" && ipl_ball_by_ball_2008_2022[extra_type]<>     "Byes"), ipl_ball_by_ball_2008_2022[total_run]),(SUM(ipl_ball_by_ball_2008_2022[iswicket_delivery])))

-	**Find out Batter Strike rate:** (Number of runs scored / Number of balls faced) * 100
  
  **Strike Rate** = 100*(SUM(ipl_ball_by_ball_2008_2022[batsman_run])/COUNT(ipl_ball_by_ball_2008_2022[ball_number]))

**-	Find out Bowler Strike rate:** (Balls Bowled / Wickets Taken)
  
      **Bowler SR** = COUNT(ipl_ball_by_ball_2008_2022[bowler])/SUM(ipl_ball_by_ball_2008_2022[iswicket_delivery])

**-	Find out match winner by toss.**
  
      **MatchWInnBytoss** = CALCULATE(COUNTROWS(ipl_matches_2008_2022), ipl_matches_2008_2022[toss_winner] = ipl_matches_2008_2022[winning_team])

-	Creating a Calculated measure
  
**Import images**
 	
-	We have use some vehicle pics for better visualization.
  
**Creating a different Charts for visualization**

-	We have used below chart to show trends
  
	Bar chart 

	Pie chart 

	Card to show KPI values.

 

