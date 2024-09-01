**X<sub>i</sub>**

# TDGVRP Scenario Overview

## Problem Description

The **Time-Dependent Generalized Vehicle Routing Problem (TDGVRP)** is a complex logistical challenge that involves optimizing routes for delivery vehicles. In this scenario, we have one distribution center **W<sub>0</sub>** and multiple front warehouses **W<sub>i</sub>** (for **i = 1, 2, ..., m**).  The vehicles used for deliveries are homogeneous cold chain vehicles that operate on diesel fuel, which is essential for maintaining the freshness of perishable goods. Additionally, the refrigeration units that are integral to these vehicles also rely on diesel power.This problem is characterized as **stochastic** due to the variable nature of demand, which can fluctuate over time. The multi-objective aspect of the problem necessitates careful consideration of various factors, including delivery times, vehicle capacity, and operational costs.

<p align="center">
  <img src="https://github.com/user-attachments/assets/06001b1e-94d2-43b3-953f-1ae63bbdd66a" alt="image" width="60%">
</p>

## Key Assumptions


1. **Demand and Capacity**: The total demand for each route does not exceed the load capacity of the vehicle. This ensures that the vehicle can accommodate all deliveries without exceeding its limits.

2. **Warehouse Service**: Each front warehouse is served by a single vehicle, which simplifies the routing process and ensures efficient service to each location.

3. **Refrigeration Power Usage**: The refrigeration unit operates at its rated power during the unloading process. This is crucial for maintaining the quality of the products being delivered.

4. **Vehicle Speed Assumptions**: Acceleration and deceleration times are not considered when changing vehicle speeds. This assumption helps streamline the calculations involved in route optimization.




This comprehensive overview sets the foundation for understanding the complexities involved in the TDGVRP and lays the groundwork for developing effective strategies to optimize vehicle routing in real-world scenarios.




