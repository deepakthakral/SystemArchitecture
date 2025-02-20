# Diagram Examples

## Flowcharts

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

## C4 Model Example

```plantuml
@startuml
!define RECTANGLE class

RECTANGLE customer {
  :Personal Banking Customer;
  :A customer of the bank, with personal bank accounts.;
}

group "Bank plc" {
    RECTANGLE supportStaff {
      :Customer Service Staff;
      :Customer service staff within the bank.;
    }
    RECTANGLE backoffice {
      :Back Office Staff;
      :Administration and support staff within the bank.;
    }
    RECTANGLE mainframe {
      :Mainframe Banking System;
      :Stores all of the core banking information about customers, accounts, transactions, etc.;
    }
    RECTANGLE email {
      :E-mail System;
      :The internal Microsoft Exchange e-mail system.;
    }
    RECTANGLE atm {
      :ATM;
      :Allows customers to withdraw cash.;
    }
    RECTANGLE internetBankingSystem {
      :Internet Banking System;
      :Allows customers to view information about their bank accounts, and make payments.;
    }
}

customer --> internetBankingSystem : Views account balances, and makes payments using
internetBankingSystem --> mainframe : Gets account information from, and makes payments using
internetBankingSystem --> email : Sends e-mail using
email --> customer : Sends e-mails to
customer --> supportStaff : Asks questions to (Telephone)
supportStaff --> mainframe : Uses
customer --> atm : Withdraws cash using
atm --> mainframe : Uses
backoffice --> mainframe : Uses
@enduml
```

## C4 Model Example-2
```plantuml
@startuml

Class Student
Class FlashCards
Class Questions
Class Answers

Student"1" -- "+"FlashCards : Interacts with >
FlashCards"1" o-- "1"Questions : has >
FlashCards"1" o-- "1"Answers : has >
Answers"1" *-- "1"Wrong : has >
Answers"1" *-- "1"Right : has >

@enduml
```