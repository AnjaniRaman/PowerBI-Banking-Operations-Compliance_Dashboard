## Total Customers
#### Counts the total number of unique customers in the dataset.
- Total Customer = DISTINCTCOUNT(Customer_Master[Customer_ID])

## Completed KYC Customers
#### Counts customers whose KYC verification has been completed.
- Completed KYC Customers = 
CALCULATE(
      DISTINCTCOUNT(KYC_Compliance[Customer_ID]),
      KYC_Compliance[KYC_Status]="Completed"
)

## Pending KYC Customer
#### Counts customers whose KYC verification is still pending.
- Pending KYC Customer = 
CALCULATE(
      DISTINCTCOUNT(KYC_Compliance[Customer_ID]),
      KYC_Compliance[KYC_Status]="Pending"
)

## KYC Completion %
#### Calculates the percentage of customers who have completed the KYC process.
- %KYC Completed =
DIVIDE(
    [Completed KYC],
    [Total Customer],
    0
)

## Open Service Requests
#### Counts all service requests that are currently open.
- Open Service Request = 
CALCULATE(
     COUNT(Service_Requests[Customer_ID]),
     Service_Requests[Status]="OPEN"
)

## Closed Service Request
#### Counts all service requests that have been successfully closed.
- Closed Service Request =
CALCULATE(
    COUNT(Service_Requests[Request_ID]),
    Service_Requests[Status] = "Closed"
)

## Average TAT (Days)
#### Calculates the average turnaround time for closed service requests.
- Average TAT =
CALCULATE(
    AVERAGE(Service_Requests[TAT Days]),
    Service_Requests[Status]="Closed"
)

## SLA Breach Count
#### Counts the number of service requests that exceeded the defined SLA.
- SLA Breach Count =
CALCULATE(
    COUNTROWS(Service_Requests),
    Service_Requests[SLA Breach] = "Yes"
)

## SLA Breach %
#### Calculates the percentage of service requests that breached the SLA.
- SLA Breach % =
DIVIDE(
    [SLA Breach Count],
    COUNTROWS(Service_Requests),
    0
)

## Escalation %
#### Calculates the percentage of service requests that were escalated.
- Escalation % =
DIVIDE(
    CALCULATE(
        COUNTROWS(Service_Requests),
        Service_Requests[Escalated] = "Yes"
    ),
    COUNTROWS(Service_Requests),
    0
)
