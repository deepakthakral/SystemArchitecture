
This includes -

1. Logical architecture, including key components, their relationships, and the overallsystem flow

2. Different channels integration with System, communication protocols and dataformats between different system components/Channel.

3. Purpose, responsibilities, and functionality of each component.

4. Highlights the interfaces, inputs, outputs, or interactions with other components.

## Logical Architecture Flow
![Logical Architecture](/LogicalArchitecture.png)


## Application Flow

```mermaid
graph TD
    subgraph Channels
        direction TB
        C1[Mobile App]
        C2[Internet Banking]
        C3[Staff App]
        C4[Channel/POS]		
    end
	subgraph FullfillmentSystem
        direction TB
        F1[OBS]
        F2[HCC]
        F3[CUS]
        F4[TransactionBanking]		
    end
	subgraph DomainPAPILayer
        direction TB
        L1[Domain Papi1]
        L2[Domain Papi2]
        L3[Domain Papi3]
        L4[Domain PapiN]		
    end
    subgraph PaymentApplication
        direction TB
        P1[Domestic Payment]
        P2[International Payment]
        P3[Mandate Management]
        P4[Payment Limit Check]		
    end
    subgraph Gateway
        direction LR
        G1[API Gateway]
        G2[Centrized Authentication System]
		G1 <--> G2
    end	
	subgraph SAPILayer
        direction TB
        S1[SAPI1]
        S2[SAPI2]
        S3[SAPI3]
        S4[SAPIN]		
    end
	subgraph OtherSystem
        direction TB
        O1[Notification]
        O2[Fraud]
		O1<-->O2
    end
    Channels <-->|Interact with| Gateway
	Gateway <--> DomainPAPILayer
	DomainPAPILayer <--> PaymentApplication
	PaymentApplication <--> SAPILayer
	SAPILayer <-->FullfillmentSystem
    PaymentApplication <--> OtherSystem
    OtherSystem <--> PaymentApplication
```

## Sequence Diagrams

```mermaid
sequenceDiagram
  autonumber
  Server->>Terminal: Send request
  loop Health
      Terminal->>Terminal: Check for health
  end
  Note right of Terminal: System online
  Terminal-->>Server: Everything is OK
  Terminal->>Database: Request customer data
  Database-->>Terminal: Customer data
```
## Component Diagrams
![Component Diagram](/ComponentDiagram.png)
