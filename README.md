# Large-Dataset-Analysis

•	Task 1 - Acquire the top 200,000 posts by ViewCount
o	Using Data Explorer on Stack exchange, the data was queried and extracted
o	The code used to query on Data Explorer is available on this link : https://github.com/aditi-1309/Large-Dataset-Analysis/blob/main/Step1:%20Data%20Extraction/1.%20Data%20Extraction%20from%20Stack%20Exchange
•	Task 2 & 3 - Use Pig/Hive/MapReduce - Extract, Transform and Load the data: 
o	The dataset available after task 1 needed cleaning. The Body and the Title columns had HTML tags and escape characters. Using Pandas, this data was loaded into Python. Using Regular Expressions, the HTML tags and the escape characters were omitted. The complete code for this is available on https://github.com/aditi-1309/Large-Dataset-Analysis/blob/main/Step%202:%20ETL%20and%20Querying/1.%20Data%20Cleaning.ipynb
o	The database posts_db and the table posts_table were created in Hive using HQL. The data was loaded into posts_table using the LOAD function. As the data to be loaded is in CSV format, OpenCSVSerde was use. This however converts all the columns’ datatypes into string. Hence, a view called posts_view was created and the columns were typecasted to their original datatype.
o	The view was queried for the 2.2.1, 2.2.2, 2.2.3 tasks. These queries in addition to database creation are available on this link: https://github.com/aditi-1309/Large-Dataset-Analysis/blob/main/Step%202:%20ETL%20and%20Querying/2.%20DB%20creation%20and%20querying
o	The snapshots of the above steps are available in the Appendix.
•	Task 4 - Use Mapreduce/Pig/Hive to calculate the per-user TF-IDF of the top 10 terms for each of the top 10 users
o	TF-IDF is an acronym for Term Frequency-Inverse Document Frequency. 
o	TF is the number of times a word has repeated itself with respect to all words used in the document. IDF is the importance of each word occurring the document. TF-IDF is calculated using the following formula:
 
o	As HQL is a high-level language, the amount of programming on it limited. Hence, PyHive is used here avail the flexibility of programming on Python. Using PyHive, a connection to Hive was made. The data is extracted from the Hive and stored into a DataFrame. 
o	In ScikitLearn package, there is a TfidfVectorizer. This feature allowed in transformation of data into a matrix of TF-IDF features. A function was created to calculate the TF-IDF of the given data. This was further iterated on all 10 users.
o	The GitHub Link to the Python code is : 
o	The data used here is a view created called using the following query:
CREATE VIEW top10_users AS (SELECT OwnerUserId, sum(Score) as PostScore FROM posts_view WHERE OwnerUserID is not NULL GROUP BY OwnerUserId ORDER BY PostScore DESC LIMIT 10); (Git Link: https://github.com/aditi-1309/Large-Dataset-Analysis/blob/main/Step%202:%20ETL%20and%20Querying/2.%20DB%20creation%20and%20querying)
