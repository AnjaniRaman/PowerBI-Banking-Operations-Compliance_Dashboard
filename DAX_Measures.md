## Total Customers
### Counts the total number of unique customers in the dataset.
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

## Closed Service Request
Closed Service Request =
CALCULATE(
    COUNT(Service_Requests[Request_ID]),
    Service_Requests[Status] = "Closed"
)

## Average TAT (Days)
Average TAT =
CALCULATE(
    AVERAGE(Service_Requests[TAT Days]),
    Service_Requests[Status]="Closed"
)

## SLA Breach Count
SLA Breach Count =
CALCULATE(
    COUNTROWS(Service_Requests),
    Service_Requests[SLA Breach] = "Yes"
)

## SLA Breach %
SLA Breach % =
DIVIDE(
    [SLA Breach Count],
    COUNTROWS(Service_Requests),
    0
)

## Escalation %
Escalation % =
DIVIDE(
    CALCULATE(
        COUNTROWS(Service_Requests),
        Service_Requests[Escalated] = "Yes"
    ),
    COUNTROWS(Service_Requests),
    0
)
