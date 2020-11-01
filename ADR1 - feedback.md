# 1. Handling Customer Feedback

## Status
Proposed

## Context
* Customers may provide feedback about a meal that they ordered.
  * e.g. The kale in this meal was wilted.
* Customers may provide feedback about other aspects of their experience.
  * e.g. Your smart fridge at this location charged me twice for the same item.
* Customers may provide feedback as responses to a merchant-generated survey.
  * e.g. What do you think of these new menu items? What do you think about a new kiosk at this coffee shop?

Feedback can be provided at their own initiative or in response to a request. It may be about a specific order, a location, a problem with the web/app interface. These categories and characteristics can drive different response workflows. Unsolicited feedback may potentially require greater attention than solicited feedback; there may need to be triage. 

## Decision
Keep separate feedback processor components to handle customer-initiated vs merchant-solicited feedback.

Our initial thought was to have a feedback processor component that handled all sorts of user feedback. However, customer-initiated feedback requires a more event-driven approach than merchant-solicited feedback. For the former, the mechant may have to triage and respond quickly to a quality issue. For the latter, the merchant can review responses at their own leisure. The workflows governing how both are connected and analyzed are different.

## Consequences
This decision will allow for customer-intiiated feedback to have a different set of metadata/messaging contract from merchant-solicited feedback.
One can follow an event-driven workflow and the other a request-driven workflow.
