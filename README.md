# IBM HR Attrition Dashboard (Data Studio / Looker Studio)

A two-page interactive HR dashboard design for the IBM HR Analytics dataset (`HR_Analytics_Final_Dataset.xlsx`: 1,470 employees, 35 columns, no missing values). Page 1 is a basic overview; Page 2 uses five calculated fields to show attrition rates by segment. Every figure below was calculated from the data and cross-checked in the Excel working file, where each number is a live formula. The dashboard itself is built in Data Studio by following `datastudio_build_guide.md`.

---

## Executive Summary

- **Attrition:** 237 of 1,470 employees left, a rate of **16.1%**.
- **By department:** Sales **20.6%**, Human Resources **19.0%**, Research & Development **13.8%**. R&D has the most leavers (133) but the lowest rate.
- **By age:** employees aged 18-25 leave at **35.8%**, 2.2 times the company rate; 36-45 is the most stable group (9.2%).
- **By income:** the lowest bracket (under 3,000 a month) leaves at **28.6%**, the highest (10,000+) at **8.9%**.
- **By satisfaction:** low job satisfaction 22.8% vs very high 11.3%.
- **Overtime:** employees working overtime leave at **30.5%** vs 10.4% without. This is the largest single gap in the data.
- **Travel:** frequent travellers leave at 24.9%, non-travellers at 8.0%.
- **Roles:** Sales Representatives (39.8%), Laboratory Technicians (23.9%) and Human Resources staff (23.1%) have the highest rates; Research Directors (2.5%) and Managers (4.9%) the lowest.

---

## Page 1: HR Overview (basic)

| Element | Result |
| :--- | :--- |
| Total employees | 1,470 |
| Employees who left | 237 |
| Average monthly income | 6,503 (currency not stated in the data) |
| Average age | 36.9 |
| Attrition split (donut) | Yes 16.1%, No 83.9% |
| Leavers by department | R&D 133, Sales 92, Human Resources 12 |
| Employees by job role | Sales Executive 326, Research Scientist 292, Laboratory Technician 259, Manufacturing Director 145, Healthcare Representative 131, Manager 102, Sales Representative 83, Research Director 80, Human Resources 52 |
| Gender | Male 882 (60%), Female 588 (40%) |
| Attrition by business travel (Yes / No) | Non-Travel 12 / 138, Travel_Rarely 156 / 887, Travel_Frequently 69 / 208 |
| Filters | Department, Gender, OverTime |

## Page 2: Advanced analysis (calculated fields)

| Segment | Attrition rate (employees) |
| :--- | :--- |
| Department | Sales 20.6% (446), Human Resources 19.0% (63), R&D 13.8% (961) |
| Age Group | 18-25 35.8% (123), 26-35 19.1% (606), 36-45 9.2% (468), 46-60 12.5% (273) |
| Income Bracket | 1-Low 28.6% (395), 2-Mid 12.7% (519), 3-Upper-Mid 12.0% (275), 4-High 8.9% (281) |
| Satisfaction Level | 1 - Low 22.8% (289), 2 - Medium 16.4% (280), 3 - High 16.5% (442), 4 - Very High 11.3% (459) |

Pivot (Department x Gender): Human Resources female 30.0% (20 employees) vs male 14.0% (43); R&D female 11.3% (379) vs male 15.5% (582); Sales female 20.1% (189) vs male 21.0% (257).

Calculated fields: Attrition Flag, Attrition Rate, Age Group, Income Bracket, Satisfaction Level (formulas are in the build guide).

---

## Recommendations

- **Early-career retention:** the 18-25 group leaves at more than twice the company rate; target onboarding, mentoring and career paths.
- **Look at overtime:** a 30.5% vs 10.4% gap makes workload the first lever to test, especially in Sales and Laboratory roles.
- **Review pay in the lowest bracket:** nearly 3 in 10 employees under 3,000 a month leave.
- **Prioritise Sales:** the highest department rate, and Sales Representatives leave at almost 40%.
- **Track satisfaction and travel:** low satisfaction and frequent travel both go with higher attrition.
- **Use rates, not counts:** R&D has the most leavers but is the most stable large department.

---

## Corrections to the lecture guide

- The guide says the data has 32 fields; the file has **35** columns.
- The guide says low-income attrition is "40%+" and high-income "below 5%". The data gives **28.6%** and **8.9%**: the direction is right, the size is smaller.
- The guide shows the rupee symbol for income, but the data does not state a currency.
- The guide's title says "2024"; the data has no date field.

All other expected values in the guide's checklist match the data (1,470; 237; 6,503; 36.9; 133 / 92 / 12; Sales 20.6%, HR 19.0%, R&D 13.8%; 18-25 at 35.8%).

---

## Repository Structure

```text
├── data/
│   └── HR_Analytics_Final_Dataset.xlsx
├── working_files/
│   └── HR_Attrition_DataStudio_Working_File.xlsx
├── screenshots/
│   ├── hr_dashboard_page1_preview.png
│   └── hr_dashboard_page2_preview.png
├── presentation/
│   └── HR Attrition Analytics.pptx
├── datastudio_build_guide.md
└── README.md
```

### Excel working file

| Sheet | Contents |
| :--- | :--- |
| Page1_Overview | KPIs, donut, department, job role, gender and travel tables (live formulas) |
| Page2_Advanced | Attrition rate by department, age group, income bracket, satisfaction, overtime, job role, and the department x gender pivot |
| Calculated_Fields | The five Data Studio formulas |
| Notes | Assumptions and corrections |
| Data | The 1,470 employees plus the four calculated columns (orange headers) |

---

## Limitations

- **Association, not causation.** Attrition rates describe patterns, not reasons.
- **Small groups are noisy:** Human Resources has 63 employees, so its department-by-gender cells are very small.
- **No dates:** the data is a snapshot, so no trends over time can be shown.
- **Screenshots:** the two PNG files are drawn in Python from the data as previews of the Data Studio layout. They are not Data Studio exports; replace them with your own screenshots once the dashboard is built.
