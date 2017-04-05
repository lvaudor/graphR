---
title       : graphR 3 - Axes, echelles et themes
description : Ces exercices visent a vous apprendre à paramétrer de manière plus fine les axes et échelles associés à vos graphiques

--- type:NormalExercise lang:r xp:75 skills:1
## 1) Etiquettes et transformations d'axes


*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```


*** =instructions

`ggplot2` et `diamonds` ont déjà été chargés.

**Modifiez** le code ci-contre pour que: 
- les étiquettes d'axes soient "coupe" (en x) et "prix" (en y)
- l'échelle des y soient transformée par une **transformation log10**
- les valeurs de l'axe x soient traduites (en "Correcte","Bonne","Très bonne","Premium","Idéale")

*** =sample_code
```{r}
p <- ggplot(diamonds, aes(x=cut, y=price)) +
  geom_boxplot(fill="pink") +
  _______ +
  _______ +
  _______
plot(p)
```


*** =solution
```{r}
p <- ggplot(diamonds, aes(x=cut, y=price)) +
  geom_boxplot(fill="pink") +
  labs(x="coupe",y="prix") +
  scale_y_log10() +
  scale_x_discrete(labels=c("Correcte","Bonne","Très bonne","Premium","Idéale"))
plot(p)
```
*** =sct
```{r}
test_error()
test_function("ggplot",c("data","mapping"))
test_function("geom_boxplot")
test_function("labs", c("x","y"))
test_function("scale_y_log10")
```

--- type:MultipleChoiceExercise lang:r xp:50
## 2) Types d'echelles colorees

Imaginons que je souhaite produire un **nuage de points** montrant `carat` en fonction de `cut`, en faisant **varier la couleur en fonction de `price`**. 

**Quelle fonction** devrais-je utiliser pour éventuellement **modifier l'échelle colorée**? (consultez l'antisèche ggplot2!)


*** =instructions

- scale_color_brewer()
- scale_color_gradient()
- scale_fill_brewer()
- scale_fill_gradient()

*** =sct
```{r}
test_mc(correct = 3,
        feedback_msgs = c("Non, `brewer` s'applique à des échelles discrètes, or ici `price` est continu",
                          "Non, ici on s'intéresse à une couleur de bordure et non une couleur de remplissage",
                          "Oui, bravo! Retenez cette solution pour l'exercice suivant...",
                          "Non, car ici on s'intéresse à une couleur de remplissage et à une échelle continue..."))
```


--- type:NormalExercise lang:r xp:50 skills:1
## 3) Themes et echelles colorees

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
p <-ggplot(diamonds, aes(x=cut, y=carat,color=price))+
  geom_jitter() +
  theme_minimal()+
  scale_color_gradient(low="yellow",high="blue")
plot(p)
```


*** =instructions

`ggplot2` et `diamonds` ont déjà été chargés, et un graphique produit.

Modifiez le code qui vous est fourni ci-contre pour reproduire cette figure. 

Il s'agit de 

- **modifier le thème** 
- **modifier l'échelle colorée** pour que les prix les plus bas correspondent à la couleur jaune et les prix les plus hauts à la couleur bleue.



*** =sample_code
```{r}
p <-ggplot(diamonds, aes(x=cut, y=carat,color=price))+
  geom_jitter() +
  __________()+
  __________(_______)
plot(p)
```

*** =solution
```{r}
p <-ggplot(diamonds, aes(x=cut, y=carat,color=price))+
  geom_jitter() +
  theme_minimal()+
  scale_color_gradient(low="yellow",high="blue")
plot(p)
```

*** =sct
```{r}
test_error()
test_function("ggplot",c("data","mapping"))
test_function("theme_minimal")
test_function("scale_color_gradient",c("low","high"))
```

