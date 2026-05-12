# Project Title: Workforce Analytics and Operational Performance Report
## Table of Content
- [Executive Summary](#executive-summary)
- [Project Overview](#project-overview) 
- [Building Stakeholders Trust in the Insight](#building-stakeholders-trust-in-the-insight)
- [Data Cleaning and Preparation Steps](#data-cleaning-and-preparation-steps)
- [Assumptions and Analytical Decisions](#assumptions-and-analytical-decisions)
- [Key Insights and Findings](#key-insights-and-findings)
- [Conclusion](#conclusion)





## Executive Summary
This project analysed employee workforce and performance data to understand staffing levels, employee availability, and productivity trends over time. The goal was to turn raw workforce data into clear insights that could support workforce planning and operational decision-making.

The analysis was completed in Microsoft Power BI using Power Query for data cleaning and DAX for calculations and reporting. A structured data model was built to ensure accurate analysis across different reporting periods.

A major part of the project involved improving data quality. The original datasets contained issues such as inconsistent dates, duplicate fields, missing values, and calculation errors. These problems were cleaned and validated before analysis to ensure reliable results. Key workforce metrics, including Availability % and Occupancy %, were rebuilt using business rules instead of relying on source calculations.

The analysis focused on three main areas:
- Workforce capacity and contracted hours over time
- Employee availability trends
- How productivity changed as employees gained experience in their roles

The findings showed that workforce staffing levels remained mostly stable before increasing towards the end of 2025 and early 2026, suggesting workforce growth. Employee availability also stayed fairly consistent, although there was a temporary drop towards the end of 2025.

The analysis also showed that employees became more productive as they gained experience. Occupancy levels were lower during the early months of employment but increased steadily before stabilising over time.

Throughout the project, unexpected results and data anomalies were investigated carefully to ensure the insights reflected real operational patterns rather than data errors.

Overall, the project demonstrated how Power BI and structured analytical methods can transform raw workforce data into reliable business insights through validated KPIs, trend analysis, and interactive reporting dashboards.

# Project Overview
This project focused on analysing workforce capacity, availability, and operational productivity using employee and performance data provided across multiple Excel worksheets. The objective was to transform raw operational data into meaningful business insights that could support workforce planning, performance monitoring, and operational decision-making.

The dataset consisted of four primary components: employee information, monthly performance records, business metric definitions, and analytical questions. The employee dataset contained workforce attributes such as operational area, FTE values, banding, weekly working hours, and employee start dates. The performance dataset contained monthly operational metrics including contracted hours, available hours, occupied hours, availability percentages, and occupancy percentages. Supporting documentation was also provided to define the meaning and business logic behind each metric.

The project was developed using Microsoft Power BI Desktop, with Power Query used for data cleaning and transformation, and DAX used for business calculations and analytical modelling. A structured analytical workflow was followed, beginning with data profiling and quality assessment before progressing into transformation, modelling, metric validation, visualisation, and business interpretation.

A significant portion of the work focused on improving data quality and ensuring analytical reliability. The source data contained several issues including duplicate date fields, mixed UK and US date formats, null values, blank records, inconsistent formatting, and calculation errors. These issues were addressed systematically within Power Query to ensure that the final analysis remained accurate, reproducible, and aligned with business definitions.

The project ultimately addressed three key analytical objectives:
- Calculate the typical number of contracted hours per FTE and analyse workforce FTE trends over time.
- Analyse and visualise workforce availability trends across reporting periods.
- Evaluate how occupancy levels changed as a function of employee tenure and time since start date.

To support these objectives, a relational data model was developed using a star-schema-style structure, including a dedicated Date table for time-based analysis. Business metrics such as Availability % and Occupancy % were recreated as DAX measures using the formal business definitions provided, ensuring consistency and reducing reliance on potentially unreliable source calculations.

The final dashboard combined KPI indicators, trend analysis, tenure-based productivity analysis, and interactive slicers to allow users to explore workforce behaviour across operational areas, reporting periods, and employee groups. Each visualisation was accompanied by concise business interpretations to ensure that the outputs remained understandable and actionable for both technical and non-technical stakeholders.

Overall, the project demonstrated the end-to-end business intelligence workflow, including data preparation, modelling, analytical validation, DAX development, visualisation, and insight communication. The analysis prioritised analytical integrity and business relevance to ensure that the resulting insights accurately reflected operational workforce performance.

# Building Stakeholders Trust in the Insight
A major way I built stakeholder confidence in the insights was by ensuring that the analysis process was transparent, logically consistent, and closely aligned with the business definitions provided in the dataset documentation. Rather than relying solely on the raw outputs from the source data, I validated calculations, investigated anomalies, and structured the analysis in a way that made the findings both technically reliable and easy to interpret.

The first step in building confidence was establishing a strong data quality foundation. The source data contained several issues, including duplicate date columns, inconsistent date formats, null values, blank records, and calculation errors such as #DIV/0!. To address this, I performed all data cleaning and transformation processes within Power Query in Power BI. This ensured the workflow remained reproducible, transparent, and auditable, while preserving the integrity of the raw source data. I standardised column names, corrected date formats using UK locale settings, removed invalid and blank rows, handled missing values appropriately, and validated numeric data types before beginning any analytical work.

I also ensured that the data model itself reflected proper business intelligence design principles. A dedicated Date table was created to support accurate time-based analysis and chronological sorting, and a one-to-many relationship was established between the Users table and the Performance Data table to maintain consistency between workforce attributes and monthly operational metrics. Structuring the model in this way reduced ambiguity in calculations and ensured that all visualisations responded consistently to filters and slicers.

Another important aspect of building stakeholder trust was validating the business logic behind the metrics rather than assuming the source calculations were correct. Although the dataset already contained Availability % and Occupancy % fields, I recreated these calculations in DAX using the formal definitions provided in the documentation. This ensured that the reported metrics were directly traceable to the agreed business rules and prevented issues caused by source-level errors or inconsistent aggregations. For example:
  - Availability %= Contracted Hours / Available Hours

    and
    
  - Occupancy %= Available Hours / Occupied Hours

were implemented as controlled DAX measures rather than relying on imported percentage fields.

A particularly important moment in the project involved validating the “Contracted Hours per FTE” calculation. An initial aggregation produced an unrealistic value exceeding 1,200 hours per FTE, which immediately suggested a granularity issue between the static Users table and the monthly Performance Data table. Instead of accepting the result at face value, I investigated the relationship between reporting grain and aggregation context. 

By aligning the calculation with the business definition that 1 FTE corresponds to approximately 37 hours per week, I refined the logic to produce a realistic monthly equivalent of approximately 148 hours per FTE. This validation process significantly increased confidence that the analysis reflected operational reality rather than a technical aggregation error.

I also investigated anomalies rather than automatically treating them as bad data. During the tenure analysis, negative “Months Since Start” values initially appeared problematic. However, after inspecting the records in detail, I identified that these observations were consistently associated with zero contracted hours, indicating that they were likely pre-activation or onboarding placeholder records rather than incorrect dates. Rather than manually altering the dates, I applied business-driven filtering logic by excluding non-contracted records from the occupancy analysis. This ensured that the final insight focused only on operationally active employees while preserving the integrity of the underlying source data.

To further support stakeholder understanding and trust, I complemented each visualisation with concise written interpretations explaining the operational meaning of the trends observed. This helped bridge the gap between technical outputs and business interpretation by clearly explaining patterns such as workforce expansion, stable availability levels, and the relationship between employee tenure and productivity. Adding contextual explanations reduced the risk of misinterpretation and made the dashboard more accessible to non-technical audiences.

Finally, I designed the report to encourage transparency and interactivity. Slicers for Operational Area, Band, and Reporting Month allowed stakeholders to independently explore the data and validate trends across different workforce segments. This interactive capability helped reinforce confidence in the insights by enabling users to test assumptions and observe how metrics behaved under different filtering conditions.

Overall, stakeholder confidence was built through a combination of rigorous data validation, transparent modelling practices, alignment with formal business definitions, careful anomaly investigation, and clear communication of findings. Rather than focusing solely on producing visuals, the project prioritised analytical integrity and traceability to ensure the insights were both accurate and operationally meaningful.

# Data Cleaning and Preparation Steps
A structured data cleaning and preparation process was carried out to ensure that the analysis was accurate, reliable, and suitable for workforce performance reporting. All transformation activities were completed within Power Query in Microsoft Power BI Desktop to maintain transparency, reproducibility, and separation between the raw source data and the analytical model.

## Initial Data Profiling
The first stage involved profiling the imported datasets to identify the following:
- Null and blank values
- Duplicate records
- Inconsistent date formats
- Invalid calculations and errors
- Incorrect data types
- Inconsistent categorical values

Column quality, column distribution, and column profiling tools within Power Query were used to assess the overall condition of the data before transformation began.

## Users Table Cleaning
The Users table contained workforce attributes such as operational area, employee identifiers, FTE values, bands, start dates, and weekly working hours.

The following cleaning steps were performed:
### Removal of Redundant and Empty Columns
- Duplicate and incorrectly labelled date columns were identified and removed.
- Empty columns and fully blank rows were deleted to improve model clarity and reduce noise.
  
### Standardisation of Column Names
- Column headers were renamed using consistent naming conventions to improve readability and simplify modelling and DAX development.
  
### Date Standardisation
The dataset contained mixed UK and US date formats. To ensure dates were interpreted correctly:
- Locale-aware date conversion was applied using UK regional settings.
- Start Date fields were converted into proper date data types.

### Data Type Validation
The following fields were converted into appropriate data types:
- FTE → Decimal Number
- Weekly Hours → Decimal Number
- Start Date → Date

### Null Handling
Rows missing critical identifiers, such as User values were removed because they could not support relational analysis or workforce tracking.

### Text Cleaning
Text-based fields such as User, Operational Area, and Band were cleaned using Trim and Clean transformations to remove trailing spaces and hidden characters that could affect relationships and filtering behaviour.

## Performance Data Table Cleaning
The Performance Data table contained monthly operational workforce metrics including contracted, available, and occupied hours.

The following cleaning activities were completed:
### Removal of Blank Rows
Completely empty records were removed from the dataset to prevent invalid aggregation and filtering behaviour.

### Reporting Month Standardisation
The Reporting Month field was:
- Converted into a valid date field
- Standardised using UK locale settings
- Validated for chronological consistency
  
### Numeric Type Validation
Operational metrics were converted into decimal numeric formats, including:
- Contracted Hours
- Available Hours
- Occupied Hours

Percentage fields were formatted appropriately for analytical calculations and visualisation.

### Error Handling
Invalid calculations such as #DIV/0! were identified and replaced using controlled logic to prevent errors propagating into the analytical layer.

### Null and Blank Value Handling
Operational hour fields were reviewed and handled according to business meaning:
- Blank operational values were standardised where appropriate
- Records lacking meaningful operational context were excluded when necessary

### Relationship Validation
User identifiers were cleaned and validated to ensure successful one-to-many relationships between the Users table and the Performance Data table.

## Date Table Creation
A dedicated Date table was created within Power BI to support:
- Time intelligence
- Chronological sorting
- Trend analysis
- Consistent monthly reporting

Additional calculated fields such as Year, Month Name, Month-Year, and Year-Month sort keys were created to improve reporting usability and visual ordering.

## Business Logic Validation
Rather than relying entirely on source-calculated percentage fields, key business metrics were recreated using DAX measures based on the formal business definitions provided in the dataset documentation.

This included:
- Availability %
- Occupancy %
- Contracted Hours per FTE

This approach improved consistency and reduced reliance on potentially inaccurate source-level calculations.

## Anomaly Investigation and Filtering
During tenure analysis, negative “Months Since Start” values were identified. Investigation revealed that these records consistently corresponded with zero contracted hours, suggesting that they represented pre-activation or onboarding placeholder records rather than incorrect dates.

To maintain analytical relevance:
- Non-operational records with zero contracted hours were excluded from occupancy trend analysis.
- Business-driven filtering logic was applied rather than arbitrary deletion or manual alteration of source values.

## Data Modelling Validation
After cleaning, relationships between tables were validated to ensure:
- Correct one-to-many cardinality
- Proper filter propagation
- Consistent behaviour across visuals and slicers

A star-schema-style structure was implemented to improve analytical performance and maintain model clarity.

## Outcome
The data cleaning process transformed the raw source files into a structured, validated, and analysis-ready data model suitable for workforce trend analysis and operational performance reporting. The final dataset supported reliable KPI calculation, accurate trend visualisation, and meaningful business interpretation.

# Assumptions and Analytical Decisions
Several assumptions and analytical decisions were made during the project to ensure that the analysis remained logically consistent, operationally meaningful, and aligned with the available data structure. These assumptions were necessary because the dataset contained incomplete contextual information and certain business processes were not explicitly documented.

## FTE Interpretation
The project assumed that FTE values represented workforce capacity relative to a standard full-time working pattern of approximately 37 hours per week, based on the formal definition provided in the dataset documentation.

As the Performance Data table was reported monthly, the “Contracted Hours per FTE” calculation was interpreted as a monthly equivalent rather than a weekly measure. Therefore, a typical monthly contracted hour value of approximately 148 hours per FTE was considered operationally reasonable and consistent with the business definition.

## Active Workforce Assumption
The dataset did not contain employee end dates or explicit workforce status indicators. As a result, workforce participation within a reporting period was inferred from user presence within the monthly Performance Data table.

For the purpose of monthly FTE trend analysis, users appearing within a given reporting month were treated as operationally active during that period.

## Handling of Negative Tenure Values
During the tenure analysis, some records produced negative “Months Since Start” values, meaning the reporting month preceded the recorded employee start date.

Further investigation showed that these records consistently had zero contracted hours and were likely to represent:
- Pre-activation employee records
- Onboarding placeholders
- Administrative setup periods

Rather than treating these as data entry errors, the analysis assumed that these records did not represent operational workforce activity.

Consequently:
- Records with zero contracted hours were excluded from the occupancy-by-tenure analysis to ensure that only operationally active workforce records contributed to productivity insights.

## Availability and Occupancy Calculation Assumptions
Although the dataset included pre-calculated Availability % and Occupancy % fields, these values were not relied upon directly because:
- Some rows contained invalid calculations such as #DIV/0!
- Certain percentage values exceeded expected operational ranges
- Source aggregation logic could not be fully verified

To improve reliability, Availability % and Occupancy % were recalculated using DAX measures based on the formal business definitions provided in the documentation.

## Null and Blank Value Handling
Null and blank values were handled selectively based on business context rather than through blanket replacement rules.

The following assumptions guided the treatment of missing data:
- Rows missing critical identifiers such as User values were considered analytically unusable and removed.
- Fully blank records were treated as non-operational data artefacts and excluded.
- Blank operational hour values were interpreted according to their business meaning before replacement or exclusion decisions were made.

## Time Intelligence Assumptions
A dedicated Date table was created to support chronological reporting and time-based analysis. Reporting periods were assumed to represent monthly operational snapshots, and trend analysis was therefore performed at monthly granularity.

Month-Year labels were sorted using custom Year-Month keys to ensure chronological sequencing across reporting periods.

## Workforce Productivity Interpretation
Occupancy % was interpreted as an operational productivity indicator representing the proportion of available workforce time spent on meaningful work activities.

The occupancy-by-tenure analysis assumed that changes in Occupancy % over time could reflect:
- Onboarding and training effects
- Operational integration
- Workforce experience and efficiency
However, the analysis did not assume direct causation, as additional contextual operational data was not available.

## Scope Limitation Assumptions
The project assumed that:
- The supplied datasets represented complete operational reporting for the period provided.
- No external workforce or HR systems were required to validate the core business metrics.
- The analysis was intended for operational trend evaluation rather than formal financial or regulatory reporting.

## Overall Analytical Approach
Where uncertainty existed, assumptions were guided by:
- The formal business definitions provided
- Observable data patterns
- Operational plausibility
Consistency with workforce reporting practices

All assumptions were applied transparently and were intended to preserve analytical integrity while ensuring that the resulting insights remained operationally meaningful and defensible.

# Key Insights and Findings
## 1. FTE Trend Over Time
The workforce FTE trend remained relatively stable throughout most of 2025, indicating a generally consistent level of operational workforce capacity across the reporting period. A moderate decline was observed during the middle of the year, followed by a steady increase from approximately September 2025 onwards, with workforce capacity reaching its highest level in January 2026.

This pattern may suggest:
- gradual workforce expansion towards the end of the reporting period,
- increased staffing activity,
- or operational scaling in response to business demand.

The analysis also identified that the typical contracted hours per FTE was approximately 147.66 hours per reporting period. This aligned closely with the expected monthly equivalent of a full-time employee based on the business definition that 1 FTE corresponds to approximately 37 hours per week. This provided additional confidence that workforce capacity calculations were operationally consistent and analytically reliable.

## 2. Availability Percentage Trend
Availability levels remained broadly stable throughout most of the reporting period, fluctuating around the long-term average of approximately 78–80%. This indicated that the proportion of contracted workforce time available for operational work remained relatively consistent across most reporting months.

However, a noticeable decline occurred towards the end of 2025, particularly during December 2025, before partially recovering in January 2026. This temporary reduction in availability may reflect:
- seasonal workforce pressures,
- increased leave or absence levels,
- operational disruptions,
- or year-end organisational activities impacting workforce availability.

Despite this fluctuation, the overall trend suggested that workforce availability remained reasonably stable and operationally sustainable across the reporting period.

## 3. Occupancy Percentage by Employee Tenure
The occupancy-by-tenure analysis revealed a strong relationship between workforce occupancy levels and employee tenure.
Occupancy levels were relatively low during the earliest stages of employment, beginning below 20% during the initial months after employee onboarding. However, occupancy increased rapidly during the first several months of tenure before stabilising around the long-term average after approximately 6–8 months.

This pattern suggests:
- a workforce onboarding and integration effect,
- gradual improvement in operational productivity,
- and increasing employee contribution as familiarity with systems, processes, and responsibilities develops over time.

After the initial growth period, occupancy levels remained relatively stable with only moderate fluctuations across longer tenure periods, indicating that employees generally maintained consistent operational productivity once fully integrated into their roles.

## Insight Summary
The analysis demonstrated that workforce capacity, availability, and productivity remained generally stable across the reporting period, while also highlighting important operational dynamics related to employee tenure and workforce utilisation.

The findings suggest that:
- workforce capacity expanded moderately towards the end of the reporting period,
- workforce availability remained operationally resilient despite short-term fluctuations,
- and employee productivity improved significantly during early tenure before stabilising at a sustainable operational level.

Overall, the project provided a structured view of workforce operational performance and demonstrated how workforce analytics can be used to support capacity planning, operational monitoring, and employee productivity evaluation.

# Conclusion

This project successfully turned raw workforce and performance data into a clear and reliable workforce analytics solution using Microsoft Power BI. The work included data cleaning, data modelling, DAX calculations, visualisation, and business analysis to understand workforce capacity, employee availability, and productivity trends over time.

A major focus of the project was ensuring accuracy and reliability. Key workforce metrics were rebuilt and validated using official business definitions rather than relying only on source calculations. Data issues and unusual results were carefully investigated to make sure the analysis reflected real operational patterns.

The analysis showed that workforce capacity stayed mostly stable before increasing towards the end of 2025, while employee availability remained generally consistent with some temporary fluctuations. It also showed that employees became more productive as they gained experience in their roles.

The project demonstrated both technical and business-focused analytical skills, including:
- cleaning and validating data,
- building a reliable data model,
- creating and testing DAX calculations,
- investigating anomalies,
- and communicating insights clearly to stakeholders.

The final Power BI dashboard provides an interactive and scalable way to monitor workforce performance and supports workforce planning and operational decision-making. Overall, the project demonstrates a complete end-to-end business intelligence workflow focused on data quality, transparency, and actionable insights.

