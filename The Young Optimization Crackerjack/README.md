https://datahack.analyticsvidhya.com/contest/the-young-optimization-crackerjack-contest/

Problem Statement
ABC is a global manufacturer of pharmaceutical products serving customers across 18 regions.They have 81 SKUs in their portfolio.

ABC has 3 manufacturing plants (A, B, & C) in different parts of the world. Each plant has multiple production lines and different production costs. Shipping costs from each plant differs for all 18 regions.

A senior client, VP – Production Planning, is wondering how to plan production for the coming quarter.

Objective is twofold: -

Forecast demand with high accuracy
Meet minimum production constraints and maximize profit margin ((revenue -cost)/cost).
The major decision to be taken are –

Forecast demand for next quarter based on historical data (36 months of historical data is present)
Sourcing demand from different plants
Sequencing of product for each production line
The ideal output the client is looking for is a 3-month forward looking schedule for each production line and order fulfillment rate for each product. Provide forecasted demand values and shipped volumes for plant-region combination as well.

Constraints:
Active days for production and change-over per month is 30 days
Consecutive days of production per batch is 14 days
You must do production at least one day for each month
After consecutive run of a product for 14 days either a changeover is required if switching to another product or a non-production day is required if continuing production of same product
Minimum run for a production is 1 day
Production should be able to meet at least 50% of total demand each month (carried forward inventory can also be used for meeting demand)
Production should produce atleast 30% of total quarterly demand for each product
Changeover time is specified for changeover from a product to another product
Inventory can be carried forward to next month at nil cost in same plant and cannot be transferred from one plant to another
Demand is valid only for the month – it cannot be back fulfilled. If demand is not fulfilled in a month they are considered as lost sales
There is no starting inventory at any plant and ending inventory after last month will not be considered for revenue recognition
Datasets
historical_demand.csv: The historical demand (Metric Ton (MT)) for a SKU in a region is provided for last 36 months.
demand_price.csv: The revenue of a SKU in a region is calculated based on selling price and quantity.
production_cost.csv: Cost of producing a MT of a SKU by a production plant. All the lines in a production plant will have same production cost.
production_capacity.csv: Quantity of a product (in MT) produced in a day on a production line. Wherever it is zero or blank, that SKU and production line combination is not valid
fixed_cost.csv: ($/day)Each production line has fixed cost which charged each day. This will be charged irrespective of production line is in production, changeover or idle.
delivery_cost.csv: ($/MT)Logistics cost is the cost of shipping a MT of a SKU from a production plant to a region. These are applied to all shipments. Shipments between plants are not allowed
changeover_days.csv: Changeover days matrix by production line (in Days)For each change in the SKU production on a production line, the production line settings need to be changed. The time taken for setting up production line depends upon the existing SKU and new SKU. These are non-production days and mandatory to change production from one SKU to another SKU. These are given in number of Days.
changeover_cost.csv: Changeover unit cost by production lines ($/ Changeover)For each production changeover on a line, there are costs associated with it. These are charged for each changeover on all lines.



Tips for solving the crackerjack competition
The approach we recommend is to divide this problem into multiple smaller sub-problems and solve them using the 80-20 approach. The aim is to reach a feasible solution and then attempt to increase its optimality. A few examples of sub-problems are:

forecasting
scheduling
sequencing
transportation distribution
For instance, the first objective of making a forecast for the next 3 months can be accomplished using a time-series forecasting technique. It’s a fairly straight-forward approach. You can think about aggregation and disaggregation approaches as well.

Below, we have mentioned the steps you can follow to solve a sourcing/sequencing problem:

Aim to solve the problem for the first month and use the same approach for the second and third months.
Sourcing can be formulated as a scheduling problem. Basically, it can be said to be both a scheduling and a sequencing problem. You can solve it one by one – first look at the scheduling part and then the sequencing part.
First a few thoughts on the scheduling (sourcing) problem:
Scheduling can be a relatively easy exercise if we add aggregated product demand in rows and plant capacity in columns. By doing this, we get a 81 x 6 matrix for 81 SKUs and 6 production lines. It is quite easy to solve this as a product mix problem using Excel solver or some other linear programming solver (or any heuristics approach). Minimize for the production cost and add capacity constraints for each production line as approximate capacity at monthly level.
Don’t worry if you can’t produce for full demand. The plant obviously doesn’t have the capacity to produce for the demand of all the SKUs. So start with only 30-40% of SKUs and then keep adding more as you go.
Solve for items that have the lowest processing time so that you can aim to produce for maximum demand possible (or try out a few variations here).
Once you have the schedule for one month, then you can try sequencing it on the production lines.
Use variations of “greedy” algorithm (consider Local Search, Constraint programming or other heuristics technique). For example, you can sort the setup time matrix in ascending order (lowest setup time in the top-left corner and highest setup time in the bottom right corner). Also, look-out for patterns in changeover matrix.
Then start sequencing products exactly as per this sorted setup time matrix.
You can minimize setup time and maximize production time by this method or a similar greedy algorithm.
Once you have a solution that works for one month, you can then try to validate for constraints.

If required, some “hand adjustments” can also be made. We don’t necessarily need a fully automated process to make this work (at least not in the first attempt).

We can then move onto building a similar solution for the remaining two months.

Don’t lose hope, keep trying!
