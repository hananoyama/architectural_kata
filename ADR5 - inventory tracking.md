# 5. Keeping Updated Inventory

## Status
Proposed

## Context
* A smart fridge tracks its inventory based on RFID tags on product packaging.
* A kiosk tracks its inventory based on sales via the POS software.
* The fridge and POS vendors presumably have APIs that expose inventory by location. But we assume that these vendors don't expose a message broker that will allow our Farmacy Food system to receive inventory updates upon the conclusion of each sale. Instead, we will have to query them periodically to get inventory updates by location. Furthermore, it's possible that other venues where me might sell meals or a future POS system only supports querying for inventory and so we treat synchronous updates as the lowest common denominator.

## Decision
Request inventory information synchronously from each vendor API (i.e. Byte Tech, Toast) across every location on a periodic basis.

## Consequences
* The merchant and other administrators can only ever see total inventory across ALL locations as of a certain time based on when our system last conducted a global update for inventory. This may not scale well as we expand to thousands of locations, but who within Farmacy Foods requires a real-time snapshot of global inventory? 
* We might require global inventory for reporting purposes, but that can always be derived after the fact for a given point in time from third-party business intelligence systems (e.g. an OLAP cube).
* As the operation grows, the merchant's role may expand beyond a single individual, e.g. to regional sales managers or admins, who would be responsible for overseeing inventory for a set of locations. If they need a real-time snapshot of inventory, they could initiate a query for current inventory across all fridges and kiosks within their coverage area.
* When a distributor restocks the meals at a location, it should be possible to send a location inventory update via some interface to the distribution component. However, this would be optional so long as we have a mechanism in place to periodically refresh the inventory snapshot.
