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


<p align="center">
  <img src="https://github.com/user-attachments/assets/0f9348a7-d9bf-47ed-99ae-9eb83f0b5e2f" alt="image" width="50%">
</p>

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

<p align="center">
  <img src="https://github.com/user-attachments/assets/1ba3c378-4977-4c1b-9574-05bf2f4d2b94" alt="image" width="60%">
</p>

## MpG vs Weight Plot

As illustrated in the graph below, the fitted function demonstrates a strong capability in estimating fuel consumption based on the weight of the vehicle. This relationship is crucial for understanding how weight impacts fuel efficiency.
The graph likely shows a clear trend, indicating that as weight increases, fuel consumption also tends to rise, which is consistent with expectations in automotive engineering.
The accuracy of the fitted model suggests that it can reliably predict fuel consumption for various vehicle weights, making it a valuable tool for manufacturers and consumers alike. This predictive ability can aid in making informed decisions related to vehicle design and efficiency improvements.


<p align="center">
  <img src="https://github.com/user-attachments/assets/2df25bff-e553-449a-be99-74c93edb5b5d" alt="image" width="60%">
</p>

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

<p align="center">
  <img src="https://github.com/user-attachments/assets/f5e6a235-f5b2-4e30-b188-56399b561ab6" alt="image" width="20%">
</p>

---

### Refrigeration Cost
Vehicles used in cold chain logistics are equipped with refrigerated storage to maintain essential products. The refrigeration system operates on electricity produced from diesel fuel, meaning the cost of diesel reflects the refrigeration expenses. These costs can be categorized into two segments: the expenses incurred while driving and those incurred during the unloading process.

#### Expenses Incurred While Driving:
<p align="center">
  <img src="https://github.com/user-attachments/assets/1b13892c-a26d-4c55-8400-bfe1a790db80" alt="image" width="53%">
</p>

#### Expenses Incurred During the Unloading Process:
<p align="center">
  <img src="https://github.com/user-attachments/assets/230e804b-aefe-4fdd-809b-c165a8c3beae" alt="image" width="36%">
</p>

Thus, the overall refrigeration cost for the entire distribution process, denoted as (C2), can be calculated by:

<p align="center">
  <img src="https://github.com/user-attachments/assets/27473b0a-e375-44e2-a885-88e99001ad19" alt="image" width="18%">
</p>


---

### Fuel Consumption Cost

Considering the variable speeds of vehicles at different times of the day, the mpg data has been utilized and multiplied by the cost of each fuel unit. The fuel consumption cost is given by:

<p align="center">
  <img src="https://github.com/user-attachments/assets/642742b7-d861-4ec3-93fb-35c89b3fadc4" alt="image" width="40%">
</p>

---

### Carbon Emission Cost

Since cold storage in cold chain logistics vehicles uses electric energy, there is no direct carbon emission cost. However, we need to consider the indirect carbon emission costs resulting from diesel consumption. Additionally, the vehicle's power, which is also derived from diesel fuel, contributes to carbon emissions. Consequently, the overall carbon emission cost comprises two components:

#### Indirect Carbon Emission Cost
The indirect carbon emission cost for the vehicle traveling from node \( i \) to node \( j \) can be represented as:

<p align="center">
  <img src="https://github.com/user-attachments/assets/0086c9cc-462b-4bf7-989d-d6a18b71c7a4" alt="image" width="65%">
</p>

#### Fuel Consumption of the Vehicle Engine

The fuel consumption cost associated with the unloading process can be expressed as:



#### Total Carbon Emission Cost
Hence, the total carbon emission cost \( C4 \) can be expressed as:

<p align="center">
  <img src="https://github.com/user-attachments/assets/6f02ceba-b90f-4770-9616-5a045d7e34e5" alt="image" width="19%">
</p>

---

### Penalty Cost

If trucks arrive late at demand points beyond a specified time, they must pay a penalty. The penalty cost \( C5 \) can be expressed as:

<p align="center">
  <img src="https://github.com/user-attachments/assets/30b6cab0-b457-4968-9f7a-a13b9c49e568" alt="image" width="20%">
</p>

---

### The Damage Cost

Fresh products transported by cold chain logistics vehicles are maintained at low temperatures to preserve their quality. However, factors such as compression and spoilage can lead to a decline in freshness throughout the distribution process. The total damage cost incurred during distribution comprises two components: the damage cost during transportation and the damage cost during unloading.

#### Damage Cost During Transportation
The damage cost incurred during transportation can be expressed as:

<p align="center">
  <img src="https://github.com/user-attachments/assets/e6f966f5-67b3-478d-aabf-58ae9c852595" alt="image" width="45%">
</p>

#### Damage Cost During Unloading
The damage cost incurred during unloading is given by:

<p align="center">
  <img src="https://github.com/user-attachments/assets/67a7c890-94cc-453b-b17c-71a928f4aa1d" alt="image" width="57%">
</p>

#### Total Damage Cost
Hence, the total damage cost \( C6 \) can be expressed as:

<p align="center">
  <img src="https://github.com/user-attachments/assets/9e523430-2ecf-4dd8-9ca5-d000fdeae14d" alt="image" width="18%">
</p>


## Model

![image](https://github.com/user-attachments/assets/d9542473-fe78-4a5c-9c34-040657f73dd5)
![image](https://github.com/user-attachments/assets/7e259674-180a-409c-a0f5-da7bd3506eaf)
![image](https://github.com/user-attachments/assets/341db89c-06b5-4d50-9229-ba0a046b8c06)
![image](https://github.com/user-attachments/assets/086d5e8f-ac30-4405-b5eb-439209094852)
![image](https://github.com/user-attachments/assets/5b5cffcb-5bf6-4877-899d-e5d8343724bf)
![image](https://github.com/user-attachments/assets/dc09cbd6-e5a9-4538-bb93-40edcd6cdd9d)






















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



<p align="center">
  <img src="https://github.com/user-attachments/assets/f597531e-e191-45bb-979d-1e7d9d45a638" alt="image" width="60%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/39ab3f3b-3606-41e5-8ac9-793e8518f019" alt="image" width="60%">
</p>



## Numerical Results

<p>
  <strong>Objective Function Value = 6271.4193239902371</strong><br>
  <strong>C1 = 768.5000000000001</strong><br>
  <strong>C2 = 690.4668189893814</strong><br>
  <strong>C3 = 2965.3618974141928</strong><br>
  <strong>C4 = 602.0195914334953</strong><br>
  <strong>C5 = 265.74164649999994</strong><br>
  <strong>C6 = 979.329369653168</strong>
</p>


<p align="center">
  <img src="https://github.com/user-attachments/assets/980d4fec-bc1c-4e2b-9b1b-f4f0c6932de3" alt="image" width="45%">
</p>

## Obtained Paths


<p align="center">
  <img src="https://github.com/user-attachments/assets/60c5b94f-22af-4251-8bbc-663af0a8ccbf" alt="image" width="60%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/8fba418a-42ea-4cf3-a1ea-84ef0ebe30a2" alt="image" width="60%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/d804ddc1-a60b-4e52-93d8-1b4774ac0753" alt="image" width="60%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/0eac4ad3-b023-4693-94a9-2088cee5ab85" alt="image" width="60%">
</p>

# Logistics Cost Analysis

This document provides an in-depth analysis of various costs associated with logistics operations, highlighting their significance in optimizing overall efficiency and cost-effectiveness. 

## Cost Breakdown

The pie chart below illustrates the ratios of different costs to the objective function value within the logistics context. Each cost category plays a crucial role in shaping operational strategies and enhancing financial performance.

### **Fuel Consumption Cost (C<sub>3</sub>) - 47.3%**

The most significant component, accounting for 47.3%, is the **fuel consumption cost**. This substantial share indicates that fuel expenses are a critical factor in overall logistics costs. Optimizing fuel efficiency not only leads to significant cost savings but also contributes to sustainability efforts by reducing environmental impact. Companies should consider investing in fuel-efficient technologies and practices to mitigate these expenses.

### **Damage Cost (C<sub>6</sub>) - 15.6%**

Following the fuel costs, the **damage cost** represents 15.6% of total expenses. This cost emphasizes the financial impact of product damage that occurs during transportation. Effective management strategies aimed at minimizing damage can significantly enhance the cost-effectiveness of logistics operations. Implementing better packaging and handling procedures can mitigate these risks and improve overall operational efficiency.

### **Delay Penalty Cost (C<sub>5</sub>) - 4.2%**

The **delay penalty cost**, while only 4.2%, is noteworthy due to its potential adverse effects on customer satisfaction and company reputation. Even a small percentage of penalties can accumulate, underscoring the importance of timely deliveries. Companies should focus on improving their scheduling and delivery processes to minimize delays and enhance customer relations.

### **Carbon Emission Cost (C<sub>4</sub>) - 9.6%**

At 9.6%, the **carbon emission cost** reflects the increasing concern regarding the environmental impact of logistics operations. This cost highlights the necessity for companies to adopt sustainable practices. By reducing carbon emissions, businesses can not only improve their public perception but also comply with regulatory requirements, fostering a responsible corporate image.

### **Fixed Cost (C<sub>1</sub>) - 12.3%**

The **fixed cost**, comprising 12.3% of total expenses, includes expenditures that do not vary with the volume of goods transported, such as salaries and equipment maintenance. These costs are essential to maintaining operational stability and should be monitored closely to ensure efficient resource allocation.

### **Refrigeration Cost (C<sub>2</sub>) - 11%**

Lastly, the **refrigeration cost**, accounting for 11%, pertains to expenses related to maintaining appropriate temperatures for perishable goods during transportation. Effective management of refrigeration can enhance the quality of goods delivered and reduce waste, thereby improving financial outcomes.

## Conclusion

In summary, the analysis indicates that fuel and damage costs are the most impactful on total logistics expenses. Strategic focus on these areas can lead to improved efficiency and reduced operational costs. Additionally, prioritizing environmental considerations and timely deliveries is essential for enhancing customer satisfaction and upholding corporate responsibility. Sustainable and efficient logistics practices will ultimately contribute to a company's long-term success in a competitive market.




#### Importance of Optimization

The findings demonstrate that integrating carbon emission costs into logistics optimization strategies not only reduces overall operational expenses but also significantly lowers carbon footprints. This dual benefit is increasingly crucial in today’s market, where consumers and regulatory bodies alike are demanding more sustainable practices from businesses. 

#### Strategic Framework

Furthermore, the proposed optimization model serves as a valuable tool for logistics firms aiming to improve their service delivery while adhering to stringent environmental standards. By focusing on the optimization of cold chain processes, companies can streamline operations, reduce waste, and enhance the quality of service provided to customers. This is especially significant in industries where product quality is directly linked to temperature control, such as food and pharmaceuticals.

#### Need for Innovation

As industries strive for sustainable development, it becomes imperative to adopt innovative approaches that effectively address the unique challenges of cold chain logistics. This includes leveraging advanced technologies such as IoT (Internet of Things) for real-time monitoring, AI for predictive analytics, and automation for efficiency. These innovations can facilitate better temperature management, optimize routing, and reduce energy consumption, aligning operational practices with sustainability goals.

#### Long-Term Impact

Ultimately, the optimization of cold chain logistics not only contributes to immediate cost savings but also positions companies as leaders in sustainable practices within their industries. By prioritizing environmental responsibility, logistics firms can enhance their brand reputation, attract eco-conscious consumers, and comply with increasingly stringent regulations. 
In summary, the integration of economic efficiency with environmental sustainability through optimized cold chain logistics is not merely a competitive advantage; it is becoming a necessity for business longevity and success in a rapidly evolving marketplace.








