# PowerBIDAX
100 Procurement DAX Queries

Below are the DAX queries for all 100 KPIs listed. Each query is structured to match the corresponding KPI, considering columns and measures typically required in procurement data. Some queries might need to be adjusted based on the actual data model.

---

### 1. Supplier Performance Report

```DAX
SupplierPerformance =
AVERAGEX(
    Suppliers,
    Suppliers[Supplier Rating]
)
```

---

### 2. Procurement Cycle Time Analysis

```DAX
ProcurementCycleTime =
AVERAGEX(
    PurchaseOrders,
    DATEDIFF(PurchaseOrders[Requisition Date], PurchaseOrders[Receipt Date], DAY)
)
```

---

### 3. Purchase Order Status Report

```DAX
OpenOrders =
COUNTROWS(FILTER(PurchaseOrders, PurchaseOrders[Status] = "Open"))

ClosedOrders =
COUNTROWS(FILTER(PurchaseOrders, PurchaseOrders[Status] = "Closed"))
```

---

### 4. Vendor Lead Time Comparison

```DAX
VendorLeadTime =
SUMMARIZE(
    PurchaseOrders,
    Vendors[Vendor Name],
    "Average Lead Time",
    AVERAGEX(PurchaseOrders, DATEDIFF(PurchaseOrders[Order Date], PurchaseOrders[Delivery Date], DAY))
)
```

---

### 5. Contract Compliance Report

```DAX
ContractCompliance =
DIVIDE(
    SUM(Contracts[Compliant Amount]),
    SUM(Contracts[Total Amount]),
    0
)
```

---

### 6. Procurement Spend Analysis

```DAX
TotalProcurementSpend =
SUM(PurchaseOrders[Amount])
```

---

### 7. Supplier On-Time Delivery Rate

```DAX
OnTimeDeliveryRate =
DIVIDE(
    COUNTROWS(FILTER(PurchaseOrders, PurchaseOrders[Actual Delivery Date] <= PurchaseOrders[Promised Delivery Date])),
    COUNTROWS(PurchaseOrders),
    0
)
```

---

### 8. Procurement Savings Dashboard

```DAX
ProcurementSavings =
SUM(PurchaseOrders[Budgeted Amount]) - SUM(PurchaseOrders[Actual Amount])

SavingsPercentage =
DIVIDE(ProcurementSavings, SUM(PurchaseOrders[Budgeted Amount]), 0) * 100
```

---

### 9. Top 10 Vendors by Spend

```DAX
Top10Vendors =
TOPN(
    10,
    SUMMARIZE(
        PurchaseOrders,
        Vendors[Vendor Name],
        "Total Spend", SUM(PurchaseOrders[Amount])
    ),
    [Total Spend],
    DESC
)
```

---

### 10. Contract Renewal Tracker

```DAX
ContractsExpiringSoon =
FILTER(
    Contracts,
    DATEDIFF(TODAY(), Contracts[End Date], DAY) <= 30
)
```

---

### 11. Purchase Order vs. Actual Receipt Report

```DAX
POvsReceiptVariance =
SUM(PurchaseOrders[Ordered Quantity]) - SUM(PurchaseOrders[Received Quantity])
```

---

### 12. Procurement Forecast Accuracy

```DAX
ForecastAccuracy =
1 - ABS(SUM(PurchaseOrders[Forecasted Quantity]) - SUM(PurchaseOrders[Actual Quantity])) / SUM(PurchaseOrders[Forecasted Quantity])
```

---

### 13. Supplier Risk Assessment

```DAX
SupplierRiskScore =
SUMMARIZE(
    Suppliers,
    Suppliers[Supplier Name],
    "Risk Score", AVERAGE(Suppliers[Risk Factor])
)
```

---

### 14. Requisition Approval Time Report

```DAX
ApprovalTime =
AVERAGEX(
    Requisitions,
    DATEDIFF(Requisitions[Request Date], Requisitions[Approval Date], DAY)
)
```

---

### 15. Supplier Quality Dashboard

```DAX
QualityScore =
AVERAGEX(
    Suppliers,
    Suppliers[Quality Rating]
)
```

---

### 16. Procurement Budget Utilization

```DAX
BudgetUtilization =
DIVIDE(
    SUM(PurchaseOrders[Actual Spend]),
    SUM(PurchaseOrders[Budget Amount]),
    0
)
```

---

### 17. Vendor Engagement Report

```DAX
VendorEngagements =
COUNTROWS(VendorInteractions)
```

---

### 18. Procurement Spend by Category

```DAX
SpendByCategory =
SUMMARIZE(
    PurchaseOrders,
    Categories[Category Name],
    "Total Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 19. Contract Expiry Alert

```DAX
ExpiryAlerts =
FILTER(
    Contracts,
    Contracts[End Date] <= TODAY()
)
```

---

### 20. Supplier Diversity Report

```DAX
DiversitySpend =
SUMMARIZE(
    PurchaseOrders,
    Suppliers[Supplier Type],
    "Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 21. Procurement Cost Breakdown

```DAX
CostBreakdown =
SUMMARIZE(
    PurchaseOrders,
    "Material Cost", SUM(PurchaseOrders[Material Cost]),
    "Logistics Cost", SUM(PurchaseOrders[Logistics Cost]),
    "Other Costs", SUM(PurchaseOrders[Other Costs])
)
```

---

### 22. Procurement Trends by Quarter

```DAX
QuarterlyTrends =
SUMMARIZE(
    PurchaseOrders,
    Dates[Quarter],
    "Total Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 23. Supplier Fulfillment Rate

```DAX
FulfillmentRate =
DIVIDE(
    SUM(PurchaseOrders[Delivered Quantity]),
    SUM(PurchaseOrders[Ordered Quantity]),
    0
)
```

---

### 24. Procurement Request Turnaround Time

```DAX
TurnaroundTime =
AVERAGEX(
    Requests,
    DATEDIFF(Requests[Submission Date], Requests[Approval Date], DAY)
)
```

---

### 25. Material Delivery Lead Time

```DAX
MaterialLeadTime =
AVERAGEX(
    Deliveries,
    DATEDIFF(Deliveries[Planned Delivery Date], Deliveries[Actual Delivery Date], DAY)
)
```

---

### 26. Supplier Contract Performance

```DAX
ContractPerformance =
DIVIDE(
    SUM(Contracts[Delivered Value]),
    SUM(Contracts[Contract Value]),
    0
)
```

---

### 27. Purchase Order Amendment History

```DAX
AmendmentCount =
COUNTROWS(PurchaseOrderAmendments)
```

---

### 28. Late Delivery Penalty Tracker

```DAX
LatePenaltyAmount =
SUMX(
    FILTER(PurchaseOrders, PurchaseOrders[Actual Delivery Date] > PurchaseOrders[Promised Delivery Date]),
    PurchaseOrders[Penalty Amount]
)
```

---

### 29. Procurement Savings by Vendor

```DAX
SavingsByVendor =
SUMMARIZE(
    PurchaseOrders,
    Vendors[Vendor Name],
    "Savings", SUM(PurchaseOrders[Budgeted Amount]) - SUM(PurchaseOrders[Actual Amount])
)
```

---

### 30. Open Purchase Orders Report

```DAX
OpenPurchaseOrders =
COUNTROWS(FILTER(PurchaseOrders, PurchaseOrders[Status] = "Open"))
```

### 31. Supplier Invoice Processing Time

```DAX
InvoiceProcessingTime =
AVERAGEX(
    Invoices,
    DATEDIFF(Invoices[Submission Date], Invoices[Approval Date], DAY)
)
```

---

### 32. Contract Value Tracker

```DAX
TotalContractValue =
SUM(Contracts[Contract Value])
```

---

### 33. Procurement Spend by Department

```DAX
SpendByDepartment =
SUMMARIZE(
    PurchaseOrders,
    Departments[Department Name],
    "Total Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 34. Supplier Capacity Utilization

```DAX
SupplierCapacityUtilization =
DIVIDE(
    SUM(PurchaseOrders[Ordered Quantity]),
    SUM(Suppliers[Capacity]),
    0
)
```

---

### 35. Lead Time Deviation Report

```DAX
LeadTimeDeviation =
AVERAGEX(
    PurchaseOrders,
    DATEDIFF(PurchaseOrders[Promised Delivery Date], PurchaseOrders[Actual Delivery Date], DAY)
)
```

---

### 36. Procurement Efficiency Index

```DAX
ProcurementEfficiency =
DIVIDE(
    SUM(PurchaseOrders[Actual Spend]),
    SUM(PurchaseOrders[Ordered Quantity]),
    0
)
```

---

### 37. Single-Source Procurement Tracker

```DAX
SingleSourceProcurements =
COUNTROWS(FILTER(PurchaseOrders, PurchaseOrders[Procurement Type] = "Single-Source"))
```

---

### 38. Purchase Order Amendment History

```DAX
AmendmentHistory =
COUNTROWS(PurchaseOrderAmendments)
```

---

### 39. Rejected Purchase Orders Report

```DAX
RejectedOrders =
COUNTROWS(FILTER(PurchaseOrders, PurchaseOrders[Status] = "Rejected"))
```

---

### 40. Procurement Source of Supply

```DAX
SourceOfSupply =
SUMMARIZE(
    PurchaseOrders,
    Suppliers[Source Type],
    "Total Orders", COUNTROWS(PurchaseOrders)
)
```

---

### 41. Supplier Compliance Scorecard

```DAX
ComplianceScore =
DIVIDE(
    SUM(Suppliers[Compliant Orders]),
    COUNTROWS(Suppliers),
    0
)
```

---

### 42. Emergency Procurement Requests

```DAX
EmergencyRequests =
COUNTROWS(FILTER(PurchaseOrders, PurchaseOrders[Procurement Type] = "Emergency"))
```

---

### 43. Supplier Performance Improvement

```DAX
PerformanceImprovement =
SUMMARIZE(
    Suppliers,
    Suppliers[Supplier Name],
    "Performance Change", LASTNONBLANK(Suppliers[Current Performance], 1) - FIRSTNONBLANK(Suppliers[Previous Performance], 1)
)
```

---

### 44. Procurement Contract Status Dashboard

```DAX
ActiveContracts =
COUNTROWS(FILTER(Contracts, Contracts[Status] = "Active"))

ExpiredContracts =
COUNTROWS(FILTER(Contracts, Contracts[Status] = "Expired"))
```

---

### 45. Outsource vs. In-house Procurement Analysis

```DAX
OutsourceSpend =
SUMX(FILTER(PurchaseOrders, PurchaseOrders[Procurement Type] = "Outsource"), PurchaseOrders[Amount])

InHouseSpend =
SUMX(FILTER(PurchaseOrders, PurchaseOrders[Procurement Type] = "In-house"), PurchaseOrders[Amount])
```

---

### 46. Supplier Price Comparison Report

```DAX
PriceComparison =
SUMMARIZE(
    PurchaseOrders,
    Suppliers[Supplier Name],
    "Average Price", AVERAGE(PurchaseOrders[Unit Price])
)
```

---

### 47. Purchase Price Variance (PPV) Report

```DAX
PPV =
SUMX(
    PurchaseOrders,
    PurchaseOrders[Budgeted Unit Price] - PurchaseOrders[Actual Unit Price]
)
```

---

### 48. Top 5 Procurement Categories by Spend

```DAX
TopCategories =
TOPN(
    5,
    SUMMARIZE(
        PurchaseOrders,
        Categories[Category Name],
        "Total Spend", SUM(PurchaseOrders[Amount])
    ),
    [Total Spend],
    DESC
)
```

---

### 49. Procurement Spend by Supplier Country

```DAX
SpendByCountry =
SUMMARIZE(
    PurchaseOrders,
    Suppliers[Country],
    "Total Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 50. Inventory Turnover Analysis

```DAX
InventoryTurnover =
DIVIDE(
    SUM(Inventory[Cost of Goods Sold]),
    AVERAGE(Inventory[Average Inventory Value]),
    0
)
```

---

### 51. Supplier Contract Breach Report

```DAX
ContractBreaches =
COUNTROWS(FILTER(Contracts, Contracts[Status] = "Breached"))
```

---

### 52. Procurement Invoice Approval Rate

```DAX
ApprovalRate =
DIVIDE(
    COUNTROWS(FILTER(Invoices, Invoices[Approval Status] = "Approved")),
    COUNTROWS(Invoices),
    0
)
```

---

### 53. Purchase Order Lead Time by Vendor

```DAX
LeadTimeByVendor =
SUMMARIZE(
    PurchaseOrders,
    Vendors[Vendor Name],
    "Average Lead Time", AVERAGEX(PurchaseOrders, DATEDIFF(PurchaseOrders[Order Date], PurchaseOrders[Delivery Date], DAY))
)
```

---

### 54. Procurement Spend by Payment Terms

```DAX
SpendByPaymentTerms =
SUMMARIZE(
    PurchaseOrders,
    PurchaseOrders[Payment Terms],
    "Total Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 55. Supplier Contract Performance

```DAX
ContractPerformanceBySupplier =
SUMMARIZE(
    Contracts,
    Suppliers[Supplier Name],
    "Performance", DIVIDE(SUM(Contracts[Delivered Value]), SUM(Contracts[Contract Value]), 0)
)
```

---

### 56. Monthly Procurement Budget Report

```DAX
MonthlyBudgetReport =
SUMMARIZE(
    PurchaseOrders,
    Dates[Month],
    "Budget Utilized", SUM(PurchaseOrders[Actual Spend])
)
```

---

### 57. Purchase Order Fulfillment Report

```DAX
FulfilledOrders =
COUNTROWS(FILTER(PurchaseOrders, PurchaseOrders[Delivery Status] = "Fulfilled"))
```

---

### 58. Open Purchase Orders Report

```DAX
OpenPurchaseOrdersDetailed =
FILTER(
    PurchaseOrders,
    PurchaseOrders[Status] = "Open"
)
```

---

### 59. Procurement Audit Dashboard

```DAX
AuditFindings =
COUNTROWS(FILTER(AuditLogs, AuditLogs[Finding Type] <> "Compliant"))
```

---

### 60. Vendor Payment Terms Analysis

```DAX
PaymentTermsAnalysis =
SUMMARIZE(
    Vendors,
    Vendors[Payment Terms],
    "Average Payment Time", AVERAGE(Vendors[Payment Time])
)
```

---

### 61. Purchase vs. Rental Decision Dashboard

```DAX
SpendComparison =
SUMMARIZE(
    PurchaseOrders,
    PurchaseOrders[Procurement Type],
    "Total Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 62. Procurement Spend Trend Analysis

```DAX
SpendTrend =
SUMMARIZE(
    PurchaseOrders,
    Dates[YearMonth],
    "Total Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 63. Supplier Disqualification Report

```DAX
DisqualifiedSuppliers =
COUNTROWS(FILTER(Suppliers, Suppliers[Status] = "Disqualified"))
```

---

### 64. Late Delivery Penalty Tracker

```DAX
LatePenalties =
SUM(PurchaseOrders[Penalty Amount])
```

---

### 65. Procurement Contract Negotiation Tracker

```DAX
NegotiationStatus =
SUMMARIZE(
    Contracts,
    Contracts[Negotiation Stage],
    "Total Contracts", COUNTROWS(Contracts)
)
```

---

### 66. Top 10 Expiring Contracts

```DAX
ExpiringContracts =
TOPN(
    10,
    FILTER(Contracts, Contracts[End Date] >= TODAY()),
    Contracts[End Date],
    ASC
)
```

---

### 67. Supplier Onboarding Efficiency

```DAX
OnboardingTime =
AVERAGEX(
    Suppliers,
    DATEDIFF(Suppliers[Onboarding Start Date], Suppliers[Approval Date], DAY)
)
```

---

### 68. Request for Quotation (RFQ) Status

```DAX
RFQStatus =
SUMMARIZE(
    RFQs,
    RFQs[Status],
    "Total RFQs", COUNTROWS(RFQs)
)
```

---

### 69. Vendor Spend Concentration

```DAX
VendorConcentration =
SUMMARIZE(
    PurchaseOrders,
    Vendors[Vendor Name],
    "Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 70. Procurement Contract Escalation

```DAX
ContractEscalations =
COUNTROWS(FILTER(Contracts, Contracts[Escalation Count] > 0))
```

---

### 71. Supplier Order Processing Time

```DAX
OrderProcessingTime =
AVERAGEX(
    PurchaseOrders,
    DATEDIFF(PurchaseOrders[Order Date], PurchaseOrders[Approval Date], DAY)
)
```

---

### 72. Contract Compliance by Vendor

```DAX
ComplianceByVendor =
SUMMARIZE(
    Contracts,
    Vendors[Vendor Name],
    "Compliance", DIVIDE(SUM(Contracts[Compliant Amount]), SUM(Contracts[Total Amount]), 0)
)
```

---

### 73. Procurement Exception Handling

```DAX
ExceptionsHandled =
COUNTROWS(FILTER(Exceptions, Exceptions[Status] = "Resolved"))
```

---

### 74. Supplier Pre-Qualification Analysis

```DAX
PreQualificationAnalysis =
SUMMARIZE(
    Suppliers,
    Suppliers[Qualification Stage],
    "Total Suppliers", COUNTROWS(Suppliers)
)
```

---

### 75. Procurement Workforce Performance

```DAX
EmployeePerformance =
AVERAGEX(
    Workforce,
    Workforce[Performance Score]
)
```

---

### 76. Procurement Spend vs. Budget Forecast

```DAX
SpendVsBudget =
SUMMARIZE(
    PurchaseOrders,
    Dates[Month],
    "Forecasted Budget", SUM(PurchaseOrders[Budget Amount]),
    "Actual Spend", SUM(PurchaseOrders[Actual Spend])
)
```

---

### 77. Supplier Late Delivery Rate

```DAX
LateDeliveryRate =
DIVIDE(
    COUNTROWS(FILTER(PurchaseOrders, PurchaseOrders[Delivery Status] = "Late")),
    COUNTROWS(PurchaseOrders),
    0
)
```

---

### 78. Purchase Order Cost per Unit

```DAX
CostPerUnit =
DIVIDE(
    SUM(PurchaseOrders[Actual Spend]),
    SUM(PurchaseOrders[Ordered Quantity]),
    0
)
```

---

### 79. Procurement Request Turnaround Time

```DAX
RequestTurnaround =
AVERAGEX(
    Requests,
    DATEDIFF(Requests[Submission Date], Requests[Approval Date], DAY)
)
```

---

### 80. Rejected Invoices Tracker

```DAX
RejectedInvoices =
COUNTROWS(FILTER(Invoices, Invoices[Status] = "Rejected"))
```

---

### 81. Supplier Warranty Compliance

```DAX
WarrantyCompliance =
DIVIDE(
    SUM(Suppliers[Compliant Warranties]),
    COUNTROWS(Suppliers),
    0
)
```

---

### 82. Spend per Vendor Over Time

```DAX
VendorSpendOverTime =
SUMMARIZE(
    PurchaseOrders,
    Dates[YearMonth],
    Vendors[Vendor Name],
    "Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 83. Material Delivery Lead Time Report

```DAX
MaterialDeliveryLeadTime =
AVERAGEX(
    Deliveries,
    DATEDIFF(Deliveries[Scheduled Date], Deliveries[Actual Delivery Date], DAY)
)
```

---

### 84. Supplier Invoice Reconciliation

```DAX
ReconciledInvoices =
COUNTROWS(FILTER(Invoices, Invoices[Reconciliation Status] = "Reconciled"))
```

---

### 85. Procurement Cost Avoidance Report

```DAX
CostAvoidance =
SUMX(
    PurchaseOrders,
    PurchaseOrders[Budgeted Amount] - PurchaseOrders[Actual Amount]
)
```

---

### 86. Vendor Financial Stability Analysis

```DAX
VendorStability =
AVERAGEX(
    Vendors,
    Vendors[Financial Stability Score]
)
```

---

### 87. Supply Chain Disruption Report

```DAX
DisruptionsLogged =
COUNTROWS(FILTER(SupplyChainLogs, SupplyChainLogs[Status] = "Disrupted"))
```

---

### 88. Procurement Spend by Material Type

```DAX
SpendByMaterialType =
SUMMARIZE(
    PurchaseOrders,
    Materials[Material Type],
    "Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 89. Vendor Grievance Report

```DAX
GrievancesFiled =
COUNTROWS(FILTER(Grievances, Grievances[Status] = "Filed"))
```

---

### 90. Procurement Spend under Contract

```DAX
ContractSpend =
SUMX(FILTER(PurchaseOrders, PurchaseOrders[Under Contract] = TRUE()), PurchaseOrders[Amount])
```

---

### 91. Procurement Trends by Quarter

```DAX
QuarterlyTrendsDetailed =
SUMMARIZE(
    PurchaseOrders,
    Dates[Quarter],
    "Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 92. Procurement Cost Escalation Tracker

```DAX
CostEscalation =
SUMX(
    PurchaseOrders,
    PurchaseOrders[Escalated Cost] - PurchaseOrders[Original Cost]
)
```

---

### 93. Purchase Order Delivery Rate by Region

```DAX
DeliveryRateByRegion =
SUMMARIZE(
    PurchaseOrders,
    Regions[Region Name],
    "Delivery Rate", DIVIDE(COUNTROWS(FILTER(PurchaseOrders, PurchaseOrders[Delivery Status] = "On-Time")), COUNTROWS(PurchaseOrders), 0)
)
```

---

### 94. Supplier Payment Disputes Report

```DAX
PaymentDisputes =
COUNTROWS(FILTER(Disputes, Disputes[Status] = "Open"))
```

---

### 95. Procurement Legal Compliance Dashboard

```DAX
LegalCompliance =
DIVIDE(
    SUM(Legal[Compliant Cases]),
    COUNTROWS(Legal),
    0
)
```

---

### 96. Purchase Order Cancellation Rate

```DAX
CancellationRate =
DIVIDE(
    COUNTROWS(FILTER(PurchaseOrders, PurchaseOrders[Status] = "Cancelled")),
    COUNTROWS(PurchaseOrders),
    0
)
```

---

### 97. Sustainable Procurement Practices Report

```DAX
SustainableSpend =
SUMX(
    PurchaseOrders,
    IF(PurchaseOrders[Sustainability Flag] = TRUE(), PurchaseOrders[Amount], 0)
)
```

---

### 98. Top 5 Procurement Vendors per Category

```DAX
TopVendorsByCategory =
SUMMARIZE(
    TOPN(
        5,
        PurchaseOrders,
        Categories[Category Name],
        Vendors[Vendor Name],
        SUM(PurchaseOrders[Amount])
    ),
    Categories[Category Name],
    Vendors[Vendor Name],
    "Total Spend", SUM(PurchaseOrders[Amount])
)
```

---

### 99. Procurement Contract Error Rate

```DAX
ContractErrorRate =
DIVIDE(
    COUNTROWS(FILTER(Contracts, Contracts[Error Flag] = TRUE())),
    COUNTROWS(Contracts),
    0
)
```

---

### 100. Procurement Automation Effectiveness Report

```DAX
AutomationEffectiveness =
DIVIDE(
    COUNTROWS(FILTER(ProcessLogs, ProcessLogs[Automation Status] = "Successful")),
    COUNTROWS(ProcessLogs),
    0
)
```


