# Notebook Iteration and Change Log

This document serves as an overview of the developments made between each notebook, so that the solution iteration is easier to follow. 
Any additional features added, improvements made, or key alterations each week will be outlined here, and updated on a rolling basis.

## Week 1

- Created notebook, initialising data pipelines, models, and key performance metrics.
- Served as a starting point, building the key infrastructure that could be built upon.

## Week 2

- Added scaling to output data (y values).
This helped with boundary issues (models recommending new query points that were on the boundary of the sample space - this is not ideal).
Since the output values are so small in function 1, ranging from $10^{-121}$ to $10^{-16}$, it did not work well with scaling and all
values were approximated to 0.

## Week 3

- Huge improvements in performance metrics and visualisations:
-   Added improvement per iteration as a new plotted metric.
-   Visually improved graphs with better axis labelling and colouring.
-   Added best observed y value and next recommended query point to scatter plots,
  so it is easy to visualise how close the next query point is to the current, known maximum.
Also added a legend to the plots to increase interpretability.
