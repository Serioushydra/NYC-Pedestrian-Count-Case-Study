# *From Hedge Fund Case Studies to Real-World Data: Predicting Economic Vitality in NYC* 


I recently came across a classic quantitative finance interview question: “How can you use anonymized GPS foot traffic data to predict a retail chain's in-store revenue?”
Instead of just theorizing, I decided to build a "Proxy Revenue Model" using NYC Open Data.
The Challenge: In the real world (and at firms like Citadel), you deal with sampling bias, non-normalized pings, and the "panel size" problem. Using the NYC Bi-Annual Pedestrian Counts dataset, I’ve modeled how foot traffic trends can serve as a leading indicator for local economic health.
To understand this code, you have to view it through the lens of a Quantitative Researcher. In the Citadel case study, the challenge isn't just "running a model"—it's handling the messy reality of Alternative Data (GPS pings, sensor counts, etc.)


## **1. The Data Acquisition - The Panel**

**URL** = "https://data.cityofnewyork.us/api/views/cqsj-cfgu/rows.csv?accessType=DOWNLOAD"

•	 Logic: In the case study, given a "panel" of 10 million phones. In this code, our "panel" is the NYC sensor network.

•	Just like the interview solution suggests, we first identify the granularity. This dataset provides counts at specific locations, which we will eventually need to "roll up" to a quarterly level if we were matching it to financial reports.


## **2. Normalization & Melt - Reshaping the Data**
 
•	The raw NYC data is "Wide" (each year is a column). Most Machine Learning models require "Long" data (one row per observation).

•	The case study mentions that panel size changes (Image 11.2). While we can't see the "number of phones" here, by melting the data, we create a structure where we could easily divide Pedestrian_Count by a Total_City_Population variable to get the "True" visit rate.


## **3. Ridge Regression (Solving Overfitting)**
   
•	This is the most critical part of the solution. Your image (Section 11.1) asks: "How would you avoid overfitting on such little data (12 quarters)?"

•	We use Ridge Regression. Unlike standard Linear Regression, Ridge adds a penalty (Alpha) to the size of the coefficients.

•	If our "Pedestrian Count" variable varied wildly due to a sensor error, standard regression might over-rely on it. Ridge "shrinks" that reliance, ensuring the model stays stable—exactly what a hedge fund wants for a stock prediction.

## **OUTCOME**
<img width="940" height="585" alt="image" src="https://github.com/user-attachments/assets/fe50e0e9-63d6-4fa0-be95-de1f7555f2e3" />
