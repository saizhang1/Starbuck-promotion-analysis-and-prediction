# Starbuck-promotion-analysis-and-prediction
Starbuck wants to know how do the 3 types of promtions work through their mobile app. Knowing better about their customers to be able to 
change their strategy.


## Dataset overview
The program used to create the data simulates how people make purchasing decisions and how those decisions are influenced by promotional
offers. Each person in the simulation has some hidden traits that influence their purchasing patterns and are associated with their 
observable traits. People produce various events, including receiving offers, opening offers, and making purchases.

As a simplification, there are no explicit products to track. Only the amounts of each transaction or offer are recorded.
There are three types of offers that can be sent: buy-one-get-one (BOGO), discount, and informational. In a BOGO offer, a user needs to 
spend a certain amount to get a reward equal to that threshold amount. In a discount, a user gains a reward equal to a fraction of the 
amount spent. In an informational offer, there is no reward, but neither is there a requisite amount that the user is expected to spend. Offers can be delivered via multiple channels.

The basic task is to use the data to identify which groups of people are most responsive to each type of offer, and how best to present 
each type of offer.

## Data Dictionary

> profile.json

Rewards program users (17000 users x 5 fields)

- gender: (categorical) M, F, O, or null
- age: (numeric) missing value encoded as 118
- id: (string/hash)
- became_member_on: (date) format YYYYMMDD
- income: (numeric)

> portfolio.json

Offers sent during 30-day test period (10 offers x 6 fields)

- reward: (numeric) money awarded for the amount spent
- channels: (list) web, email, mobile, social
- difficulty: (numeric) money required to be spent to receive reward
- duration: (numeric) time for offer to be open, in days
- offer_type: (string) bogo, discount, informational
- id: (string/hash)

> transcript.json 

**Since the transcript.json is way to big to upload in github, I just extract the first 2000 rows to show an example.**

Event log (306648 events x 4 fields)

- person: (string/hash)
- event: (string) offer received, offer viewed, transaction, offer completed
- value: (dictionary) different values depending on event type
- offer id: (string/hash) not associated with any "transaction"
- amount: (numeric) money spent in "transaction"
- reward: (numeric) money gained from "offer completed"
- time: (numeric) hours after start of test

## Key Findings

Before start to clean the data. I think is better to define our customers and divide them into different groups based on their purchasing behaviours.

Group 1: customers effected by promotion

- Behaviors 1: Offer received — offer viewed — transaction — offer completed
- Behaviors 2: Offer received — offer viewed — transaction (In case of informational offer will not have offer completed)

Group 2: customers not effected by promotions

- Behaviors 1: Offer received
- Behaviors 2: Offer received — offer viewed

Group 3: loyal customers (buy Starbucks anyway)

- Behaviors 1: transaction — offer received
- Behaviors 2: transaction — offer received — offer viewed
- Behaviors 3: offer received — transaction
- Behaviors 4: offer received — transaction — offer viewed

### Demographic and revenue

![1__hl4j0Roh3Tz3spNrZHSZw](https://user-images.githubusercontent.com/36822899/59093824-220b5f80-8915-11e9-8ad8-6ce489ef9177.png)

In general, there are more customers who are impacted by discount than other types of promotions. The informational offers are provided less to the customers.

![1_tdrfYJY1byeHsTUT4URwdQ](https://user-images.githubusercontent.com/36822899/59093982-731b5380-8915-11e9-9980-147b9ef28d65.png)

In Bogo offers, the f19421c1d4aa40978ebb69ca19b0e20d offer has the best performance, it generated the higest revenue while the cost is not vey high.

In discount offers, fafdcd668e3743c1bb461111dcafc2a4 offers definitely has the best performance, generated the highest revenue and the cost is reasonable.

In informational offer, 3f207df678b143eea3cee63160fa8bed is the best, higher revenue and lower cost.

![Capture](https://user-images.githubusercontent.com/36822899/59094035-9514d600-8915-11e9-98d9-2ae05d561b56.PNG)

Here is another small analysis about the revenue, number of users when one single user is provided by 1 type, 2 types or 3 types of offers. You can clearly see when the user is provided 2 types of promotions, it will generate more transction/revenue.

### Most predictive features of the customers

You can see from this graph, the most predictive that the feature can be effient is ‘age’, ‘income’, and ‘difficuty’ of the offer. Which can influence their decision to purchase or not, or to be impacted by the offers or not.
