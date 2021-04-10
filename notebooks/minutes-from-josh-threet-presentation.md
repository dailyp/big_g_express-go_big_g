# Minutes From Josh Threet's Presentation

- Josh Threet: Systems Analyst at Big G Express
- Datasets: fault code data and vehicle onboard diagnostic data
  - J1939Faults.csv
  - VehicleDiagnosticOnboardData.csv
- Goal: Try and predict an upcoming full derate. These are indicated by an SPN 5246. 

- Big G:
  - Headquartered in Shelbyville
  - Founded since 1995
  - Operates general freight for transportation of goods
  - 600 Tractors, 1300+ trailers
  + IKE Transportation: Deals primarly with steel and aluminum products
  - Service map: Mostly on the East Side of the Mississippi, South of New York

- 1569 before 5246
  - You don't hit 5246 before 1569: Can be assumed to be always the case
    - If you can stop the partial derate from happening then you can stop the full derate from happening
  
- Cummins already have a failure prediction system
- OUr goal is to double-check things and cross-checking with Cummins predictions

**From Q/A**

- ecuSource, sometimes populated, sometimes not
  - You would be better focusing on ecuMake instead
  - BNDWS - Stability Control System
  - EATON - Body Control Modules
- There will be a clusters of events happening near the service facilities
  - Remove where long,lat match the service facilities
- `active` column - The events can be cleared by itself
  - It is safe to only fitler for active is true
  - But note for the difference of time when they are set or unset
  - Low severity/Low coolant - Example of automatic clearing and multiple transitions
- There will be a cost-benefit analysis when making decision on stoppig a truck because of a potential full derate
- What are the situations that could lead to these derates?
  - Could be a driver negligence: Putting the engine into a state that leads to issues
  - Could be also from basic maintenance issues that were not done properly
  - Could be bad sensors, bad wiring, exhaust system faults
  - A large portion of them would be user errors
  - But mostly, preventable stuffs: E.g. We could tell the drivers to stop at their next stop to check their engine
    - Filter recycle
    - Waiting for auxillary power unit to re-fill
- Average age of the fleet
  - Should not be more than 4-5 years old, for the most part
  - Majority of fleet: Kenwood T680 & Volvo 660 (PACCR)
  - 500s to low 700s would not have match in the other datasets
  - Vehicule Make: If we want to use this file, only fitler by the ones that have matching ID in the faults dataset
- Current Solution (Baseline):
  - Existing Model: Cummins telematics system
  - We don't have access to its implementation
- How much lead time would be good?
  - We will take what we can get, even if it's only a few minutes
  - Maybe at least 15 minutes, but ideally 1~2h
  - Maximum: That would be dependent on the amount of correlations that exist