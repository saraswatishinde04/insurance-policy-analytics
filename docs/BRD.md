# Business Requirements Document (BRD)

**Project:** Insurance Policy Analytics – Executive Dashboard  
**Author:** Saraswati Sarjerao Shinde · [LinkedIn](https://www.linkedin.com/in/saraswati-shinde/) · [Portfolio](https://saraswatishinde04.github.io/3D_Portfolio/)

## 1. Document Control

| Field | Details |
|---|---|
| Project Name | Insurance Policy Analytics – Executive Dashboard |
| Document Version | 1.0 |
| Prepared By | Saraswati Sarjerao Shinde (Business Analyst) |
| Document Type | Business Requirements Document |
| Status | Final |
| Tools | MySQL, Power BI |

## 2. Purpose of the Document

This BRD defines the business needs, scope, requirements and acceptance criteria for building an Insurance Policy Analytics dashboard. It acts as the single reference between the business stakeholders and the analytics/BI team.

## 3. Business Background

The insurance company holds customer, policy, claims and payment data in separate sheets. Leadership has no consolidated, self-service view of portfolio health, so questions about active policies, premium trends and renewals take significant manual effort to answer.

## 4. Problem Statement

Leadership cannot quickly see how many policies are active, how premiums are trending, or when large numbers of policies will end. This leads to delayed retention actions, unplanned renewal workload and missed cross-sell opportunities.

## 5. Business Objectives

| ID | Objective | Success Measure |
|---|---|---|
| BO-01 | Provide one consolidated view of portfolio performance | Single dashboard covering all 21 KPI questions |
| BO-02 | Improve visibility of policy retention | Active vs inactive % visible and filterable |
| BO-03 | Monitor premium performance over time | Avg premium and growth % shown by start year |
| BO-04 | Prepare for renewal workload | Policies by end year with peak identified |
| BO-05 | Identify growth opportunities | Count of customers without a policy reported |

## 6. Scope

**In scope**
- Data from Customer Information, Policy Details, Claims, Payment History and Additional Fields
- SQL queries answering 21 KPI questions
- 3-page Power BI report (Executive Overview, Premium & Policy Lifecycle Trends, Summary)
- Filters for Payment Method, Payment Status and Year
- Insights, recommendations and data-quality notes

**Out of scope**
- Predictive modelling or machine-learning forecasts
- Real-time or automated data refresh from a live production system
- Claims fraud detection
- Row-level security and user access management

## 7. Stakeholders

| Stakeholder | Role | Interest |
|---|---|---|
| Senior Management / Executives | Primary consumer | Portfolio health, strategic decisions |
| Sales & Marketing Head | Consumer | Cross-sell and customer targeting |
| Operations / Renewals Team | Consumer | Renewal planning and workload |
| Pricing / Actuarial Team | Consumer | Premium trends and pricing review |
| Business Analyst | Author | Requirements, analysis, dashboard delivery |

## 8. Business Requirements

| ID | Requirement | Priority |
|---|---|---|
| BR-01 | The business needs to see total customers, total policies, total claim amount, average coverage and average premium at a glance | High |
| BR-02 | The business needs to know the share of active vs inactive policies | High |
| BR-03 | The business needs to segment policies by age group, gender, policy type and status | High |
| BR-04 | The business needs to track average premium and premium growth by start year | High |
| BR-05 | The business needs to see how many policies end each year and when the peak occurs | High |
| BR-06 | The business needs to filter views by payment method, payment status and year | Medium |
| BR-07 | The business needs a written summary with recommendations | High |
| BR-08 | The business needs to identify customers with no policy | Medium |

## 9. Functional Requirements

| ID | Requirement | Linked BR |
|---|---|---|
| FR-01 | Display KPI cards: Total Customers, Total Policies, Total Claim Amount, Average Coverage Amount, Average Premium Amount | BR-01 |
| FR-02 | Display a donut chart of Active vs Inactive policy % | BR-02 |
| FR-03 | Display bar charts for policies by age group, gender, policy type and status | BR-03 |
| FR-04 | Display a combo chart of average premium (bars) and average premium growth % (line) by start year | BR-04 |
| FR-05 | Display a line chart of total policies by end year with data labels | BR-05 |
| FR-06 | Display growth KPI cards: Avg Growth, Highest Growth, Lowest Growth, Growth Difference, Peak Policies Ending | BR-04, BR-05 |
| FR-07 | Provide slicers for Payment Method, Payment Status and Year that filter all relevant visuals | BR-06 |
| FR-08 | Provide navigation buttons between the three report pages | BR-07 |
| FR-09 | Provide a Summary page with "What this means", Recommendations and Notes | BR-07 |
| FR-10 | Report the number of customers with no policy | BR-08 |
| FR-11 | Source all figures from the MySQL database `policy_analytics` | All |

## 10. Non-Functional Requirements

| ID | Category | Requirement |
|---|---|---|
| NFR-01 | Usability | Dashboard readable by non-technical users with clear titles and labels |
| NFR-02 | Consistency | Uniform navy and yellow colour theme and layout across pages |
| NFR-03 | Performance | Pages load and slicers respond in a few seconds on the ~5K-record dataset |
| NFR-04 | Accuracy | Dashboard values match the SQL query results |
| NFR-05 | Maintainability | DAX measures named clearly and the data model documented |
| NFR-06 | Data quality | Known data issues are disclosed on the Summary page |
| NFR-07 | Compatibility | Report opens in Power BI Desktop and can be published to Power BI Service |

## 11. KPI Definitions

| KPI | Definition |
|---|---|
| Total Customers | Count of distinct customers |
| Total Policies | Count of distinct policies |
| Total Claim Amount | Sum of all claim amounts |
| Average Coverage Amount | Average coverage amount across policies |
| Average Premium Amount | Average premium across policies |
| Active Policy % | Active policies ÷ total policies |
| Inactive Policy % | Lapsed + terminated policies ÷ total policies |
| Avg Premium Growth % | Year-over-year change in average premium, by start year |
| Growth Difference | Highest growth % minus lowest growth % (in percentage points) |
| Peak Policies Ending | Highest number of policies ending in a single year |

## 12. Data Requirements

| Item | Detail |
|---|---|
| Source | `Policy_Data.xlsx` (5 sheets) |
| Storage | MySQL database `policy_analytics` |
| Keys | Customer ID and Policy ID link the tables |
| Volume | ~5,000 customers and ~5,000 policies |
| Refresh | Manual refresh in Power BI |

## 13. Assumptions

- The dataset is a complete and fair sample of the portfolio
- Customer ID and Policy ID are reliable keys across tables
- Policy status values (Active, Lapsed, Terminated) are correctly recorded
- Inactive = Lapsed + Terminated

## 14. Constraints

- Data appears synthetic, so conclusions are directional
- Gender values are unreliable
- Start year 2014 is a partial year (11 policies)
- Manual refresh only; no automated pipeline

## 15. Risks and Mitigation

| Risk | Impact | Mitigation |
|---|---|---|
| Poor data quality (gender, partial years) | Misleading segment insights | Disclose in Notes; exclude partial years from growth averages |
| Slicers not filtering all visuals | Inconsistent numbers | Define relationships correctly and test every slicer |
| Mismatch between SQL and dashboard | Loss of trust | Reconcile dashboard totals with SQL output |
| Misreading synthetic data as real | Wrong business decisions | State clearly that results are patterns to investigate |

## 16. Acceptance Criteria

- [ ] All 21 KPI questions are answered with SQL and reflected in the dashboard
- [ ] KPI card values match SQL results
- [ ] Slicers filter all relevant visuals
- [ ] All three pages are navigable and consistently designed
- [ ] Summary page states insights, recommendations and notes
- [ ] Known data limitations are documented

## 17. Requirements Traceability Matrix

| Business Objective | Business Requirement | Functional Requirement | Dashboard Element |
|---|---|---|---|
| BO-01 | BR-01 | FR-01, FR-11 | KPI cards (Page 1) |
| BO-02 | BR-02 | FR-02 | Active vs Inactive donut |
| BO-02 | BR-03 | FR-03 | Age, Gender, Type, Status charts |
| BO-03 | BR-04 | FR-04, FR-06 | Premium and growth combo chart |
| BO-04 | BR-05 | FR-05, FR-06 | Policies by End Year line chart |
| BO-01 | BR-06 | FR-07 | Slicers |
| BO-05 | BR-08 | FR-10 | Summary recommendation |
| BO-01 | BR-07 | FR-08, FR-09 | Summary page |

## 18. Sign-off

| Name | Role | Status |
|---|---|---|
| Saraswati Sarjerao Shinde | Business Analyst | Prepared |
