---
title       : graphR 1 - Introduction
description : Ces exercices visent a vous familiariser avec le fonctionnement de base de ggplot2


--- type:NormalExercise lang:r xp:50 skills:1 key:0f0c9d8f87
## 1) Jeu de données

On considère le jeu de données `diamonds`, fourni par la librairie `ggplot2`.

*** =sample_code

```{r}
library(ggplot2)
data(diamonds)
head(diamonds)

p <- ggplot(_____, aes(x=____)) +
  geom_histogram(fill=_____)

plot(p)
```

*** =instructions

- **Examinez** le jeu de données `diamonds`
- **Complétez** le code ci-contre pour  tracer l'histogramme correspondant au prix des diamants (couleur de remplissage: `blue`).

*** =solution 

```{r}
library(ggplot2)
data(diamonds)
head(diamonds)

p <- ggplot(diamonds, aes(x=price)) +
  geom_histogram(fill="blue")
plot(p)
```

*** =sct
```{r}
test_error()
test_function("geom_histogram",c("col"))
success_msg("Bien joué! vous avez fait votre premier graphique avec ggplot...")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:3e7eb2f40e
## 2) Choix de geom

On considère le jeu de données `diamonds`, qui se trouve déjà dans l'environnement.

Examinez les données et répondez à la question suivante. Quel **geom** est le **plus approprié** si je souhaite tracer `price` (y) en fonction de `depth` (x)?

*** =instructions

- un geom de type **point**
- un geom de type **histogram**
- un geom de type **boxplot**


*** =sct
```{r}
test_mc(correct = 1,
        feedback_msgs = c("Oui, les deux variables sont continues...",
                          "Non, un histogramme serait approprié pour un graphique univarié!",
                          "Non, un boxplot serait approprié pour une variable x catégorielle..."))
```


--- type:NormalExercise lang:r xp:50 skills:1 
## 3) Geom en tous genres

`ggplot2` et `diamonds` ont déjà été chargés.


*** =instructions
**Complétez** le code pour créer:

- `p1`, un nuage de points montrant **price** (y) en fonction de **carat** (x)
- `p2`, un boxplot montrant **price** (y) en fonction de **cut** (x)
- `p3`, un barplot montrant les effectifs de **cut** (x)

*** pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```


*** =sample_code
```{r}
# Graphique p1
p1 <- ggplot(diamonds, aes(x=___, y=___)) +
   ____()
plot(p1)

# Graphique p2
p2 <- ggplot(___________________________) +
  ______()
plot(p2)

# Graphique p3
p3 <- ______________________________________
  _____________
plot(p3)
```

*** =solution
```{r}
# Graphique p1
p1 <- ggplot(diamonds, aes(x=carat, y=price)) +
   geom_point()
plot(p1)

# Graphique p2
p2 <- ggplot(diamonds, aes(x=cut, y=price)) +
  geom_boxplot()
plot(p2)

# Graphique p3
p3 <- ggplot(diamonds, aes(x=cut)) +
  geom_bar()
plot(p3)
```

*** =sct
```{r}
test_object("p1")
test_object("p2")
test_object("p3")
success_msg("Bravo! Nous allons maintenant tenter de paramétrer un peu nos geoms...")
```

