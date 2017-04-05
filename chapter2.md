---
title       : graphR 1 - Mapping et facettes
description : Ces exercices visent a vous familiariser avec le fonctionnement de base de ggplot2

--- type:NormalExercise lang:r xp:100 skills:1 key:6910f622a9
## 1) Mapping

`ggplot2` et `diamonds` ont dÃ©jÃ  Ã©tÃ© chargÃ©s.

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```


*** =instructions

**ComplÃ©tez** le code ci- contre pour que:

- `p1`, `p2` et `p3` soient trois **nuages de points** reprÃ©sentant le **prix** (`price`) en fonction du **nombre de carats** (`carat`)
- la **couleur** des points de `p1` corresponde Ã  la coupe des diamants (`cut`)
- la **taille** des points de `p2` corresponde Ã  la table des diamants(`table`)
- `p3` remplisse **les deux conditions prÃ©cÃ©dentes** (couleur fonction de `cut` et taille fonction de `table`)

*** =sample_code

```{r}
p1 <- ggplot(diamonds, aes(x=___, y=___)) +
  geom_point(aes(____))
plot(p1)


p2 <- ggplot(________, aes(_____________))+
  geom_point(_________)
plot(p2)


p3 <- ggplot(____________________________)+
   ________(__________)
plot(p3)
```



*** =solution 

```{r}
p1 <- ggplot(diamonds, aes(x=carat, y=price)) +
  geom_point(aes(color=cut))
plot(p1)


p2 <- ggplot(diamonds, aes(x=carat, y=price))+
  geom_point(aes(size=table))
plot(p2)


p3 <- ggplot(diamonds, aes(x=carat, y=price))+
  geom_point(aes(size=table, color=cut))
plot(p3)
```

--- type:NormalExercise lang:r xp:100 skills:1 key:524d21b485
## 2) ParamÃ¨tres fixes vs paramÃ¨tres variables

<<<<<<< HEAD
=======
`ggplot2` et `diamonds` ont dÃ©jÃ  Ã©tÃ© chargÃ©s.

>>>>>>> 3cffc5f069b867911abc9897bc1978e10003b51e
*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```


*** =instructions

<<<<<<< HEAD
`ggplot2` et `diamonds` ont déjà été chargés. On reprend le dernier graphique créé, `p3`. 

**Modifiez** le code ci-contre pour que la **forme** des points corresponde à une étoile à 6 branches (voir l'antisèche ggplot2...)

=======
On reprend le dernier graphique crÃ©Ã©, `p3`. 

**Modifiez** le code ci-contre pour que la **forme** des points corresponde Ã  l'Ã©toile Ã  6 branches (voir l'antisÃ¨che ggplot2...)
>>>>>>> 3cffc5f069b867911abc9897bc1978e10003b51e

*** =sample_code

```{r}
p3 <- ggplot(diamonds, aes(x=carat, y=price))+
  geom_point(aes(size=table, color=cut))
plot(p3)
```

*** =solution 

```{r}
p3 <- ggplot(diamonds, aes(x=carat, y=price))+
  geom_point(shape=11, aes(size=table, color=cut))
plot(p3)
```

*** =sct
```{r}
test_error()
test_function("ggplot",c("data","mapping"))
test_function("geom_point",c("shape","mapping"))
success_msg("Oui! Vous pouvez soit dÃ©finir les paramÃ¨tres des geoms comme des constantes, ou bien les relier Ã  des variables via le processus de mapping...")
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:30600e01a4
## 3) Esthétique globale ou de geom

Considérez les lignes de codes suivantes:

```{r}
p <- ggplot(diamonds, aes(x=cut, y=carat, color=cut))+
  geom_boxplot(fill="grey") +
  geom_rug()
plot(p)
```

Quelle proposition est **vraie**?

*** =instructions

- la **couleur de remplissage** des boxplots dépend de `cut`
- la **couleur** des "rugs" est grise
- la **couleur de bordure** des boxplots est grise
- la **couleur de remplissage** des boxplots est grise

*** =sct
```{r}
test_mc(correct = 4,
        feedback_msgs = c("Non, c'est la couleur de bordure des boxplots qui dépend de `cut`",
                          "Non, la couleur des rugs dépend de `cut`!",
                          "Non, la couleur de bordure des boxplots dépend de `cut`...",
                          "Oui, bravo! Les paramètres renseignés dans l'appel à `ggplot()` valent pour l'ensemble des geoms..."))
p <- ggplot(diamonds, aes(x=cut, y=carat, color=cut))+
  geom_boxplot(fill="grey") +
  geom_rug(aes(color=cut))
plot(p)
```
