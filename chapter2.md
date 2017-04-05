---
title       : graphR 1 - Mapping et facettes
description : Ces exercices visent a vous familiariser avec le fonctionnement de base de ggplot2

--- type:NormalExercise lang:r xp:100 skills:1 key:6910f622a9
## 1) Mapping

<<<<<<< HEAD
`ggplot2` et `diamonds` ont déjà été chargés.
=======
`ggplot2` et `diamonds` ont dÃƒÂ©jÃƒÂ  ÃƒÂ©tÃƒÂ© chargÃƒÂ©s.
>>>>>>> fd224fd9127ca1a54c6753227b157c2fc7923991

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```


*** =instructions

<<<<<<< HEAD
**Complétez** le code ci- contre pour que:

- `p1`, `p2` et `p3` soient trois **nuages de points** représentant le **prix** (`price`) en fonction du **nombre de carats** (`carat`)
- la **couleur** des points de `p1` corresponde à la coupe des diamants (`cut`)
- la **taille** des points de `p2` corresponde à la table des diamants(`table`)
- `p3` remplisse **les deux conditions précédentes** (couleur fonction de `cut` et taille fonction de `table`)
=======
**ComplÃƒÂ©tez** le code ci- contre pour que:

- `p1`, `p2` et `p3` soient trois **nuages de points** reprÃƒÂ©sentant le **prix** (`price`) en fonction du **nombre de carats** (`carat`)
- la **couleur** des points de `p1` corresponde ÃƒÂ  la coupe des diamants (`cut`)
- la **taille** des points de `p2` corresponde ÃƒÂ  la table des diamants(`table`)
- `p3` remplisse **les deux conditions prÃƒÂ©cÃƒÂ©dentes** (couleur fonction de `cut` et taille fonction de `table`)
>>>>>>> fd224fd9127ca1a54c6753227b157c2fc7923991

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

<<<<<<< HEAD
--- type:NormalExercise lang:r xp:100 skills:1 key:979e26f73b
## 2) Paramètres fixes vs paramètres variables

=======
--- type:NormalExercise lang:r xp:100 skills:1 key:524d21b485
## 2) ParamÃƒÂ¨tres fixes vs paramÃƒÂ¨tres variables

<<<<<<< HEAD
=======
`ggplot2` et `diamonds` ont dÃƒÂ©jÃƒÂ  ÃƒÂ©tÃƒÂ© chargÃƒÂ©s.

>>>>>>> 3cffc5f069b867911abc9897bc1978e10003b51e
>>>>>>> fd224fd9127ca1a54c6753227b157c2fc7923991
*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```


*** =instructions

<<<<<<< HEAD
`ggplot2` et `diamonds` ont déjà été chargés. On reprend le dernier graphique créé, `p3`. 
=======
<<<<<<< HEAD
`ggplot2` et `diamonds` ont dÃ©jÃ  Ã©tÃ© chargÃ©s. On reprend le dernier graphique crÃ©Ã©, `p3`. 
>>>>>>> fd224fd9127ca1a54c6753227b157c2fc7923991

**Modifiez** le code ci-contre pour que la **forme** des points corresponde Ã  une Ã©toile Ã  6 branches (voir l'antisÃ¨che ggplot2...)

<<<<<<< HEAD
=======
=======
On reprend le dernier graphique crÃƒÂ©ÃƒÂ©, `p3`. 

**Modifiez** le code ci-contre pour que la **forme** des points corresponde ÃƒÂ  l'ÃƒÂ©toile ÃƒÂ  6 branches (voir l'antisÃƒÂ¨che ggplot2...)
>>>>>>> 3cffc5f069b867911abc9897bc1978e10003b51e
>>>>>>> fd224fd9127ca1a54c6753227b157c2fc7923991

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
<<<<<<< HEAD
success_msg("Oui! Vous pouvez soit définir les paramètres des geoms comme des constantes, ou bien les relier à des variables via le processus de mapping...")
=======
success_msg("Oui! Vous pouvez soit dÃƒÂ©finir les paramÃƒÂ¨tres des geoms comme des constantes, ou bien les relier ÃƒÂ  des variables via le processus de mapping...")
>>>>>>> fd224fd9127ca1a54c6753227b157c2fc7923991
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:30600e01a4
## 3) EsthÃ©tique globale ou de geom

ConsidÃ©rez les lignes de codes suivantes:

```{r}
p <- ggplot(diamonds, aes(x=cut, y=carat, color=cut))+
  geom_boxplot(fill="grey") +
  geom_rug()
plot(p)
```

Quelle proposition est **vraie**?

*** =instructions

- la **couleur de remplissage** des boxplots dÃ©pend de `cut`
- la **couleur** des "rugs" est grise
- la **couleur de bordure** des boxplots est grise
- la **couleur de remplissage** des boxplots est grise

*** =sct
```{r}
test_mc(correct = 4,
<<<<<<< HEAD
        feedback_msgs = c("Non, c'est la couleur de bordure des boxplots qui dépend de `cut`",
                          "Non, la couleur des rugs dépend de `cut`!",
                          "Non, la couleur de bordure des boxplots dépend de `cut`...",
                          "Oui, bravo! Les paramètres renseignés dans l'appel à `ggplot()` valent pour l'ensemble des geoms..."))
require(ggplot2)
data(diamonds)
=======
        feedback_msgs = c("Non, c'est la couleur de bordure des boxplots qui dÃ©pend de `cut`",
                          "Non, la couleur des rugs dÃ©pend de `cut`!",
                          "Non, la couleur de bordure des boxplots dÃ©pend de `cut`...",
                          "Oui, bravo! Les paramÃ¨tres renseignÃ©s dans l'appel Ã  `ggplot()` valent pour l'ensemble des geoms..."))
>>>>>>> fd224fd9127ca1a54c6753227b157c2fc7923991
p <- ggplot(diamonds, aes(x=cut, y=carat, color=cut))+
  geom_boxplot(fill="grey") +
  geom_rug(aes(color=cut))
plot(p)
```
