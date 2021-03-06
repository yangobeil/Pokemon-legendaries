# Predict legendary Pokemons

This is a short machine learning project that uses a Pokemon dataset found on [kaggle](https://www.kaggle.com/abcsds/pokemon) (includes the first 6 generations) to predict if a Pokemon is Legendary or not from its stats and type. It turns out not to be the best dataset available in my opinion but it is a good exercise anyway.

We use the following 4 classification algorithms and pick the result from the best one:
- Logistic regression
- Naive Bayes
- k-Nearest Neighbors with 5 neighbors
- Random forest

## Data

The dataset contains 800 examples and 13 features

- Number (int): all values from 1 to 721, some repeated
- Name (str): 800 different values
- Type 1 (str): 18 different values
- Type 2 (str): 18 different values, 386 null entries
- Total (int): values from 180 to 780
- HP (int): values from 1 to 255
- Attack (int): values from 1 to 255
- Defense (int): values from 5 to 230
- Sp. Atk (int): values from 10 to 194
- Sp. Def (int): values from 20 to 230
- Speed (int): values from 5 to 180
- Generation (int): all values from 1 to 6
- Legendary (int): 735 False and 65 True

There are many small problems with this data that we need to take care of before using it. 

First of all there are null entries in the 'Type 2' feature. Since these don't come from missing data but from the fact that the Pokemons simply don't have a second type we convert these to the value 'none'. We also create dummy variables for the types of Pokemon, which converts the string variables 'Type 1' and 'type 2' to respectively 18 and 19 boolean variables.

Next we scan the 'Name' variable to see if a Pokemon is a mega evolution and we store this in a new variable called 'Mega'. We create a separate dataset where we eliminate the mega evolutions because they might get confused for legendaries.

## Features

Let's summarize a few of the most important relations visible in the data. 

By plotting the distribution of types, we see that there seems to be favored and disfavored types for legendaries, which don't necessarily correlate with the most popular types for non legendaries. This is not significant enough to allow directly to classify legendaries but should be a nice piece of the puzzle.

By studying the distribution of total skills we see a clear trend that the legendaries have higher total points. This will be extremely important to help us in our taks.

The generation and dual type features don't seem to discriminate between legendaries and non legendaries almost at all. Of course the name and number features don't tell us anything here.

Finally the distribution of total skills for mega evolutions is pretty similar to the one for legendaries so including may cause some confusion and it will hopefully be better to ignore them.


## Conclusions

The best algorithms seem to be kNN and random forest. We end up being able to predict with great accuracy if a Pokemon is legendary (around 96%). However since there are so few positive cases (65 legendaries out of 800 Pokemons) a better metric is the macro F1 score, which is a little bit lower but still good (around 87%). Getting rid of the mega evolutions helps improve the succes rate, most likely because they are strong so they look like legendaries even though they are not.

By looking at the examples that were wrongly classified we see a remaining problem in the data that may cause some errors. It turns out that there are Pokemons called mythical that have characteristics similar to legendaries but are officialy not (ex. Genesect or Cresselia). We could potentially get a better result by labeling them as legendaries.

Like mentionned above this is not the best dataset available on the web. There are better datasets that include features such as weight, height and catch rate. They also include each Pokemon once (no megas) and classify mythicals as legendary. I discovered this after fiishing this project and since the goal is just to learn the method and not to get the best model I didn't start over with the new data.
