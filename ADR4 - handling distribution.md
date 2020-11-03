# 4. Handling Meal Distribution

## Status
Proposed

## Context
The merchant is responsible for coordinating meal production and distribution, deciding how many meals the kitchen(s) need to produce and for which locations based on anticipated sales. This is a very complex task based on the number of parties that are involved.
* They need to give the kitchens sufficient notice so the latter can better manage ingredient procurement and on-board more kitchens if necessary.
* The merchant's decisionmaking is a function not only of current inventory across all sales locations, but also historic customer demand and taste. 
* As our ssytem collect more data about meal sales, a component incorporating machine learning could be introduced to suggest optimal meal quantities, locations and delivery schedules to aid the merchant in their task.
* Deliveries to the fridges and kiosks (and anywhere else) also have to be coordinated with the distributor.

## Decision
To allow the merchant to coordinate meal production and distribution, we propose a microkernel-based meal preparation scheduling component. This component will complement the meal distribution component.
The meal prep scheduling component interfaces with the kitchen staff and any kitchen systems that handle meal prep requests. This component is responsible for tracking whether meal prep requests have been fulfilled and making that data available to accounting. It will also have to communicate fulfillment to the distribution component, which will notify distributors as meals become ready for pick up and restocking.

## Consequences
* A UI for the merchant is needed to monitor meal quantities at locations and to schedule and monitor deliveries.
* A notification mechanism is needed to alert the distributors of a scheduled delivery. Meal fulfillment should be event-driven where possible, i.e. once the kitchen has prepared the meals, it should send notification to meal preparation scheduling. If that push model is not possible, then meal preparation scheduling needs to synchronously check for meal readiness at the date and time specified in the original meal prep request sent to the ktichen.
* A UI for the distributors is needed to confirm and resolve delivery status and allow the system to update inventory.
* To aid a merchant in their decision making, the merchant will be able to poll the kiosks, smart fridges and other locations for current meal quantities via the location inventory tracker.
* We want a microkernel approach because we can think of meal ordering and fulfillment as the core, and responsibilities such as distribution, inventory update as plug-ins to this system. 
* If we ever employ ML to predict orders, that would be implemented as a plug-in that would substitute for the inputs originally provided by the merchant via a UI.
* When it comes to tracking meal distribution, availability and reliability are forefront concerns. A failure in either the scheduling or distribution component could be operationally damaging.
