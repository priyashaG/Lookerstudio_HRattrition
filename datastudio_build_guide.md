# Data Studio build guide (IBM HR attrition dashboard)

Data Studio is now called Looker Studio (lookerstudio.google.com). The steps and fields are the same. Check each number against `README.md` as you build.

## 1. Data
1. Upload `HR_Analytics_Final_Dataset.xlsx` to Google Sheets (File > Import > Replace spreadsheet, keep "Convert text to numbers and dates"). Name the sheet `HR Data`.
2. Check: 1,471 rows (header + 1,470), 35 columns.
3. In Looker Studio: Create > Report > Google Sheets > your sheet. Rename the report and the pages (`HR Overview Dashboard`, `Advanced Attrition Analysis`).

## 2. Page 1: expected values
| Element | Setup | Expected |
| :--- | :--- | :--- |
| Scorecard: employees | Record Count | 1,470 |
| Scorecard: left | Record Count, filter Attrition = Yes | 237 |
| Scorecard: income | AVG(MonthlyIncome) | 6,503 |
| Scorecard: age | AVG(Age), 1 decimal | 36.9 |
| Donut | Dimension Attrition, Record Count, % labels | 16.1% Yes / 83.9% No |
| Bar | Dimension Department, Record Count, filter Attrition = Yes | R&D 133, Sales 92, HR 12 |
| Horizontal bar | Dimension JobRole, Record Count | Sales Executive 326, Research Scientist 292, Laboratory Technician 259 ... |
| Pie | Dimension Gender, Record Count | Male 882, Female 588 |
| 100% stacked bar | Dimension BusinessTravel, breakdown Attrition | Yes share: 8.0%, 15.0%, 24.9% (Non-Travel, Rarely, Frequently) |
| Filter controls | Department, Gender, OverTime (use Insert > Control, not chart filters) | all charts update |

## 3. Calculated fields (Resource > Manage added data sources > Edit > Add a field)
Type them by hand; pasting can add curly quotes.

| Field | Formula |
| :--- | :--- |
| Attrition Flag | `CASE WHEN Attrition = 'Yes' THEN 1 ELSE 0 END` |
| Attrition Rate | `SUM(Attrition Flag) / COUNT(EmployeeNumber)` (set Type = Percent) |
| Age Group | `CASE WHEN Age <= 25 THEN "18-25" WHEN Age <= 35 THEN "26-35" WHEN Age <= 45 THEN "36-45" ELSE "46-60" END` |
| Income Bracket | `CASE WHEN MonthlyIncome < 3000 THEN "1-Low" WHEN MonthlyIncome < 6000 THEN "2-Mid" WHEN MonthlyIncome < 10000 THEN "3-Upper-Mid" ELSE "4-High" END` |
| Satisfaction Level | `CASE WHEN JobSatisfaction = 1 THEN "1 - Low" WHEN JobSatisfaction = 2 THEN "2 - Medium" WHEN JobSatisfaction = 3 THEN "3 - High" WHEN JobSatisfaction = 4 THEN "4 - Very High" ELSE "Unknown" END` |

Use the numbered income labels from the start so alphabetical sort gives the right order. Check: SUM(Attrition Flag) = 237 and Attrition Rate = 16.1%.

## 4. Page 2: expected values
| Chart | Dimension / Metric | Expected |
| :--- | :--- | :--- |
| A | Department / Attrition Rate (reference line at 16.1%) | Sales 20.6%, HR 19.0%, R&D 13.8% |
| B | Age Group / Attrition Rate | 35.8%, 19.1%, 9.2%, 12.5% |
| C | Income Bracket / Attrition Rate | 28.6%, 12.7%, 12.0%, 8.9% |
| D | Satisfaction Level / Attrition Rate | 22.8%, 16.4%, 16.5%, 11.3% |
| E | Pivot: rows Department, columns Gender / Attrition Rate | HR F 30.0% M 14.0%; R&D F 11.3% M 15.5%; Sales F 20.1% M 21.0% |
| Filters | JobRole, Age Group, Income Bracket, OverTime | |

Optional extra chart: OverTime / Attrition Rate (30.5% Yes vs 10.4% No), the strongest split in the data.

## 5. Finish
Add the page navigation buttons, test every filter in View mode, then Share > Anyone with the link > Viewer. Take your own screenshots of both pages and save them as `screenshots/hr_dashboard_page1.png` and `page2.png`.

## Known differences from the lecture guide
The data has 35 columns (not 32); low-income attrition is 28.6% (not 40%+) and high-income 8.9% (not under 5%); the data has no currency or year.
