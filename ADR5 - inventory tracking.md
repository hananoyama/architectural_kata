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
* The merchant and other administrators can only ever see total inventory across ALL locations as of a certain time based on when our system last conducted a global update for inventory. This may not scale too well if we expand to many locations, but who within Farmacy Foods requires a real-time snapshot of global inventory? We might require global inventory as of a certain time for reporting purposes, and that can always be derived after the fact. The merchant may devolve into regional sales managers or admins who are responsible for maintaining inventory for a set of locations.
