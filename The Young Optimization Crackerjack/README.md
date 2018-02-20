https://datahack.analyticsvidhya.com/contest/the-young-optimization-crackerjack-contest/


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
