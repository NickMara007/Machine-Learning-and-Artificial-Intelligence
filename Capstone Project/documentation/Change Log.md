# Notebook Iteration and Change Log

This document serves as an overview of the developments made between each notebook, so that the solution iteration is easier to follow. 
Any additional features added, improvements made, or key alterations each week will be outlined here, and updated on a rolling basis.

Some weeks there were major changes to the notebook, whilst in others there were very few. Generally, as the project progressed I made fewer alterations to the models and visualisations since they had already been updated, leaving less room for any further improvements to be made. This was especially true during the final few rounds where the model was performing well and there was little need to make drastic changes.

## Week 1

- Created notebook, initialising data pipelines, models, and key performance metrics.
- Served as a starting point, building the key infrastructure that could be built upon.

## Week 2

- Added scaling to output data (y values).
This helped with boundary issues (models recommending new query points that were on the boundary of the sample space - this is not ideal).
Since the output values are so small in function 1, ranging from $10^{-121}$ to $10^{-16}$ in magnitude, it did not work well with scaling as all
values were approximated to 0. Therefore, function 1 was left unscaled.

## Week 3

- Huge improvements in performance metrics and visualisations:
  -   Added improvement per iteration as a new plotted metric.
  -   Visually improved graphs with better axis labelling and colouring.
  -   Reformatted performance metric plots from a 1x3 to a 2x2 arrangement.
  -   Added best observed y value and next recommended query point to scatter plots,
  so it is easy to visualise how close the next query point is to the current best observed value.
  -  Added a legend to scatter plots for increased interpretability.
 
## Week 4

- Improved colour coding on scatter plots to make it more intuitive.

## Week 5

Huge improvements and changes this week:
- Added a neural network for each objective function, which is trained on observed data, then used to predict the probability of X-candidate points being in a 'high performing' region (defined as being in the top 20% of observed y-values).
- Factored these probabilities into the acquisition function calculation, so that both Gaussian Process and neural network models were contributing to the next query point selection.
- Added the `current_week` variable, which is defined at the top of the notebook. This variable is used in the file paths to retrieve the current week's data, so that it only has to be changed once each week instead of going through each objective function and manually changing the path.
- This increased the level of automation within the project, and helped me to save time which can be used to focus on improving the model rather than changing file paths each week.
- Decluttered the notebook massively by converting recurring code into functions at the beginning of the notebook, which are used and called for each objective function. This included:
  - Acquisition function calculations
  - Performance metric calculations and visualisations
  - Scatter, contour, and mesh plot visualisations

## Week 6

- Added previous query point to pair scatter plots, to give a visual comparison of how close it is to the next and best-perfroming query points, helping to give a greater level of intuition and understanding of where the data points lie.
- For functions 1 and 2: updated the acquisition function 3D mesh plots to incorporate the neural network probabilities, so that model behaviour aligned with visualisations.

 ## Week 7

 **Functions 1 and 2:**
 - Swicthed to sobol sampling from random sampling, to generate candidiate query points.
 - Added `if` statements to easily switch between acqusisition functions (UCB and EI).
 - Completely overhauled the mesh and contour plots since I found they were massively inaccurate:
   - These original visualisations were derived from defining a new and separate set of candidate points through creating a mesh grid, used only for visualisation. The GP and neural network models then made predictions on these new points.
   - Instead, the new visualisations use the exact same set of generated X-candidate points (from sobol sampling) that the actual models use, meaning that model behaviour is now represented accurately by the contour and mesh plots.

From this image of the original contour plots, you can clearly see how the areas of low uncertainty do not line up with where the queried data points are in the search space:

<img width="436" height="383" alt="image" src="https://github.com/user-attachments/assets/16549b17-be8c-445a-83f7-f6cb25c6431b" />

With the improved contour plots, you can see that the areas of low uncertainty do line up with the observed data points, as expected:

<img width="407" height="387" alt="image" src="https://github.com/user-attachments/assets/e4c10a7a-808b-43ff-9d3d-b493c8f66709" />

- Added mesh plots to visualise the neural network's probabilistic predictions:

<img width="526" height="435" alt="image" src="https://github.com/user-attachments/assets/e36a522b-9833-4e7e-9910-ca107ffe21ac" />

**Function 3:**
- Switched to sobol sampling from random sampling.

**Function 5:**
- Added `if` statements to easily switch between acquisition functions (UCB and EI).

 ## Week 8

 For the remainder of the functions:
 - Added `if` statements to easily switch between acquisition functions (UCB and EI).

## Week 9

**For all functions:**
- Increased number of X candidate points via sobol sampling from $2^{15}$ to $2^{16}$.

**Functions 3 and 4:**
- Added contour feature pair contour plots for these higher dimensional functions. Due to the high dimensionality, it proved to not be very useful in providing an accurate visual representation of mean, uncertainty, and acquisition function values.

## Week 10

**Function 1:**
- Applied a transformation to y (output data) to help with surrogate modelling. Due to the scale of the nature being extremely small, ranging from $10^{-3}$ to $10^{-124}$ in magnitude, the GP was giving inaccurate mean estimates, causing aquisition functions to suggest query points at the edge of the search space which are dead areas.

**All functions:**
- Altered function input data presentation slighlty for increased clarity.

## Week 11

**Function 3 and 4:**
- Removed higher-dimensional contour plots, since they did not provide an accurate visual representation of mean, uncertainty, or acquisition function values, like they did in two dimensions (for functions 1 and 2).

## Week 12

**Function 1:**
- Changed kernel from RBF to Matern ($\nu$ = 2.5) and set `normalize_y = True`. This improved modelling and the acquisition function was not suggesting query points on the edge of the search space anymore.

## Week 13

No changes to the notebook this week.
