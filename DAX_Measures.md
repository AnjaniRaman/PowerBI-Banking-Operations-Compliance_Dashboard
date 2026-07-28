## Total Customers
Total Customer = DISTINCTCOUNT(Customer_Master[Customer_ID])

## Completed KYC Customers
Completed KYC Customers = CALCULATE(DISTINCTCOUNT(KYC_Compliance[Customer_ID]),KYC_Compliance[KYC_Status]="Completed")
