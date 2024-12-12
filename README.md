java c
Prompt
Instructions
For each question in this assignment, show the steps of your calculation in R . (Please only use R to check your results.)
This assignment will be graded out of 100 points, where 100 / 100 = 100%.
Teams may talk to each other about how to approach the problems, but we expect each team to do their own work.
Please submit a .docx file listing your R code and responses, according to this format:
1: All lines of code must be clearly explained. 2: All analyses must be performed in R .
I highly recommend collaborating in Google Docs, but you must submit a .docx file at the end. (Google Doc share links will not be accepted.)
(All values below are hypothetical, unless otherwise indicated, for educational purposes, but are meant to be plausible examples.)
Be sure to review the Background and Measures tabs above before starting!
Background
Jolly Cobblers, a family-owned North Pole shoe store, has been selling quality shoes to Santa and his elves for generations.
Unfortunately, rising market competition has forced Jolly Cobblers to re-evaluate their product design, because after a night delivering presents, Santa’s boots face a lot of wear and tear; the backstay of the heel always breaks by the end of the night. Their customers need a sturdier boot, ASAP - otherwise Santa will just buy boots on Amazon instead.
So, the elves at Jolly Cobblers designed and implemented a factorial experiment to develop a more durable boot!
Measures
They measured the following outcome:
boot durability: the number of times an elf can hammer a boot heel with the weight of Santa Claus before the heel breaks.
For example, click here to see this Heel Stomper!
Then, they made a series of 240 boots, randomly assigning groups of 15 boots to a particular amount of leather , layers , foam thickness, and waterproofing solvent concentration. All other aspects of the production process were held constant.
leather: thickness of the leather, in millimeters ( 1.0 vs. 1.5 millimeters).
layers: layers of leather ( 2 vs. 3 )
foam: thickness of foam padding on the backstay ( 3.0 vs. 4.0 millimeters).
solvent: concentration of a water-proofing solvent ( 0.25 = 25% solvent with 75% water; 0.50 = equal parts solvent and water).
Santa needs some new boots!
Photo by Erik Mclean on Unsplash (https://unsplash.com/photos/4Q0QynPM8UA)
Data  Packages
# Load packages
library(tidyverse)
library(broom)
library(viridis)
library(metR)
# Questions 1-2 uses this dataset, 'boots.csv'
boots = read_csv("workshops/boots.csv")
# Questions 3-4 uses this dataset, 'allboots.csv"
allboots = read_csv("workshops/allboots.csv")
# Let's view the boots dataset
boots %>% glimpse()
## Rows: 240
## Columns: 7
## $ id  1, 2, 3, 4, 5, 6, 7, 8, 9, 1…
## $ group  1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
## $ durability  44, 123, 52, 62, 65, 82, 93,…
## $ thickness  1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
## $ layers  2, 2, 2, 2, 2, 2, 2, 2, 2, 2…
## $ foam  3, 3, 3, 3, 3, 3, 3, 3, 3, 3…
## $ solvent  0.25, 0.25, 0.25, 0.25, 0.25…
Staff at Jolly Cobblers are eager to use Six Sigma!
Photo by Karsten Winegeart on Unsplash (https://unsplash.com/s/photos/santa?
utm_source=unsplashutm_medium=referralutm_content=creditCopyText)
Q1. Factorial Design at 2 Levels (25 points)
Using the boots.csv dataset, create a table of contrasts estimating the direct/main effects and interaction effects (15 effects total). Use the difference of means in R (not a regression model).
This table should contain 15 rows and 5 columns, with columns for the (1) contrast , (2) estimated effect , (3) standard error ( se ), and (4) lower and (5) upper confidence intervals. Follow the instructions below to create this table, showing your work in R .
Hint: See Workshop 14
a. (5 points) Estimate the standard error for this factorial experiment’s differences of means.
Hint: See Workshop 14.2
b. (5 points) Estimate the direct/main effects of each treatment (4 total).
Hint: See Workshop 14.1
c. (10 points) Estimate all interaction effects of every possible unique combination of treatments (11 total).
Hint: See Workshop 14.5
d. (5 points) Use the data from parts a, b, and c to estimate upper and lower confidence intervals for each effect from parts b  c, with a 95% confidence level. Report the finished table, presenting results rounded to 1 decimal place.
Hint 1: (Optional) bind_cols() may help you combine data.frames .
Hint 2: See Workshop 14.4
Q2. Factorial Experiment Quantities of Interest (15 points)
a. (5 points) Using only the information gathered in Q1 part d, how would you determine which of the estimated effects are likely to be real, significant effects and not just due to sampling error? [Handwritten OK]
Hint: Look at the confidence intervals. Discussed in Lectures for Workshop 14, among others.
b. (10 points) Which of the estimated effects are likely to be the real effects and not just due to chance? Describe each significant effects in a sentence or more, listing (1) the contrast levels in their original units, (2) the estimated effect in units of times the boot heel is crushed, and (3) the confidence interval. [Handwritten OK]
Hint: Look at the confidence intervals. Discussed in Lectures for Workshop 14, among others.
BONUS: (+5 points) The present conditions of operation are the lower settings for each contrast ( thickness = 1 mm, layers = 2, foam = 3,  solvent = 0.25). Some of the代 写Factorial Design at 2 LevelsR
代做程序编程语言se potential changes cost more than others! Use the information below to deduce which of your significant effects is most cost effective.
For each boot, it costs…
$5 dollars to improve the thickness of the leather from 1 mm to 1.5mm,
$2 to increase the layers from 2 to 3,
$1 to increase the foam padding from 3 mm to 4 mm, and…
$2.5 to increase the concentration of waterproofing solvent from 25% to 50%.
Hint: Use the costs above to calculate the added-cost of each treatment effect (eg. the cost of switching solvent from 25% to 50% AND layers from 2 to 3 would be $2 + $2.50 = $4.50 ). Then, use your estimate to calculate the added-durability of a boot in times crushed per dollar spent! (Round your payoff to 1 decimal place.)
Hint: Don’t over-think it. It’s multiplication and division.
Q3. Interaction Models  RSM (25 points)
Enthused by their promising findings, the elves added a few more contrast levels to their existing treatment variables ( thickness = 1, 1.5,  2 mm, layers = 2, 3,  4, foam = 3, 3.5, 4, and solvent = 0.25 , 0.375 ,  0.5 ). Their data is available is allboots.csv (it’s very high tech at the North Pole).
# Import data for Questions 3-4
allboots = read_csv("workshops/allboots.csv")
# View it!
allboots %>% glimpse()
## Rows: 1,215
## Columns: 7
## $ id  1, 2, 3, 4, 5, 6, 7, 8, 9, 1…
## $ group  1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
## $ durability  44, 123, 52, 62, 65, 82, 93,…
## $ thickness  1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
## $ layers  2, 2, 2, 2, 2, 2, 2, 2, 2, 2…
## $ foam  3, 3, 3, 3, 3, 3, 3, 3, 3, 3…
## $ solvent  0.250, 0.250, 0.250, 0.250, …
a. (10 points) Estimate durability using a second-order polynomial model in lm() with all interaction effects, called m1 . Write out your entire model equation. (Example: Predicted Durability = 2.5 + 3 x thickness... etc.) (You may round coefficients to the first decimal place.)
Hint: See Workshop 15.1
b. (5 points) Your outcome is a count bounded at zero. Make 2 more models m2 and m3 , one of which models the square root of your outcome and one of which models the natural log of your outcome.
1. Report the , F statistic, and p-value for each model. (Round your your answers to 3 decimal places.) R2
2. Which of your 3 models fits best? How do you know?
Hint: See Workshop 15.1.3
c. (10 points) Using the best fitting model you selected in part b, generate a grid of predictions using all specs below in requirements (1), (2), and (3). Visualize that grid as a contour plot with labels in ggplot! (Do not use contour() .)
1. Vary the thickness from 1 to 4 by 0.1 mm each and number of layers from 1 to 4 by 1 layer each!
2. Hold the level of foam at their real current values of 3 mm and solvent at 25% . (Be sure to back-transform. your predictions if your outcome is transformed.)
3. Add clear labels, themes, and a visually appealing color palette (not the default blue).
Hint: See Workshop 15.2
Q4. RSM Quantities of Interest (35 points)
The elves are excited about their promising results, but they really need to refine them into usable quantities of interest for decision-making. Answer the questions below to help them analyze their results.
# Import data for Questions 3-4
allboots = read_csv("workshops/allboots.csv")
# View it!
allboots %>% glimpse()
## Rows: 1,215
## Columns: 7
## $ id  1, 2, 3, 4, 5, 6, 7, 8, 9, 1…
## $ group  1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
## $ durability  44, 123, 52, 62, 65, 82, 93,…
## $ thickness  1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
## $ layers  2, 2, 2, 2, 2, 2, 2, 2, 2, 2…
## $ foam  3, 3, 3, 3, 3, 3, 3, 3, 3, 3…
## $ solvent  0.250, 0.250, 0.250, 0.250, …
a. (5 points) Based on your grid from Q3 part c, without changing anything else, what precise thickness and total layers produces the optimal predicted durability ?
Hint: This is just dplyr data-wrangling. Use your data.frame. to find precise numbers.
b. (10 points) Calculate the predicted durability with a 95% simulated confidence interval, using 10,000 random draws, for the following situations:
1. predicted durability under optimal conditions (from Q4 part a)
2. predicted durability under current conditions. Current conditions are: thickness = 1 , layers = 2 , foam = 3 , and solvent = 0.25 .
Hint: Remember to back-transform. your outcome variable if necessary before getting quantiles() .)
c. (5 points) Visualize your two confidence intervals for the original vs.   optimal durability from Q4b in a single plot in ggplot !
(Be sure to use clear labeling, themes, and colors.)
Hint: Any of the strategies from Workshop 14.4.2
d. (10 points) Suppose you want to cut costs for the other factors. Apply Response Surface Methodology using the steps below to investigate the intervening effect of foam padding on durability:
Create a new grid, repeating the same conditions but allowing the level of foam padding to vary between 2 , 2.5 , and 3 mm.
Visualize the new plot, split into panels for each level of foam !
Each bin should have a width of 500 .
Hint: See Workshop 15.3.3
e. (5 points) For each level of foam, filter() to find the optimal durability and the associated level of thickness and layers . If you decrease the amount of foam padding, what do you need to do to the thickness and/or layers to achieve optimal durability ?
Hint: This is just data-wrangling. Use your dplyr toolkit.





         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
