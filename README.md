# architectural_kata

[Architectural Decision Records](#adrs)

[Actors and Actions](#actors)

[Components and Responsibilities](#components)

[Questions](#questions)

<a name="adrs"/>

## Architectural Decision Records (ADRs)
Please refer to the listing of files within this repo (above) for all ADRs.

<a name="actors"/>

## Actors and Actions
* Registered Customer
  * view available meals by location
  * view order history
  * identify diet/health preferences
  * identify demographic characteristics
  * provide feedback on a past meal
  * purchase meal at a kiosk or smart fridge
  * subscribe to a meal plan of delivered meals (future)
  
* Unregistered Customer
  * purchase meal at a kiosk or smart fridge
  * become a registered customer

* Merchant (Farmacy Food)
  * view feedback on a customer's past meal
  * view aggregate feedback on meals
  * view aggregate feedback on locations
  * view aggregate feedback from a customer
  * issue a customer survey
  * set prices on meals
  * set discounts on meals by menu item, by date/time
  * set discounts on meals by demographic (future)
  * provide coupons to customers by demographic
  * view meal inventory by location(s)
  * view aggregate meal transactions by location, by customer, by menu item
  * schedule and request meal prep from the kitchen
  * decide what meals to produce and where to distribute
  
* Kiosk Point-of-Sale (Toast)
  * record transacted meal
  * provide current kiosk inventory

* Smart Fridge (Byte Tech)
  * record transacted meal
  * provide current fridge inventory

* Kitchen
  * prepare meals based on merchant order
  * procure ingredients to prepare meals

* Kitchen Inventory Management (Cheftec)
  * manage meal recipes
  * manage ingredient procurement/inventory
  * track nutrition facts

* Distributor
  * pick up meals from kitchen(s) and deliver to kiosks, fridges and other venues
  
* Donor (future)
  * donate funds
  * identify beneficiaries
  * review donation impact

<a name="components"/>

## Components and Responsibilities
* location inventory tracker
  * track meal inventory at a location where meals are sold (kiosk, fridge, etc.)
* customer order tracker
  * track customer meal order history
* customer demographics
  * collect customer diet and health preferences
  * collect customer income and demographic details (low income, student)
* feedback processor
  * collect customer feedback on ordered meals
  * notify merchant, customer service, etc. of critical feedback
* survey feedback
  * push surveys to customers
  * collect customer survey responses
* meal preparation schedule
  * send meal orders to the kitchen(s)
* meal distribution
  * notify distributors of prepped meal pickup
* price setting
  * allow setting of discounted prices by menu item or location or other non-customer characteristic
  
<a name="questions"/>

## Questions
* How should feedback be handled?
  * How does handling survey feedback differ from handling meal feedback?
    * survey feedback is merchant-initiated and merchant reviews it at their own leisure (merchant pushes to customer)
    * meal feedback is client-initiated (client pushes to merchant) and may be time-sensitive and require review

* How do we handle inventory? Our solution/system is the global repository of meal inventory.
  * How does our system obtain a current snapshot of inventory?
    * Fridges and kiosks, etc. would not push inventory updates (or sales) to our system
    * Need to periodically query fridge/kiosk APIs to get inventory levels and aggregate
    
* How does a kitchen know what meals to prepare?
  * Merchant sets the menu and decides what is required in whcih locations.
  * Kitchen just needs to know how many meals and handle procurement.
  * Distribution is a separate function.

* How does a kiosk differ from a smart fridge?
  * Kiosks and smart fridges are separate modes of distribution. The term "kiosk" is not a synonym for the venue where you might find a smart fridge:  a kiosk is NOT a place where a smart fridge would be placed.

  * A kiosk refers to a place within a coffee shop or some other staffed location where customers can directly grab a Farmacy meal and then pay at a register. From the customers' point of view, they're paying for the Farmacy meal as if it were any other merchandise in the venue. From the venue staff's point of view, there may or may not be a difference, but the transaction has to be captured by Farmacy's point-of-sale system (Toast).

  * A smart fridge could be situated anywhere (e.g. an office). A customer making a purchase at a smart fridge interacts only with the fridge's tablet/electronic interface using a credit/debit card or some other token to auhenticate and pay. The fridge belongs to a third-party (Byte Tech). The completed transaction is captured in the Byte Tech network. The transaction DOES NOT require the involvement of any attendant to complete; that is what makes it a smart fridge. That said, nothing stops a smart fridge from also being placed inside a coffee shop.

* How is inventory tracked by a smart fridge and a kiosk?
  * A smart fridge can track its own inventory levels and act as its own point-of-sale. The product packaging for a meal has an RFID tag that a receiver on the fridge can detect and the act of removing an item from the fridge/closing the door completes the transaction and records the data to the Byte Tech network.

  * The kiosk point-of-sale system (Toast) tracks sales and inventory levels, which are updated when the venue staff completes the sale.
