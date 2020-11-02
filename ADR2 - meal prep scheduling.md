# 2. Scheduling Meal Prep

## Status
Proposed

## Context
* The central kitchen uses Cheftec software to manage ingredient inventory and procurement and meal recipe-to-ingredient mapping.
  * description at https://www.cheftec.com/cheftec-basic

Our initial thought was that the kitchen was synonymous with the Cheftec software API and could communicate directly with our inventory tracking component, but further discussion indicated that our solution may actually have very minimal interaction with the Cheftec software. The merchant ultimately has to decide how many meals are needed, at which locations, and according to what schedule. The ktichen only needs to know how many meals to produce given a recipe, date and time.

## Decision
Maintain a meal prep scheduling component to manage communication between the kitchen(s) and the merchant. This component may potentially have to deal with multiple kitchens or food vendors.

The main communication between the meal prep scheduling component and kitchen(s) is 
* request-driven when the merchant sends an order to the kitchen for some quantity of meals (designated by some sort of meal recipe ID) to be ready for distribution by some date/time
* event-driven when the kitchen has fulfilled the order, it will update the meal prep scheduler with the completion status. The meal prep scheduler will need to collaborate with the meal distributor component to notify distributors to pick up meals from the kitchen for distribution.

## Consequences
This decision will require a separate UI for kitchen staff to interface with our system if the Cheftec software does not offer an API for communicating incoming orders and is designed for only for interfacing with kitchen staff/human operators. Kitchen staff will need to monitor our UI for orders and translate that into Cheftec.

As the meal prep scheduling component also tracks fulfillment, it may also have to communicate that fulfillment to the accounting system (Quickbooks) to support reconciliation with invoices from the kitchen for completed orders. That communication may not be automated, depending on the Quickbooks API.

A decision to build a UI and API for this component allows for the possibility of integrating with other kitchen inventory software.
