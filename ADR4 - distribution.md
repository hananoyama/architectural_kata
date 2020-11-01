# 1. Handling Meal Distribution

## Status
Proposed

## Context
The merchant is responsible for deciding how many meals the kitchen(s) need to produce and for which locations based on past sales data. Perhaps as more data accumulates, a new component incorporating machine learning could be introduced that can suggest meal quantities, locations and delivery schedules.

Deliveries to the fridges and kiosks (and anywhere else) also have to be coordinated with the distributor.

## Decision
To allow the merchant to coordinate meal production and distribution, we are introducing a meal preparation scheduling component where the merchant will specify the distribution inventory and schedule. This component will communicate with the meal distribution component. The former is responsible for tracking whether meal prep requests have been fulfilled. It will communicate fulfillment to the distribution component, which will notify distributors once meals are ready to be picked up.

## Consequences
* A UI for the merchant is needed to monitor meal quantities at locations and to schedule and monitor the deliveries.
* A notification mechanism is needed to alert the distributors of a scheduled delivery. Meal fulfillment should be event-driven where possible, i.e. once the kitchen has prepared the meals, it should send notification to meal preparation scheduling. If that push is not possible, then meal preparation scheduling needs to synchronously check for meal readiness at the date and time specified in the original request.
* A UI for the distributors is needed to confirm and resolve delivery status and allow the system to update inventory.
* To aid a merchant in the decision making, the merchant will be able to poll the kiosks, smart fridges and other locations for current meal quantities via the location inventory tracker.
