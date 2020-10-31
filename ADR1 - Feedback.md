# 1. Separate Workflow Components for Customer-Initiated vs Merchant-Initiated/Requested Feedback

## Status
Under Discussion

## Context
What types of feedback are possible? Customers can provide feedback on meals/food items that they ordered. 

The merchant/Farmacy Food admins can solicit feedback also on a specific menu item.

## Decision
Separate components/processors for each type of feedback.

## Consequences
This decision will require feedback events to be sent to multiple queues.
