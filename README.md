# METHODOLOGY: Using machine learning to predict hall of famers and all stars from the 2017 draft

[Link to blog post.](https://dribbleanalytics.blogspot.com/2018/10/hof-all-star-rookies.html)

## Data collection

Reddit user SamShinkie gave me a database of every individual player season in Basketball Reference's database. Big thanks to him for the database. I would not have done this project without it.

Using the database, I took every rookie season since the 1979-1980 season (introduction of the 3-point line). The database had every Basketball Reference stat for each player. However, in my models, I used only the following stats:


| Shooting stats | Defensive/passing/rebounding stats | Other stats |
| ----------- | -------------------- | ----------- |
| FG/G | AST/G | G |
| FGA/G | STL/G | MPG |
| 2P% | BLK/G | |
| 3P% | TOV/G | |
| FT% | PF/G | |
| TS% | TRB/G | |
| 3PAr |  | 
| FTr | |

I then recorded these stats for every player in the 2017 draft class who played over 50 games. This restriction limited the number of players to 30, and excluded Markelle Fultz.

For a list of hall of famers, I used [this Hoophall list](http://www.hoophall.com/hall-of-famers/all/) to assign every hall of fame player in the database a value of 1 in the hall of fame column. It did not include the 2018 inductees, so I added those manually from Basketball Reference.

For a list of all stars, I used [this Basketball Reference page](https://www.basketball-reference.com/awards/all_star_by_player.html). Every player who made an all star team was assigned a value of 1 in the all star column.

Lastly, every player with above a 90% hall of fame probability according to [Basketball Reference's hall of fame calculator](https://www.basketball-reference.com/leaders/hof_prob.html) was given a value of 1. Manu Ginobili was also given a 1 despite his 20.05% probability, as it's clear he's making the hall of fame.

## Data organization

As mentioned above, I added two columns in the dataset: a hall of fame column, and an all star column. Every hall of famer or all star was assigned a value of 1, and everyone else was assigned a value of 0.

## Model creation

Using scikit-learn, I created four models: a support vector machine, a random forest, a k-Nearest Neighbors, and a deep neural network. Each model used scikit-learn's train test split function with a test size of 25%.

Each of these 4 models were created twice; once to have the hall of fame column as the output, and once to have the all star column as the output.

After creating the models, I performed a randomized search for hyperparameters. However, the randomized search did not change any of the models' predictions. Therefore, I stuck with my initially assigned hyperparameters.

## Predicting the best defenders in the draft

After making the models, I used the models to predict outputs for the rookie dataset.
