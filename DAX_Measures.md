## Total Customers
- Total Customer = DISTINCTCOUNT(Customer_Master[Customer_ID])
#### Counts the total number of unique customers in the dataset.

## Completed KYC Customers

- Completed KYC Customers = 
CALCULATE(
      DISTINCTCOUNT(KYC_Compliance[Customer_ID]),
      KYC_Compliance[KYC_Status]="Completed"
)
#### Counts customers whose KYC verification has been completed.

## Pending KYC Customer

- Pending KYC Customer = 
CALCULATE(
      DISTINCTCOUNT(KYC_Compliance[Customer_ID]),
      KYC_Compliance[KYC_Status]="Pending"
)
#### Counts customers whose KYC verification is still pending.

## KYC Completion %
- %KYC Completed =
DIVIDE(
    [Completed KYC],
    [Total Customer],
    0
)
#### Calculates the percentage of customers who have completed the KYC process.

## Open Service Requests
- Open Service Request = 
CALCULATE(
     COUNT(Service_Requests[Customer_ID]),
     Service_Requests[Status]="OPEN"
)
#### Counts all service requests that are currently open.

## Closed Service Request
- Closed Service Request =
CALCULATE(
    COUNT(Service_Requests[Request_ID]),
    Service_Requests[Status] = "Closed"
)
#### Counts all service requests that have been successfully closed.

## Average TAT (Days)
- Average TAT =
CALCULATE(
    AVERAGE(Service_Requests[TAT Days]),
    Service_Requests[Status]="Closed"
)
#### Calculates the average turnaround time for closed service requests.

## SLA Breach Count
- SLA Breach Count =
CALCULATE(
    COUNTROWS(Service_Requests),
    Service_Requests[SLA Breach] = "Yes"
)
#### Counts the number of service requests that exceeded the defined SLA.

## SLA Breach %
- SLA Breach % =
DIVIDE(
    [SLA Breach Count],
    COUNTROWS(Service_Requests),
    0
)
#### Calculates the percentage of service requests that breached the SLA.

## Escalation %
- Escalation % =
DIVIDE(
    CALCULATE(
        COUNTROWS(Service_Requests),
        Service_Requests[Escalated] = "Yes"
    ),
    COUNTROWS(Service_Requests),
    0
)
#### Calculates the percentage of service requests that were escalated.
