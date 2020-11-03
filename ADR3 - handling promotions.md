# 3. Handling Promotions

## Status
Proposed

## Context
* The current distribution points may be able to identify the customer from their payment card, but have no notion of whether they are eligible for discounted pricing (based on demographic characteristics) unless they also support querying our Farmacy Foods system for that info at the point of swipe. We doubt there is support for such custom integration (i.e. where a smart fridge or kiosk POS, upon identifying the customer, asks our system whether custom meal prices need to be communicated to the customer) and even if one vendor supports it, we doubt that all vendors do (i.e. the smart fridge may support it, but not the kiosk POS just by the nature of how a transaction happens in the latter case). 

* With the smart fridge, by the time a card swipe happens, the customer will have already seen a standard set of prices that the merchant set in advance via the fridge's tablet/screen interface. Even if the fridge is smart enough to present new prices based on identifying the customer from a swipe, it's unlikely there would be a way, from a usaibility perspective, to signal to the customer that they are now eligible for special pricing. 

## Decision
* Support only coupons when customers make purchases from a kiosk or a smart fridge
  * assumes the kiosk POS software supports scanning of merchant-issued coupons (paper- or app-based)
  * assumes the smart fridge allows for coupon code entry via the fridge's screen interface prior to the customer being charged
* Support tiered pricing/discounts based on customer demographics only with sales models that support ordering in advance, e.g. the subscription model mentioned as desirable in the future.
  * If a merchant supports the idea of setting up discounted prices in smart fridges in specific venues, e.g. a college campus or senior center, this could also be achieved within the current solution, as the merchant may set prices by tracking location characteristics using our pricing component and push them to the smart fridge.

## Consequences
* None of these options require significant changes to the proposed architecture. Enhancements to the pricing component might be needed to accommodate the price discount at a location. 
* On the face of it, this may not seem like an architectural decision, but the assumed mechanics of how a customer purchases a meal at a fridge or a kiosk seem to disallow tiered pricing. This record is to indicate what we believe is possible price promotion-wise.
