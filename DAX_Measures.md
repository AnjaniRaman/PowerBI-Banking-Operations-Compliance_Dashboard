## Total Customers
Total Customer = DISTINCTCOUNT(Customer_Master[Customer_ID])

## Completed KYC Customers
Completed KYC Customers = 
CALCULATE(
      DISTINCTCOUNT(KYC_Compliance[Customer_ID]),
      KYC_Compliance[KYC_Status]="Completed"
)

## Pending KYC Customer
Pending KYC Customer = 
CALCULATE(
      DISTINCTCOUNT(KYC_Compliance[Customer_ID]),
      KYC_Compliance[KYC_Status]="Pending"
)

## Open Service Requests
Open Service Request = 
CALCULATE(
     COUNT(Service_Requests[Customer_ID]),
     Service_Requests[Status]="OPEN"
)

## Average TAT (Days)
Average TAT =
CALCULATE(
    AVERAGE(Service_Requests[TAT Days]),
    Service_Requests[Status]="Closed"
)
