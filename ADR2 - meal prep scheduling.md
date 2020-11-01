# 1. Scheduling Meal Prep

## Status
Proposed

## Context
* The central kitchen uses Cheftec software to manage ingredient inventory and procurement and meal recipe-to-ingredient mapping.
  * description at https://www.cheftec.com/cheftec-basic
  * 
Feedback can be provided at their own initiative or in response to a request. It may be about a specific order, a location, a problem with the web/app interface. These categories and characteristics can drive different response workflows. Unsolicited feedback may potentially require greater attention than solicited feedback; there may need to be triage. 

## Decision
Maintain a meal prep scheduling component to manage communication between the kitchen(s) and the merchant. This component may potential have to deal with multiple kitchens or food vendors.

Our initial thought was that the kitchen was synonymous with the Cheftec API and could communicate directly with our inventory tracking component, but further discussion indicated that our solution may actually have very minimal interaction with the Cheftec software. The merchant ultimately has to decide how many meals are needed, at which locations, and according to what schedule. 

The main communication between the meal prep scheduling component and Cheftec is 
*request-driven when the merchant sends an order to the kitchen for some quantity of meals (designated by some sort of meal recipe ID) to be ready for distribution by some date/time
*event-driven when the kitchen has fulfilled the order (assuming Cheftec can notify; if not, meal prep scheduling will check with Cheftec for order fulfillment status at the date/time). The meal prep scheduler will need to collaborate with the meal distributor component to notify distributors to pick up meals from the kitchen for distribution. 

## Consequences
This decision may require a separate UI for kitchen staff to interface with our system if the Cheftec software does not offer an API for communicating incoming orders and is designed for only for interfacing with kitchen staff/human operators. Kitchen staff will need to monitor our UI for orders and translate that into Cheftec.
