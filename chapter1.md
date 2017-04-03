---
title       : graphR 1 - Introduction
description : Ces exercices visent a vous familiariser avec le fonctionnement de base de ggplot2


--- type:NormalExercise lang:r xp:50 skills:1 key:0f0c9d8f87
## 1) Jeu de données

On considère le jeu de données `diamonds`, qui se trouve déjà dans l'environnement. Le package ggplot2 a déjà été chargé.

*** =sample_code
```{r}
require(ggplot2)
data(diamonds)
head(diamonds)

p <- ggplot(_____, aes(x=____)) +
  geom_point(col=_____)
```

*** =instructions

- **Examinez** le jeu de données `diamonds`
- **Complétez** le code ci-contre pour  tracer l'histogramme correspondant au prix des diamants (couleur de remplissage: `blue`).

*** =solution 
```{r}
data(diamonds)
head(diamonds)

p <- ggplot(diamonds, aes(x=price)) +
  geom_point(col="blue")
```

*** =sct
```{r}
test_object("p")
test_error()
test_function("geom_point",c("col"))
success_msg("Bien joué! vous avez fait votre premier graphique avec ggplot...")
```

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:3e7eb2f40e
## 2) Choix de geom

On considère le jeu de données `diamonds`, qui se trouve déjà dans l'environnement.

*** =instructions

Examinez les données et répondez à la question suivante. Quel **geom** est le **plus approprié** si je souhaite tracer `price` (y) en fonction de `depth` (x)?

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
