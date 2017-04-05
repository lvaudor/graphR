---
title       : graphR 1 - Mapping et facettes
description : Ces exercices visent a vous familiariser avec le fonctionnement de base de ggplot2

--- type:NormalExercise lang:r xp:50 skills:1 key:d5b0ebb77b
## 1) Jeu de données

On considère le jeu de données `diamonds`, fourni par la librairie `ggplot2`.

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```

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
test_function("ggplot",c("data","mapping"))
test_function("geom_histogram",c("fill"))
success_msg("Bien joué! vous avez fait votre premier graphique avec ggplot...")
```
