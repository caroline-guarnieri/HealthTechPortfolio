# HealthTechPortfolio
Portfolio showcasing healthcare tech experience and process improvements.



1.) Title: Create Table
 
Purpose: To build a structured foundation for storing Case Management data in a relational database format, allowing for better organization, consistency, and scalability of information related to patients, case types, and authorizations.

 Query: 
CREATE TABLE CaseManagementData (
CaseId INTEGER PRIMARY KEY,
PatientName VARCHAR (50),
InsuranceProvider VARCHAR (50),
CaseType VARCHAR (20) -- LTC, skilled,
ReviewStatus VARCHAR (20) -- pending, approved, denied,
AdmissionDate DATE,
DischargeDate DATE,
AuthorizationNumber VARCHAR (20),
CaseManager VARCHAR (50)
);

Result: A new SQL table was created to hold key fields like patient name, insurance provider, case manager, review status, and more — preparing the data for further analysis and reporting.

Insight: Creating a formal data structure ensures that information stays consistent, easily extracted, and ready for insights. This setup supports decision-making in real-time, such as tracking denials or identifying workload imbalances among team members.



2.) Title: Insert Data

Purpose: Populate the SQL table with sample patient and case data for testing queries and simulating real-life reporting use cases.

Query:
 INSERT INTO CaseManagementData values
(776, 'Elizabeth Brown', 'Buckeye', 'skilled', 'pending', '2025-05-10', '2025-05-24', '213546897', 'Tia'),
(160, 'Barbara Anderson', 'Humana', 'LTC', 'denied', '2025-06-02', NULL, 'UHE2307987', 'Marla'),
(463, 'Joseph Smith', 'UHC', 'skilled', 'completed', '2025-06-19', '2025-07-03', '95362714', 'Jen'),
(718, 'Linda Johnson', 'Anthem', 'LTC', 'pending', '2025-05-08', NULL, 'KA3817209', 'Marla'),
(942, 'Natalie White', 'Buckeye', 'skilled', 'pending', '2025-06-01', '2025-06-15', 'UHC327984', 'Jen'),
(478, 'Bill Jackson', 'UHC', 'LTC', 'denied', '2025-05-11', NULL, 'A7234981', 'Tia'),
(845, 'Susan Davis', 'Anthem', 'skilled', 'completed', '2025-05-22', '2025-06-05', 'HUM9821347', 'Aliese'),
(156, 'Kevin Thomas', 'Humana', 'LTC', 'completed', '2025-06-10', NULL, 'B8236491', 'Olivia'),
(283, 'Roberta Harris', 'Buckeye', 'LTC', 'pending', '2025-06-04', NULL, 'UHC32841', 'Jen'),
(693, 'Jessica Wilson', 'Humana', 'skilled', 'completed', '2025-05-26', '2025-06-09', 'ZB9832714', 'Tia'),
(649, 'William Brown', 'Aetna', 'LTC', 'pending', '2025-06-14', NULL, 'BX921840', 'Marla'),
(174, 'David Smith', 'UHC', 'skilled', 'denied', '2025-05-15', '2025-05-29', 'AXE318427', 'Olivia'),
(584, 'Susan Moore', 'Anthem', 'LTC', 'completed', '2025-06-16', NULL, 'YH238471', 'Jen'),
(371, 'Robert Miller', 'Anthem', 'skilled', 'completed', '2025-05-18', '2025-06-01', 'UH29384719', 'Aliese'),
(304, 'Jessica Davis', 'Aetna', 'skilled', 'pending', '2025-06-03', '2025-06-17', 'UHC4287193', 'Marla'),
(552, 'James Harris', 'Buckeye', 'skilled', 'completed', '2025-06-06', '2025-06-20', 'AP9843721', 'Tia'),
(619, 'David Johnson', 'UHC', 'LTC', 'denied', '2025-05-30', NULL, 'UHE942371', 'Jen'),
(487, 'Patricia Smith', 'Aetna', 'skilled', 'pending', '2025-06-22', '2025-07-06', 'QRX348210', 'Olivia'),
(233, 'John Thomas', 'Buckeye', 'LTC', 'completed', '2025-05-12', NULL, '9271348U', 'Tia')

Result:  Sample data was entered into the CaseManagementData table, representing a variety of insurance providers, case types, and review statuses.

Insight:  Sample data inserted, it becomes possible to simulate real reporting questions — from identifying common payers to spotting workload trends. This data set acts as the test bed for all subsequent SQL queries.



3.) Title: Select All From Table

Purpose: To view all data entries and confirm successful insertion into the SQL table.

Query: 
SELECT * FROM CaseManagementData

Result: All rows and associated fields were displayed, confirming that the data structure and values were inputted correctly.

Insight: This query acted as a quick validation step, ensuring the data was formatted properly and that all records were available for deeper analysis. It confirmed that the table was ready for analytical queries without errors.



4.) Title: Count All Records

Purpose: To determine the total number of patient case records in the database.

Query:

SELECT COUNT (*) FROM CaseManagementData

Result: Returned a single value indicating the total number of cases in the table (19).

Insight: Even a simple count can establish a baseline for how much data is available and help track changes over time (e.g., new intakes or discharges). This query can be repurposed for auditing or performance metrics.



5.) Title: Group by Case Type

Purpose: To summarize patient data by case type (long-term care vs skilled), helping stakeholders understand workload distribution across services.

Query:
SELECT CaseType, COUNT (*) AS Total
FROM CaseManagementData
GROUP BY CaseType
ORDER BY Total DESC;

Result: The query returned counts of records for each case type.

Insight: This breakdown can help departments allocate staff or resources more efficiently. For example, if skilled cases spike, leadership may need to adjust staffing or review timelines accordingly.



6.) Title: Group by Insurance Provider

Purpose: To identify how many patient cases were associated with each insurance provider.

Query:
SELECT InsuranceProvider, COUNT (*) AS Total
FROM CaseManagementData
GROUP BY InsuranceProvider
ORDER BY Total DESC;

Result: The query showed the number of cases tied to each payer.

Insight: Understanding which insurers generate the most cases can inform payer relationship management, billing priorities, and contract negotiations. It can also highlight where denial trends might need to be addressed.



7.) Title: Number of skilled Patients per Provider

Purpose: To drill down further and analyze how many skilled-level cases each insurance provider covered.

Query: 
SELECT InsuranceProvider, COUNT (*) AS SkilledPatients
FROM CaseManagementData
WHERE CaseType = 'skilled'
GROUP BY InsuranceProvider
ORDER BY SkilledPatients DESC;

Result: The output displayed how many skilled patients each payer was responsible for.

Insight: This view allows leadership to understand which providers are most active in higher-acuity services. It can help with revenue forecasting and may also inform staff training needs or referral partnerships.



8.) Title: Most Frequent Payer

Purpose: To view which insurance provider holds the most business.

Query: 
SELECT InsuranceProvider, COUNT (*) AS TotalCases
FROM CaseManagementData
GROUP BY InsuranceProvider
ORDER BY TotalCases desc
LIMIT 1;


Result: The payer with the highest number of patients attached to it is returned.

Insight: Buckeye is the most frequent payer in this scenario. This would suggest to leadership that maintaining this relationship is of high importance. 


