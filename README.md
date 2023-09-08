# Understanding-soccer-through-Data-Science
Expected Goals model to understand scoring chances in soccer.

## Project Description And Goal
Expected Goals or XG is a soccer metric that is used to evaluate players and
teams based on the quality of their scoring chances. XG models are probability
models that predict the chance of scoring a goal from a shot.
There are 2 parts to our project goal.
1) Develop an XG model that evaluates teams and players based on the
quality of shots.
2) Develop probability rings to understand scoring chances from different
locations on a soccer pitch.

## Data Specification and Extraction
Statsbomb is a leading data collection and analysis company based in the UK.
They release some of their event data to the public for free. This data can be
found on github (https://github.com/statsbomb/open-data). The data that we
are interested in is the ‘event data’. Event data is where every action on the ball
is tracked and recorded. The match event data files are stored on Statsbomb
GitHub as json files. We used Statsbombpy, a python library that extracts
Statsbomb json files, filters them based on competition and outputs a data
frame of time series event data.

For the purpose of our project we have selected two competitions. La Liga and
champions league. For each season we have collected all events with shot type.
A total of 13000 shots were extracted from la liga and approx 500 from
champions league.

## La-Liga Analysis
We analyzed how shots and goals are distributed on a soccer pitch. We also
looked at the frequency of scoring from different locations on a pitch. From the
plots below we can see that the frequency of shots being a goal increases as
we move closer to the goal line. This is a starting point to really understand XG
models. These plots show random events that happened in 17 seasons of
la-liga. Though they show kind of a trend, we cannot base our model on the
idea that a shot from certain positions will result in a goal.

![image](https://github.com/asadsk8r02/Understanding-soccer-through-Data-Science/assets/53692166/6fa80b76-7ae6-488b-954b-42f3bbd1dd6d) 
![image](https://github.com/asadsk8r02/Understanding-soccer-through-Data-Science/assets/53692166/d350fb97-babf-490f-9156-76905e137959)
![image](https://github.com/asadsk8r02/Understanding-soccer-through-Data-Science/assets/53692166/0507964f-0005-4c4c-963e-d949c8baf409)


We further analyzed how different shot features count towards different
outcomes of a shot. One interesting fact we found from this analysis is that
even though there are fewer shots taken from the left foot than the right foot,
the conversion count of these shots are almost equal.

![image](https://github.com/asadsk8r02/Understanding-soccer-through-Data-Science/assets/53692166/45b2beaf-1fda-46c4-ab2a-999a3817974e)
![image](https://github.com/asadsk8r02/Understanding-soccer-through-Data-Science/assets/53692166/cd521382-26e9-4e18-866e-e1af6a2147dc)
![image](https://github.com/asadsk8r02/Understanding-soccer-through-Data-Science/assets/53692166/74ef8940-2bb4-45fd-8050-453d47bf5bb6)

## Feature Creation and Encoding
### Feature Creation
● Distance from goal:

The distance between the player taking the shot and the goal
center is calculated in a same way as the distance between two points
with Cartesian coordinates A(x1, y1) and B(x2, y2), given by the formula:

Distance = √[(x₂ - x₁)² + (y₂ - y₁)²],

where x and y are the transformed coordinates with respect to goal.

● Angle from goal:

To calculate the angle from which the player has taken the shot, it
is required to take into consideration basic trigonometric laws. Using the
cartesian coordinates, distance from the goal, and width of the goal, the
following equation is formulated taking reference from the paper
entitled “A mathematics-based new penalty area in football: tackling
diving ”.

Angle = arctan((b*x) / (x**2+y**2 - ((b/2)**2))),

where x and y are the transformed coordinates with respect to goal and,
goal width (b) = 8 units

![image](https://github.com/asadsk8r02/Understanding-soccer-through-Data-Science/assets/53692166/16f3a44a-6efd-4f5b-bd3d-86938e81a8ae)

● Player count:

The player count is defined as the number of players from both
sides which are in front or causing occlusion in the view of goal for the
player taking the shot. Not all players which are in front or ahead of the
player taking the shots are considered but only in the triangular region
defined by cartesian coordinates of the goal post and the player taking
the shot. The following flowchart shows the formula applied and the
condition imposed in order to calculate the player count.

![image](https://github.com/asadsk8r02/Understanding-soccer-through-Data-Science/assets/53692166/3e49adfb-b211-406d-ab17-6317434058c9)
![image](https://github.com/asadsk8r02/Understanding-soccer-through-Data-Science/assets/53692166/799ba471-4df1-44bb-8cc4-376a87d1305e)

### Feature Encoding
The following features were encoded from categorial to numeric values.
● Shot outcome(Target) : 1 if goal else 0
● Shot technique
● Shot body part
● Shot type

















