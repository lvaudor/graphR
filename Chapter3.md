---
title       : graphR 1 - Mapping et facettes
description : Ces exercices visent a vous familiariser avec le fonctionnement de base de ggplot2

--- type:NormalExercise lang:r xp:50 skills:1
## 1) Jeu de donn�es

On consid�re le jeu de donn�es `diamonds`, fourni par la librairie `ggplot2`.

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

- **Examinez** le jeu de donn�es `diamonds`
- **Compl�tez** le code ci-contre pour  tracer l'histogramme correspondant au prix des diamants (couleur de remplissage: `blue`).

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
success_msg("Bien jou�! vous avez fait votre premier graphique avec ggplot...")
```
