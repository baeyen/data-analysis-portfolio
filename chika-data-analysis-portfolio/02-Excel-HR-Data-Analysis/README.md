#HR Data Analysis (Excel Functions)
-A quiet spreadsheet that answers loud questions — tenure, bonuses, and who’s ready to rise.


#Purpose
-Turn a small HR table into clear answers for managers:

-How long has each person worked?

-Who is eligible for promotion (by a transparent rule)?

-What’s the headcount in IT?

-Create clean helper fields (employee info strings, usernames) for quick reporting.

#Files
02-Excel-HR-Data-Analysis/

├─ workbooks/

│  └─ ASSIGNMENT 2. CHIKA CELESTINE IROEGBULEM.xlsx

├─ outputs/

│  └─ screenshots/

│     └─ hr-metrics-overview.png 

└─ README.md

#Dataset (columns used)
-From the DATA SET sheet:

| Column | Header                             | Example                                       | Notes                                    |
| ------ | ---------------------------------- | --------------------------------------------- | ---------------------------------------- |
| A      | First Name                         | Alice                                         | Used for username / display              |
| H      | Joining Date                       | 2019-06-01                                    | Must be a real date                      |
| I      | Email                              | [alice@company.com](mailto:alice@company.com) | For employee info string                 |
| J      | Eligible for promotion             | YES / NO                                      | Calculated (see rule)                    |
| K      | Department                         | HR / IT / Sales                               | Used for headcount and info string       |
| L      | Standard Bonus %                   | 6 / 7 / …                                     | Optional: combine with Salary if present |
| M      | employee info                      | Alice \| HR \| alice@…                        | Calculated display string                |
| N      | Username                           | alice                                         | Calculated (lowercased first name)       |
| O      | Years worked                       | 3 / 4 / 5 / …                                 | Calculated                               |
| P      | How many employees are in IT (KPI) | 2                                             | Single-cell result                       |

#Business Questions
-Years worked for each employee.

-Promotion eligibility using the rule Years worked > 3 ⇒ YES.

-IT headcount (how many rows have Department = “IT”).

-Handy employee info strings and usernames for quick exports.

#Results (from the shared sample)
-IT headcount: 2 (cell P1)

-Promotion rule: “YES” when Years worked > 3

-Helper fields built: employee info (M) and Username (N)

-Example Years worked by row: 3, 4, 5, 2, 6

#How to View
-Open workbooks/ASSIGNMENT 2. CHIKA CELESTINE IROEGBULEM.xlsx.

-Go to the DATA SET sheet.

-Check columns O (Years worked) and J (Eligible for promotion).

-Verify employee info (M) and Username (N).

-See P1 for the IT headcount KPI.

-For a quick glance without downloading, view the image in outputs/screenshots/.
#Skills & Tools
-Excel: DATEDIF, IF, COUNTIF, text concatenation, basic KPI design, light pivoting.
-Communication: Clear rule definition for eligibility, readable helper fields for ops.
