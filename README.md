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



## speed_hour(time)

Throughout the delivery process, vehicles may encounter various traffic conditions. Each condition lasts for a defined period, during which the vehicle maintains a constant speed. Importantly, this speed is inversely proportional to the traffic congestion index.

Given that traffic rates vary at different times of the day, we created a DataFrame called `speed_hour` to analyze the varying speeds of vehicles throughout these hours. 

In this context, time plays a crucial role in influencing costs, making it essential to monitor it closely. One key factor affecting time is speed; therefore, we must analyze speed variations at different times to understand their impact on overall traffic efficiency and related expenses. 

By integrating these insights, we can make informed decisions to optimize traffic flow and effectively reduce costs.

![image](https://github.com/user-attachments/assets/ebe6bff5-6945-4b4f-a319-15c8893357a5)


## Mpg(weight)

Since fuel consumption increases with the weight of trucks, we utilized existing data to develop an optimal regression model for predicting truck fuel consumption based on their weight. By performing regression analysis on the available data, we aimed to determine the most efficient objective function value, specifically focusing on maximizing the adjusted \( R^2 \) statistic. 

This approach helps us refine our model, ensuring it accurately captures the relationship between weight and fuel consumption, leading to better predictions and more effective decision-making in fleet management.

The general form of the regression equation is:


<p align="center">
  <strong>mpg(weight) = β<sub>0</sub> + β<sub>1</sub>(weight)<sup>-f</sup></strong>
</p>

The best equation obtained is as follows:


<p align="center">
  <strong> mpg(weight) = 7.3515 + 71.6108(weight)<sup>-1.5</sup> </strong>
</p>



This equation provides a predictive model for fuel consumption, allowing for more informed operational strategies.


## Diagnostic

To evaluate the reliability of our model, we utilize diagnostic plots. These plots help us visually assess key aspects such as residuals, normality, and homoscedasticity. The absence of any issues in these diagnostic plots indicates that our model meets the necessary assumptions and performs effectively.
This reinforces the validity of our results and suggests that the model can be trusted for making predictions or drawing conclusions. By ensuring that these diagnostic criteria are satisfied, we can confidently move forward with our analysis and recommendations.

![image](https://github.com/user-attachments/assets/1ba3c378-4977-4c1b-9574-05bf2f4d2b94)



## MpG vs Weight Plot

As illustrated in the graph below, the fitted function demonstrates a strong capability in estimating fuel consumption based on the weight of the vehicle. This relationship is crucial for understanding how weight impacts fuel efficiency.
The graph likely shows a clear trend, indicating that as weight increases, fuel consumption also tends to rise, which is consistent with expectations in automotive engineering.
The accuracy of the fitted model suggests that it can reliably predict fuel consumption for various vehicle weights, making it a valuable tool for manufacturers and consumers alike. This predictive ability can aid in making informed decisions related to vehicle design and efficiency improvements.


![image](https://github.com/user-attachments/assets/2df25bff-e553-449a-be99-74c93edb5b5d)



## Symbols and Notation

### Sets:
- **\( i \)** : warehouse  
- **\( j \)** : warehouse  
- **\( k \)** : truck  
- **\( s \)** : scenario  

### Decision Variables:
- **\( X<sub>ijks</sub> \)** : if truck \( k \) travels from warehouse \( i \) to warehouse \( j \) in scenario \( s \), then 1; otherwise, 0  
- **\( Y<sub>iks</sub> \)** : if warehouse \( i \) is supplied by truck \( k \) in scenario \( s \), then 1; otherwise, 0  
- **\( V<sub>ks</sub> \)** : if truck \( k \) in scenario \( s \) is used, then 1; otherwise, 0  
- **\( TL<sub>iks</sub> \)** : the time leaving warehouse \( i \) by truck \( k \) in scenario \( s \)  
- **\( WT<sub>ijks</sub> \)** : the weight of truck \( k \) with load when traveling from warehouse \( i \) to \( j \) in scenario \( s \)  
- **\( v<sub>is</sub> \)** : the time excess of truck arrival at warehouse \( i \) in scenario \( s \) beyond the normal duration


### Parameters
- **\( q<sub>si</sub> \)** : the demand at warehouse \( i \) in scenario \( s \)  
- **\( t<sub>i</sub> \)** : the unloading time at warehouse \( i \)  
- **\( F<sub>k</sub> \)** : the fixed cost of truck \( k \)  
- **\( MAT<sub>i</sub> \)** : the maximum allowable arrival time for truck at warehouse \( i \)  
- **\( FC \)** : the fuel cost per gallon  
- **\( GC \)** : the cost per unit of fresh goods  
- **\( w \)** : the carbon emission coefficient value  
- **\( E \)** : the energy produced per gallon of diesel fuel  
- **\( P<sub>1</sub> \)** : the power of refrigeration unit during driving  
- **\( P<sub>2</sub> \)** : the power of refrigeration unit during unloading  
- **\( TW \)** : truck weight  
- **\( Q \)** : cargo capacity of each truck  
- **\( CC \)** : the cost of carbon emissions per unit  
- **\( PC \)** : the penalty cost per unit time for late arrival of the vehicle at the front warehouse  
- **\( α \)** : a penalty factor for unloading time  
- **\( β \)** : a penalty factor for driving time  
- **\( d<sub>ij</sub> \)** : the distance between warehouses \( i \) and \( j \)  
- **\( speedhour(TL<sub>iks</sub>) \)** : the usual speed of the truck at time \( TL<sub>iks</sub> \)  
- **\( mpg(WT<sub>ijks</sub>) \)** : the fuel consumption of the truck in mpg when its weight is \( WT<sub>ijks</sub> \)


## Cost Analysis

### Fixed Cost
When a vehicle makes a delivery from the distribution center to the front warehouse, certain fixed costs need to be covered, such as the driver's salary and vehicle maintenance expenses. Since these fixed costs tend to remain constant, they are relatively low compared to the number of customers.

![image](https://github.com/user-attachments/assets/1904010e-b409-48a2-8baf-176ebe07e3d5)

---
### Refrigeration Cost
Vehicles used in cold chain logistics are equipped with refrigerated storage to maintain essential products. The refrigeration system operates on electricity produced from diesel fuel, meaning the cost of diesel reflects the refrigeration expenses. These costs can be categorized into two segments: the expenses incurred while driving and those incurred during the unloading process.

#### Expenses Incurred While Driving:
![image](https://github.com/user-attachments/assets/74bbfb89-b1bd-4dd7-9153-a3adc50d3096)


#### Expenses Incurred During the Unloading Process:
![image](https://github.com/user-attachments/assets/0a4ce0e8-dcc7-4418-8583-a6d930e5a589)


Thus, the overall refrigeration cost for the entire distribution process, denoted as \( C2 \), can be calculated by:

![image](https://github.com/user-attachments/assets/279ed54c-c05c-4b0c-b6f0-955de07def51)

---
### Fuel Consumption Cost

Considering the variable speeds of vehicles at different times of the day, the mpg data has been utilized and multiplied by the cost of each fuel unit. The fuel consumption cost is given by:

![image](https://github.com/user-attachments/assets/e90ed754-bdc9-4855-98b2-6acc277b8f84)

---
### Carbon Emission Cost

Since cold storage in cold chain logistics vehicles uses electric energy, there is no direct carbon emission cost. However, we need to consider the indirect carbon emission costs resulting from diesel consumption. Additionally, the vehicle's power, which is also derived from diesel fuel, contributes to carbon emissions. Consequently, the overall carbon emission cost comprises two components:

#### Indirect Carbon Emission Cost
The indirect carbon emission cost for the vehicle traveling from node \( i \) to node \( j \) can be represented as:

![image](https://github.com/user-attachments/assets/ee9af621-65e4-42f8-9076-50ddd7342353)

#### Fuel Consumption of the Vehicle Engine
The fuel consumption cost associated with the unloading process can be expressed as:

![image](https://github.com/user-attachments/assets/cdd1f9ce-3b58-4e01-8c1f-0e3e658ba21a)


#### Total Carbon Emission Cost
Hence, the total carbon emission cost \( C4 \) can be expressed as:

![image](https://github.com/user-attachments/assets/75a5c272-c0af-4afd-a459-c77c7053cf82)

---

### Penalty Cost

If trucks arrive late at demand points beyond a specified time, they must pay a penalty. The penalty cost \( C5 \) can be expressed as:

![image](https://github.com/user-attachments/assets/ba8a1a6e-8d96-4d3b-8de1-9842fcb94611)


---
## The Damage Cost

Fresh products transported by cold chain logistics vehicles are maintained at low temperatures to preserve their quality. However, factors such as compression and spoilage can lead to a decline in freshness throughout the distribution process. The total damage cost incurred during distribution comprises two components: the damage cost during transportation and the damage cost during unloading.

### Damage Cost During Transportation
The damage cost incurred during transportation can be expressed as:

![image](https://github.com/user-attachments/assets/b54269d7-e322-494f-a7a3-733026128df7)


### Damage Cost During Unloading
The damage cost incurred during unloading is given by:

![image](https://github.com/user-attachments/assets/93cf683f-2a46-4af0-bc04-a0b2ad9a66a5)


### Total Damage Cost
Hence, the total damage cost \( C6 \) can be expressed as:

![image](https://github.com/user-attachments/assets/5d0a8dd7-d173-45d8-a7c6-0d99392648c6)

## Model
























## Objective Function

The objective function is the total sum of all costs associated with the logistics process. It aims to optimize the overall efficiency and profitability of the distribution network by minimizing these costs.

## Constraints

### Constraint 1 to 6
These constraints represent various costs associated with the logistics process. They are incorporated into the objective function to ensure the optimization model accounts for all relevant expenses in the distribution network.

### Constraint 7
A truck does not return to the output warehouse immediately after making a delivery. This reflects the logistical reality that trucks often have to travel to multiple locations before returning.

### Constraint 8
Each warehouse is served by only one truck at a time. This helps streamline operations and minimizes potential traffic and congestion at the warehouses.

### Constraint 9
The amount of cargo that each truck delivers to various warehouses must remain below its maximum capacity. This is crucial for safety and efficiency.

## Constraints (Continued)

### Constraint 10
The total demands from all warehouses must be completely fulfilled. This ensures that customer needs are met and that the distribution network operates effectively.

### Constraints 11 to 13
If a truck departs from a warehouse, it must return to that same warehouse after completing its deliveries. This ensures consistency in routing.

### Constraint 14
Only one truck can pass through each warehouse at any given time. This helps avoid bottlenecks and ensures efficient loading and unloading.

### Constraint 15
If a truck enters a warehouse, it must exit from it after completing its tasks. This maintains flow and accountability in operations.

### Constraint 16
The number of warehouses must equal the number of delivery occurrences by trucks. This ensures that each warehouse is adequately serviced.

### Constraints 17 and 18
These constraints indicate which specific truck is being utilized for each delivery. Tracking is essential for managing logistics and scheduling efficiently.

## Additional Constraints

### Constraint 19
If a truck does not pass through a warehouse, it cannot deliver any cargo there. This underscores the importance of routing in the logistics process.

### Constraint 20
This constraint specifies how much delay is permissible in the delivery time to each warehouse, setting a standard for performance.

### Constraint 21
The exit time from the warehouse for each truck must be zero. This simplifies scheduling and ensures no unnecessary delays occur.

### Constraints 22 and 23
These constraints outline the specific departure times for each truck leaving each warehouse, which is critical for maintaining an organized schedule.

### Constraints 24 and 25
These ensure that every route taken by a truck must pass through a warehouse, centralizing operations effectively.

### Constraints 26 to 29
These specify the weight of each truck with its cargo as it travels between different points, ensuring compliance with weight regulations.

### Constraint 30
All trucks deployed in the logistics process must exit the warehouse. This ensures that no resources are left idle and that the distribution process is continually moving forward.


## Computational Experiments: Parameter Setting

### Node Data

| Node | Coordinates (mile) | Demand (ton) | q1   | q2   | q3   | q4   | Service Time (hr) | Desirable Time (h) | MAT |
|------|---------------------|---------------|------|------|------|------|--------------------|---------------------|-----|
| DC   | (50, 24)           | 0             | 0    | 0    | 0    | 0    | 0                  | 0                   | 0   |
| W1   | (3, 27)            | 1             | 0.74 | 0.7  | 0.65 | 0.6  | 1.6                | 1                   | 1   |
| W2   | (9, 7)             | 1             | 0.95 | 0.9  | 0.85 | 2.5  | 2.5                | 1.5                 | 1   |
| W3   | (22, 23)           | 0.68          | 0.65 | 0.6  | 0.55 | 0.6  | 0.6                | 1                   | 1   |
| W4   | (39, 8)            | 0.78          | 0.75 | 0.7  | 0.65 | 0.7  | 0.7                | 2                   | 2   |
| W5   | (30, 50)           | 0.5           | 0.45 | 0.4  | 0.35 | 0.3  | 0.3                | 4                   | 4   |
| W6   | (67, 26)           | 0.25          | 0.2  | 0.15 | 0.1  | 0.1  | 0.4                | 2.5                 | 2.5 |
| W7   | (72, 48)           | 0.8           | 0.75 | 0.7  | 0.65 | 0.4  | 0.4                | 2.5                 | 2.5 |
| W8   | (88, 6)            | 1             | 0.95 | 0.9  | 0.85 | 0.3  | 0.3                | 3                   | 3   |
| W9   | (80, 26)           | 0.9           | 0.85 | 0.8  | 0.75 | 0.5  | 0.5                | 1                   | 1   |
| W10  | (97, 49)           | 0.4           | 0.35 | 0.3  | 0.25 | 0.2  | 0.2                | 2                   | 2   |

### Parameters

| Parameter | Value |
|-----------|-------|
| FC        | 100   |
| GC        | 100   |
| w         | 2.5   |
| E         | 10    |
| P1        | 10    |
| P2        | 8     |
| Speed     | 5     |
| tw        | 12    |
| Q         | 2     |
| CC        | 6     |
| M         | 10,000|
| PC        | 100   |
| Alpha     | 1.0003|
| Beta      | 1.0002|

### Truck Costs

| Truck    | Fixed Cost ($) |
|----------|-----------------|
| Truck 0  | 250             |
| Truck 1  | 210             |
| Truck 2  | 215             |
| Truck 3  | 189             |
| Truck 4  | 220             |
| Truck 5  | 178             |
| Truck 6  | 146             |
| Truck 7  | 154             |
| Truck 8  | 198             |
| Truck 9  | 200             |

### Scenario Probabilities

| Scenario | Probability |
|----------|-------------|
| 0        | 0.2         |
| 1        | 0.4         |
| 2        | 0.15        |
| 3        | 0.25        |




## Results

This model, with its 6,288 variables and numerous constraints, is classified as NP-hard, indicating that it may require significant time to solve using existing software. To address this complexity, we ran the problem for five hours using the PuLP library in Python. The PuLP library starts with a feasible solution and progressively improves upon it over time. As the algorithm iterates, the differences between successive solutions decrease, suggesting that we can obtain a reasonably good solution after 3 hours of running the code. This is contingent upon having sufficiently small discrepancies between the solutions by the end of the run, ensuring that we achieve an optimal result within the allocated time.

First, we fit a regression function to the solutions obtained from the model over different time intervals and then visualize this function. We observe that the adjusted \( R^2 \) value is high, indicating a good fit. Additionally, after three hours, the value does not change significantly, suggesting that further iterations yield diminishing returns. Therefore, we consider the solution obtained at the three-hour mark as our final result, confident that it represents an optimal outcome given the stability of the adjusted \( R^2 \) value.

### Best Solution


<p align="center">
  <strong>best solution (seconds) = β<sub>0</sub> + β<sub>1</sub>(seconds)<sup>-t</sup></strong>
</p>

<p align="center">
  <strong>best solution (seconds) = 6158.4870 + 3894.9576(secs)<sup>-0.4</sup></strong>
</p>



![image](https://github.com/user-attachments/assets/f597531e-e191-45bb-979d-1e7d9d45a638)

![image](https://github.com/user-attachments/assets/39ab3f3b-3606-41e5-8ac9-793e8518f019)






























