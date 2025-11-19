
📘 Splunk Log Analysis Practical — Complete Portfolio Write-Up (Polished Version)

KALEEM ALBALOSHI (Cybersecurity Analyst)

🔰 Overview

This Splunk practical demonstrates my ability to perform end-to-end log analysis using Splunk Enterprise.
The tasks performed include:
Uploading and indexing log data
Exploring events and fields
Extracting custom fields using SPL + Regex
Generating visualizations
Performing IP-based geolocation analysis
Creating reports, alerts, and dashboards
Building a complete SOC-style monitoring workflow

This project reflects real-world SOC Analyst activities such as log investigation, event correlation, anomaly detection, and reporting.

⚠️ Disclaimer
All logs used in this practical are sample logs for learning and demonstration purposes only.
No real organizational or sensitive data is used.
All actions performed in Splunk are within a controlled, offline lab environment.

STEP 1 — Uploading & Indexing Log Files

Task Performed:

Imported ZIP log file via Settings → Add Data → Upload File
Assigned source type and named the data input
Indexed the file into Splunk

Observation:

The indexed data contained 9 events, categorized under event types such as:
success
failed
denied
SCREENSHOTS
<img width="1366" height="768" alt="Screenshot (1245)" src="https://github.com/user-attachments/assets/eb034824-1fb3-4a54-b08c-9f3dbaf9271e" />
<img width="1366" height="768" alt="Screenshot (1244)" src="https://github.com/user-attachments/assets/e03593d0-ceae-467d-973d-eab194a0ce1c" />
<img width="1366" height="768" alt="Screenshot (1243)" src="https://github.com/user-attachments/assets/3b283f9b-bbdc-457e-8601-3a2da25f62e7" />
<img width="1366" height="768" alt="Screenshot (1242)" src="https://github.com/user-attachments/assets/703fdea6-6019-4715-b4c8-2c4bd194effb" />
<img width="1366" height="768" alt="Screenshot (1241)" src="https://github.com/user-attachments/assets/770b15f4-9f5a-4971-b747-d99704710462" />
<img width="1366" height="768" alt="Screenshot (1240)" src="https://github.com/user-attachments/assets/7911cb7c-0943-4d7c-a2fd-de7f9cf7cb67" />
<img width="1366" height="768" alt="Screenshot (1239)" src="https://github.com/user-attachments/assets/90945ea6-34e7-4bee-a178-08bedc12f1dd" />



STEP 2 
🔵 STEP 2 — Exploring Event Fields & Time Ranges

Actions Taken:

Opened the Fields section
Selected date_wday to analyze weekday-based patterns
Opened Event Visualization
Switched between different chart types
Experimented with custom time ranges

Purpose:

To understand how event activity changes based on time, weekday, and field types.

SCREENSHOTS
<img width="1366" height="768" alt="Screenshot (152)" src="https://github.com/user-attachments/assets/89e57b94-1910-4e0a-82c9-46c12512caef" />
<img width="1366" height="768" alt="Screenshot (151)" src="https://github.com/user-attachments/assets/eddd3bff-3550-495e-ad20-9a30975a7f1b" />
<img width="1366" height="768" alt="Screenshot (150)" src="https://github.com/user-attachments/assets/ebd7a578-9969-4c96-8450-44bc798bdf56" />
<img width="1366" height="768" alt="Screenshot (149)" src="https://github.com/user-attachments/assets/9092a617-0474-4ec9-b235-0e93c3ca1790" />
<img width="1366" height="768" alt="Screenshot (148)" src="https://github.com/user-attachments/assets/f8ece774-3353-49db-8d14-73b35b3c2885" />
<img width="1366" height="768" alt="Screenshot (147)" src="https://github.com/user-attachments/assets/b7a85c78-686e-4d58-9f5d-4ce79c62bc4c" />
<img width="1366" height="768" alt="Screenshot (146)" src="https://github.com/user-attachments/assets/c15a6087-e760-4615-85da-b048eab65895" />



STEP 3
🔵 STEP 3 — Extracting Custom Field (categoryId) Using REX
Command Used
index=main
| rex "categoryId=(?<categoryId>\d+)"

Why This Command?

Extracts numeric values after categoryId=
Creates a custom field called categoryId
Helpful when the log format does not have structured fields
Enables deeper filtering and statistics
Actions Performed
Viewed the extracted field under Interesting Fields

Analyzed:
✔ Distinct values
✔ Frequency
✔ Trend patterns
Visualized event distribution by chart type

SCREENSHOTS
<img width="1366" height="768" alt="Screenshot (1265)" src="https://github.com/user-attachments/assets/ca1647db-de21-4bb6-b23e-fae7d80744fc" />
<img width="1366" height="768" alt="Screenshot (1264)" src="https://github.com/user-attachments/assets/e595219a-c5bd-4b90-94f1-b3e7ce5ebb55" />
<img width="1366" height="768" alt="Screenshot (1263)" src="https://github.com/user-attachments/assets/c0c43be5-cc6c-4622-a286-335037e51d36" />
<img width="1366" height="768" alt="Screenshot (1262)" src="https://github.com/user-attachments/assets/6f686a04-fa7d-44dd-a958-a14fbe3708bf" />
<img width="1366" height="768" alt="Screenshot (1261)" src="https://github.com/user-attachments/assets/73c8e445-e3a3-4f01-93f7-b0f2fe6e5f65" />
<img width="1366" height="768" alt="Screenshot (1260)" src="https://github.com/user-attachments/assets/22fef37a-e2b5-47e0-9469-356cc07a480e" />
<img width="1366" height="768" alt="Screenshot (1259)" src="https://github.com/user-attachments/assets/4ad68c8e-209a-4c26-a3a3-283fa7814dac" />



STEP 4

##  Overview
In this Step we perform:
- Basic searching across all indexes  
- Field extraction and event counting  
- Time-based analysis with `timechart`  
- Rex command for extracting IP addresses  
- Country-based statistics using `iplocation`  
- Multiple visualizations: pie charts, line charts, bar charts  



🔵 STEP 4 — Basic Searching, Counting & Visualizations
4.1 — Count Events by Status
index=* 
| stats count by status


Observation:
Displayed total events grouped by status (failed, success, denied).
Created a pie chart for better visualization.


SCREENSHOTS
<img width="1366" height="768" alt="Screenshot (1303)" src="https://github.com/user-attachments/assets/40d50190-61b5-47ee-b11a-7f5b724dc842" />
<img width="1366" height="768" alt="Screenshot (1302)" src="https://github.com/user-attachments/assets/2f883d6b-e997-4400-886d-b28c2b69ff9e" />


Counting Events by Status
Command
index=* 
| stats count by status

Observation
Splunk returned 27 events.
Viewed the table and a visualization chart.

SCREENSHOT
<img width="1366" height="768" alt="Screenshot (1307)" src="https://github.com/user-attachments/assets/5bad0c10-54b2-49f2-8a6a-3f935294212f" />
<img width="1366" height="768" alt="Screenshot (1306)" src="https://github.com/user-attachments/assets/6517b8cb-ab39-4df2-ae8b-3c34473dbfed" />
<img width="1366" height="768" alt="Screenshot (1305)" src="https://github.com/user-attachments/assets/53da4bf7-3b3d-4827-b140-b44324d5f378" />


4.2 — Timechart on Internal Logs
index=_internal
| timechart count


Purpose:
To visualize Splunk internal activity over time.

Observation:

96 statistics returned

Timechart displayed successful Splunk operations

Visualization changed to pie chart & line chart
SCREENSHOT
<img width="1366" height="768" alt="Screenshot (1311)" src="https://github.com/user-attachments/assets/614a2b4d-ea92-4fe7-b81b-fb2f753136e6" />
<img width="1366" height="768" alt="Screenshot (1310)" src="https://github.com/user-attachments/assets/7a0df624-04ff-4a79-8a46-fe4bd6d7b430" />
<img width="1366" height="768" alt="Screenshot (1309)" src="https://github.com/user-attachments/assets/89af1a2e-05db-44ec-a4df-bd55e4f0b5fb" />
<img width="1366" height="768" alt="Screenshot (1308)" src="https://github.com/user-attachments/assets/3e285a14-173a-4110-8330-6a4f7da296df" />



4.3 — Extract IP Addresses + Country Analysis
index=* 
| rex field=_raw max_match=0 "(?<ip>\d{1,3}(\.\d{1,3}){3})"
| mvexpand ip
| iplocation ip
| timechart count by Country


Results:

Extracted all IPs from raw logs
Identified geolocation using iplocation
All IPs belonged to USA
Visualized country-wise activity trend

SCREENSHOT
<img width="1366" height="768" alt="Screenshot (1331)" src="https://github.com/user-attachments/assets/b5ff6914-f8d2-4cb1-8b43-48e1b0695fd0" />
<img width="1366" height="768" alt="Screenshot (1330)" src="https://github.com/user-attachments/assets/7d492dce-a1d4-4321-862b-eb0ff5a6c06f" />


4.4 — Country Statistics Sorted by Count
index=* 
| rex field=_raw max_match=0 "(?<ip>\d{1,3}(\.\d{1,3}){3})"
| mvexpand ip
| iplocation ip
| stats count by Country
| sort - count


Purpose:
To identify which country generates the most events.

SCREENSHOTS
<img width="1366" height="768" alt="Screenshot (1328)" src="https://github.com/user-attachments/assets/e396e6a5-e92b-4787-b8cb-4a0e0cf7835e" />
<img width="1366" height="768" alt="Screenshot (1327)" src="https://github.com/user-attachments/assets/bb402730-2cd7-4963-b126-3a2cc776d10a" />
<img width="1366" height="768" alt="Screenshot (1329)" src="https://github.com/user-attachments/assets/f089fd25-dedb-4964-951d-87e99df8c15a" />




STEP 5
🔵 STEP 5 — Creating a Report

Actions Performed:

Clicked Save As → Report
Set name, permissions, and description
Edited schedule (weekly execution)
Configured Send Email action (trial mode prevented email delivery)

Significance:
Reports help automate routine monitoring tasks in SOC operations.

SCREENSHOTS
<img width="1366" height="768" alt="Screenshot (1379)" src="https://github.com/user-attachments/assets/407e0f5b-ca53-45ad-82bd-2e0387bdd53e" />
<img width="1366" height="768" alt="Screenshot (1378)" src="https://github.com/user-attachments/assets/326476a6-6a7d-4e96-904a-c3eb7fcb28f6" />
<img width="1366" height="768" alt="Screenshot (1377)" src="https://github.com/user-attachments/assets/3e2b8be8-6ff5-4d20-8581-062f59d55d4f" />
<img width="1366" height="768" alt="Screenshot (1376)" src="https://github.com/user-attachments/assets/3ed412cc-4b7b-4bb5-adba-be5f7b426065" />
<img width="1366" height="768" alt="Screenshot (1375)" src="https://github.com/user-attachments/assets/32bedcfe-af9c-421c-8e7e-aca54e5c3b30" />
<img width="1366" height="768" alt="Screenshot (1374)" src="https://github.com/user-attachments/assets/156af1d2-7c6f-4cd2-a8cb-9d52c6ee6a09" />
<img width="1366" height="768" alt="Screenshot (1373)" src="https://github.com/user-attachments/assets/ffeddbd4-c67b-43ce-a879-58c853b0e9a4" />
<img width="1366" height="768" alt="Screenshot (1372)" src="https://github.com/user-attachments/assets/9c6ccc96-f5a7-40ac-98d5-981de8b6d893" />
<img width="1366" height="768" alt="Screenshot (1371)" src="https://github.com/user-attachments/assets/9a24d0c6-214f-4950-82e7-4d0d0fe8d50f" />
<img width="1366" height="768" alt="Screenshot (1370)" src="https://github.com/user-attachments/assets/044de068-5d2b-4dcd-93b7-55ff71b7a38b" />
<img width="1366" height="768" alt="Screenshot (1369)" src="https://github.com/user-attachments/assets/2fabfce2-1a60-415f-840b-e4af0158b235" />
 


STEP 6
🔵 STEP 6 — Creating Alerts

Actions Performed:

Saved search as Alert
Set trigger conditions
Added email notification action
Verified permission settings
Saved the alert successfully

Purpose:
Alerts notify analysts automatically when suspicious or important events occur.

SCREENSHOT
<img width="1366" height="768" alt="Screenshot (1386)" src="https://github.com/user-attachments/assets/289feadc-80ae-4039-8244-cf7871eae9d1" />
<img width="1366" height="768" alt="Screenshot (1385)" src="https://github.com/user-attachments/assets/8ec918f8-4ab2-4347-81f3-c9652362fa42" />
<img width="1366" height="768" alt="Screenshot (1384)" src="https://github.com/user-attachments/assets/9168384d-1c34-4caf-9f70-d9305222a475" />
<img width="1366" height="768" alt="Screenshot (1383)" src="https://github.com/user-attachments/assets/e45a6be9-2b1e-44e1-9240-e7bf63f50794" />
<img width="1366" height="768" alt="Screenshot (1382)" src="https://github.com/user-attachments/assets/499b5be0-fa1a-4bb8-b0c2-51d07504fbaf" />
<img width="1366" height="768" alt="Screenshot (1381)" src="https://github.com/user-attachments/assets/b6fe885b-8d9a-4ad8-96d8-5c89afd343a7" />
<img width="1366" height="768" alt="Screenshot (1380)" src="https://github.com/user-attachments/assets/c5b7cdd8-ea0e-48cd-b022-f3406c1a7fc1" />



STEP 7

CREATING NEW DASHBOARD

STEP 7 — Building a Dashboard

Actions:

Created Classic Dashboard
Added panels using previously built reports
Applied dark theme
Organized panels on left & right side
Included bar charts, pie charts, line charts, and tables
Saved the dashboard successfully

Outcome:
A fully functional SOC-style monitoring dashboard.

SCREENSHOTS
<img width="1366" height="768" alt="Screenshot (1415)" src="https://github.com/user-attachments/assets/aec367d6-9bac-4aca-9475-38ed59a2b015" />
<img width="1366" height="768" alt="Screenshot (1414)" src="https://github.com/user-attachments/assets/17a7ccae-e0c5-48a0-8ec2-0bd5cf8fc747" />
<img width="1366" height="768" alt="Screenshot (1413)" src="https://github.com/user-attachments/assets/45de3b0f-d783-4bff-aaa7-09e6ce2eafff" />
<img width="1366" height="768" alt="Screenshot (1412)" src="https://github.com/user-attachments/assets/13f270d8-9b13-4bd3-aa81-01547f99d034" />
<img width="1366" height="768" alt="Screenshot (1411)" src="https://github.com/user-attachments/assets/9182d0f0-4a50-4b6a-8aff-81e2a0e7e880" />
<img width="1366" height="768" alt="Screenshot (1410)" src="https://github.com/user-attachments/assets/2078ebfe-52e5-4ae5-a70f-28e4d6841994" />
<img width="1366" height="768" alt="Screenshot (1409)" src="https://github.com/user-attachments/assets/cf33cd90-67a1-4670-9df5-5fa0d8c7f782" />
<img width="1366" height="768" alt="Screenshot (1408)" src="https://github.com/user-attachments/assets/aebef747-e61b-4411-8fbf-df9985522555" />
<img width="1366" height="768" alt="Screenshot (1407)" src="https://github.com/user-attachments/assets/1afb85b0-0864-435b-ba35-c9a4c9dc8469" />
<img width="1366" height="768" alt="Screenshot (1406)" src="https://github.com/user-attachments/assets/df31242d-e2ee-466b-bf4c-3c5c59b1ec15" />
<img width="1366" height="768" alt="Screenshot (1405)" src="https://github.com/user-attachments/assets/96c55ad8-8912-49c4-9abe-947a09232127" />
<img width="1366" height="768" alt="Screenshot (1404)" src="https://github.com/user-attachments/assets/78aa354e-bf68-4d74-a423-4367788b69db" />
<img width="1366" height="768" alt="Screenshot (1403)" src="https://github.com/user-attachments/assets/81ac4bd3-1ec4-4124-968c-0398729349c5" />
<img width="1366" height="768" alt="Screenshot (1402)" src="https://github.com/user-attachments/assets/6cb944b4-e2f2-4c39-aa05-8518ba6934a2" />
<img width="1366" height="768" alt="Screenshot (1401)" src="https://github.com/user-attachments/assets/b5ccbcfd-d6e7-4271-a933-df12f94120b4" />
<img width="1366" height="768" alt="Screenshot (1400)" src="https://github.com/user-attachments/assets/6c47623e-d6c4-4f39-bfdf-b948d0ca55ef" />
<img width="1366" height="768" alt="Screenshot (1399)" src="https://github.com/user-attachments/assets/ffe8e076-f63f-4ddb-b3a2-1b0887bb791d" />
<img width="1366" height="768" alt="Screenshot (1398)" src="https://github.com/user-attachments/assets/f27a1db3-f834-4f99-8711-f2d6ba1956f7" />
<img width="1366" height="768" alt="Screenshot (1397)" src="https://github.com/user-attachments/assets/6c4755a1-022f-4a8c-b396-74c409107433" />
<img width="1366" height="768" alt="Screenshot (1396)" src="https://github.com/user-attachments/assets/0d5a82f4-3d65-498a-accd-7aba0dde6f73" />
<img width="1366" height="768" alt="Screenshot (1395)" src="https://github.com/user-attachments/assets/33c9fe95-a9ba-4b02-b7a4-d05eeb328cd5" />
<img width="1366" height="768" alt="Screenshot (1394)" src="https://github.com/user-attachments/assets/b4ea1223-dee1-4f28-9d6a-1ef07e93db57" />
<img width="1366" height="768" alt="Screenshot (1393)" src="https://github.com/user-attachments/assets/0358915e-7608-46f6-8e0b-fc1ba756153c" />
<img width="1366" height="768" alt="Screenshot (1392)" src="https://github.com/user-attachments/assets/f509d8ff-b58c-4d55-a43f-73a607905992" />
<img width="1366" height="768" alt="Screenshot (1391)" src="https://github.com/user-attachments/assets/23073525-8636-49c7-a7af-905bd19f80da" />
<img width="1366" height="768" alt="Screenshot (1390)" src="https://github.com/user-attachments/assets/b79dca66-9535-40e9-9a97-f1a90c1f480d" />
<img width="1366" height="768" alt="Screenshot (1389)" src="https://github.com/user-attachments/assets/42da6ab4-00b9-46c3-af3c-675ee6bbd596" />
<img width="1366" height="768" alt="Screenshot (1388)" src="https://github.com/user-attachments/assets/f6cde4d3-0dfc-4ab8-832b-f0bc1d57e263" />






🎯 Final Summary

Through this Splunk practical, I demonstrated real-world SOC analysis skills, including:
Searching & filtering logs
Field extraction using regex
Visual analysis with charts
IP-based geolocation enrichment
Detection-oriented statistical analysis
Alert & report automation
Dashboard creation for monitoring
This project showcases my ability to work with Splunk as part of a cybersecurity or SOC role.






    




