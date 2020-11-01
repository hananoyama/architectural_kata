# 1. Handling Meal Distribution

## Status
Proposed

## Context
Deliveries to re-stack the fridges and POSs have to be scheduled. It was tempting to have this scheduling driven by the inventory updates. However, by the time a fridge or a POS need to be re-stacked, it is too late to request meals to be cooked and delivered. This planning should be done in advance by the merchant.

## Decision
We are not confident we can automate this process just yet. Perhaps as more data is accumulated, a new component could be introduced that will pre-populate or suggest meal quantity and delivery schedules. As of now, the merchant will have the ultimate control over the meal prep and distribution scheduling. To achieve this, we are introducing a distribution component where the merchant will specify the distribution inventory and schedule. This component will communicate with the meal scheduler component. The latter will update the distribution scheduler once the meals are ready to be picked up.

To aid a merchant in the decision making, the system will integrate with POS and smart fridges to poll for the meal quantities at each location and to update the central repository.

## Consequences
* UI components for the merchant are needed to monitor meal quantities at locations and to schedule and monitor the deliveries. 
* A notification mechanism is needed to alert the distributors of a scheduled delivery.
* UI for the distributors is needed to confirm and resolve delivery status.
