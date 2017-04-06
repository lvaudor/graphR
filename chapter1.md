---
title       : graphR 1 - Introduction
description : Ces exercices visent a vous familiariser avec le fonctionnement de base de ggplot2


--- type:NormalExercise lang:r xp:50 skills:1 key:0f0c9d8f87
## 1) Jeu de donnees

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
test_function("ggplot",c("data","mapping"))
test_function("geom_histogram",c("fill"))
success_msg("Bien joué! vous avez fait votre premier graphique avec ggplot...")
```

*** =hint
Avez-vous bien spécifié le nom du tableau de données (`diamonds`, sans guillemets), le nom de la variable (`price`, sans guillemets) et la valeur du paramètre `fill` ("blue")?

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:3e7eb2f40e
## 2) Choix de geom

On considère le jeu de données `diamonds`. Ce jeu de données est fourni avec le package `ggplot2` et vous pouvez le charger dans la console ci-contre en chargeant le package puis le jeu de données

```{r}
library(ggplot2)
data(diamonds)
```

Pour en apprendre plus sur le contenu de ce jeu de données vous pouvez faire

```{r}
help(diamonds)
```


Examinez les données et répondez à la question suivante. Quel **geom** est le **plus approprié** si je souhaite tracer `price` (y) en fonction de `depth` (x)?

*** =instructions

- un geom de type **point**
- un geom de type **histogram**
- un geom de type **boxplot**


*** =sct
```{r}
test_mc(correct = 1,
        feedback_msgs = c("Oui, les deux variables sont numériques donc le nuage de point est tout indiqué...",
                          "Non, un histogramme serait approprié pour un graphique univarié!",
                          "Non, un boxplot serait approprié pour une variable x catégorielle..."))
```

*** =hint
Les deux variables sont numériques et continues...

--- type:NormalExercise lang:r xp:50 skills:1 key:86589879d3
## 3) Geom en tous genres

`ggplot2` et `diamonds` ont déjà été chargés.


*** =instructions
**Complétez** le code pour créer:

- `p1`, un nuage de points montrant **price** (y) en fonction de **carat** (x)
- `p2`, un boxplot montrant **price** (y) en fonction de **cut** (x)
- `p3`, un barplot (`geom_bar`) montrant les effectifs de **cut** (x)

*** =pre_exercise_code
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
test_error()
test_function("ggplot",c("data","mapping"),index=1)
test_function("ggplot",c("data","mapping"),index=2)
test_function("ggplot",c("data","mapping"),index=3)
test_function("geom_point")
test_function("geom_boxplot")
test_function("geom_bar")
success_msg("Bien! Il y a encore bien d'autres geoms disponibles, mais `point` et `boxplot` sont des incontournables...")
```

*** =hint
Il y a à chaque fois 3 éléments importants à spécifier: le **jeu de données**, les **variables x et** (éventuellement) **y**, et la **nature du geom**!


--- type:NormalExercise lang:r xp:50 skills:1 key:f9f76cfd80
## 4) Parametrer des geoms

`ggplot2` et `diamonds` ont déjà été chargés.

*** =pre_exercise_code
```{r}
require(ggplot2)
require(dplyr)
data(diamonds)
```

*** =instructions

On a repris les 3 graphiques créés précédemment, mais cette fois on souhaite paramétrer les geoms. **Complétez le code** pour que

- dans `p1`, les **points** soient **bleus**
- dans `p2`, l'**intérieur des boîtes** soit **rouge**
- dans `p3`, les barres soient **transparentes (à 50%)**

*** =sample_code
```{r}
# Graphique p1
p1 <- ggplot(diamonds, aes(x=carat, y=price)) +
   geom_point(___)
plot(p1)

# Graphique p2
p2 <- ggplot(diamonds, aes(x=cut, y=price)) +
  geom_boxplot(___)
plot(p2)

# Graphique p3
p3 <- ggplot(diamonds, aes(x=cut)) +
  geom_bar(____)
plot(p3)
```

*** =solution
```{r}
# Graphique p1
p1 <- ggplot(diamonds, aes(x=carat, y=price)) +
   geom_point(color="blue")
plot(p1)

# Graphique p2
p2 <- ggplot(diamonds, aes(x=cut, y=price)) +
  geom_boxplot(fill="red")
plot(p2)

# Graphique p3
p3 <- ggplot(diamonds, aes(x=cut)) +
  geom_bar(alpha=0.5)
plot(p3)
```
*** =sct
```{r}
test_error()
test_function("ggplot",c("data","mapping"),index=1)
test_function("ggplot",c("data","mapping"),index=2)
test_function("ggplot",c("data","mapping"),index=3)
test_function("geom_point",c("color"))
test_function("geom_boxplot",c("fill"))
test_function("geom_bar",c("alpha"))
success_msg("Bien joué! Quelle joie, vous allez pouvoir customiser tous vos graphiques en rose!")
```

*** =hint
Avez-vous bien trouvé le nom des paramètres qui vous intéressent? `color` pour la couleur de bordure, `fill` pour la couleur de remplissage, et `alpha` (valeurs entre 0 et 1) pour la transparence...

--- type:NormalExercise lang:r xp:50 skills:1 key:c3ac51eaa9
## 5) Superposer des geoms

`ggplot2` et `diamonds` ont déjà été chargés.

*** =pre_exercise_code
```{r}
require(ggplot2)
require(dplyr)
data(diamonds)
```

*** =instructions

**Complétez le code** pour représenter la variable `table` du jeu de données `diamonds` en **superposant** deux geoms:

- un geom de type **histogram**, et de couleur de remplissage jaune
- un geom de type **rug**

*** =sample_code
```{r}
p<-_____________________+
  _______________+
  ___________
plot(p)

```

*** =solution
```{r}
p <- ggplot(diamonds, aes(x=table)) +
  geom_histogram(fill="yellow") +
  geom_rug()
plot(p)
```

*** =sct
```{r}
test_error()
test_function("ggplot",c("data","mapping"))
test_function("geom_histogram", c("fill"))
test_function("geom_rug")
success_msg("Bravo! Vous êtes en bonne voie pour faire des graphiques vraiment sympas!...")
```

*** =hint
Avez-vous bien fait appel à la fonction `ggplot()` (pour créer le graphique), à `geom_histogram()` pour tracer l'histogramme, et à `geom_rug`  pour rajouter le "rug"?
