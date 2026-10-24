# Data Dictionary

Source file: `data/Policy_Data.xlsx` · 5 sheets · 5,000 rows each · MySQL database: `policy_analytics`

## Tables and columns

### Customer Information
| Column | Type | Description |
|---|---|---|
| Customer ID | Text | Unique customer key (PK) |
| Name | Text | Customer name |
| Gender | Text | Male / Female / Other (flagged as unreliable) |
| Age | Integer | Customer age (grouped into 18-29, 30-44, 45-59, 60-75, 76+) |
| Occupation | Text | Customer occupation |
| Marital Status | Text | Marital status |
| Address (City, State, Zip Code) | Text | Customer address |

### Policy Details
| Column | Type | Description |
|---|---|---|
| Policy ID | Text | Unique policy key (PK) |
| Policy Type | Text | Health, Property, Life, Auto |
| Coverage Amount | Integer | Sum insured |
| Premium Amount | Decimal | Premium charged |
| Policy Start Date | Date | Start date (start year used for premium growth) |
| Policy End Date | Date | End date (end year used for renewal wave) |
| Payment Frequency | Text | e.g. Monthly |
| Status | Text | Active (1,682), Terminated (1,678), Lapsed (1,640) |
| Customer ID | Text | FK to Customer Information |

### Claims
| Column | Type | Description |
|---|---|---|
| Claim ID | Text | Unique claim key (PK) |
| Date of Claim | Date | Claim date |
| Claim Amount | Integer | Claimed amount |
| Claim Status | Text | e.g. Approved, Pending |
| Reason for Claim | Text | Free-text reason |
| Settlement Date | Date | Settlement date |
| Policy ID | Text | FK to Policy Details |

### Payment History
| Column | Type | Description |
|---|---|---|
| Payment ID | Text | Unique payment key (PK) |
| Date of Payment | Date | Payment date |
| Amount Paid | Decimal | Amount paid |
| Payment Method | Text | e.g. Cash, Bank Transfer (slicer) |
| Payment Status | Text | e.g. Successful (slicer) |
| Policy ID | Text | FK to Policy Details |

### Additional Fields
| Column | Type | Description |
|---|---|---|
| Agent ID | Text | Selling agent |
| Renewal Status | Text | e.g. Not Renewed, Pending |
| Policy Discounts | Integer | Discount applied |
| Risk Score | Integer | Risk score |
| Policy ID | Text | FK to Policy Details |

## Relationships

```
Customer Information (Customer ID) 1 ──► * Policy Details (Customer ID)
Policy Details (Policy ID)         1 ──► * Claims (Policy ID)
Policy Details (Policy ID)         1 ──► * Payment History (Policy ID)
Policy Details (Policy ID)         1 ──► * Additional Fields (Policy ID)
```

## Data quality notes
- Data appears synthetic; treat results as patterns to investigate.
- Gender values look unreliable.
- 2014 is a partial start year (11 policies).
- 1,852 customers have no policy in Policy Details.
