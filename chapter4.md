---
title       : graphR 4 - Statistiques et modeles
description : Ces exercices visent a montrer les fonctions de ggplot2 qui permettent d'ajouter des informations statistiques ou des modeles de regression à vos graphiques

--- type:NormalExercise lang:r xp:50 skills:1 key:1244c2331e
## 1) Rajout d'un nuage de points montrant les moyennes


`ggplot2` et `diamonds` ont déjà été chargés.

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```

*** = instructions

**Complétez** le code ci-contre pour rajouter des **points bleus** montrant les moyennes de prix par coupe de diamant

*** =sample_code

```{r}
p <- ggplot(diamonds, aes(x=cut, y=price)) +
  geom_boxplot(fill="pink")+
  stat_summary(___________)
plot(p)
```

*** =solution
```{r}
p <- ggplot(diamonds, aes(x=cut, y=price)) +
  geom_boxplot(fill="pink")+
  stat_summary(fun="mean", geom="point",color="blue")
plot(p)
```

*** =sct
```{r}
test_error()
test_function("ggplot",c("data","mapping"))
test_function("geom_boxplot",c("fill"))
test_function("stat_summary",c("fun","color"))
success_msg("Oui! Visiblement, le prix d'un diamant est peu corrélé à la perfection de sa coupe!")
```

*** =hint

Il y a 2 arguments à spécifier dans `stat_summary()`: `fun` et `geom`

--- type:MultipleChoiceExercise lang:r xp:50 key:cc4cc85035
## 2) Des modèles par milliers?

**Examinez** le code suivant:

```{r}
p <- ggplot(diamonds, aes(x=carat, y=price)) +
  geom_point(aes(color=cut), alpha=0.1)+
  geom_smooth(method="lm", aes(linetype=clarity))
plot(p)
```
*** =instructions

Au vu de ces commandes, **combien de droites de régression** s'attendrait-on à voir sur le graphique correspondant?

- 5, autant que de niveaux de `cut`
- 8, autant que de niveaux de `clarity`
- 1, i.e. un modèle global pour l'ensemble des données
- 40, i.e. le nombre de niveaux de `cut` multiplié par le nombre de niveaux de `clarity`

*** =sct
```{r}
test_mc(correct = 2,
        feedback_msgs = c("Non, `cut` ne joue que sur la couleur des points",
                          "Oui! 8 niveaux, cela fait un graphique déjà bien assez compliqué comme ça!!",
                          "Non, `clarity` fait partie des esthétiques de `geom_smooth`.",
                          "Ouhla, non! `cut` ne joue que sur la couleur des points..."))

```

*** =hint
`cut` ne joue que sur le `geom_point()` et non sur le graphique dans son ensemble...

--- type:NormalExercise lang:r xp:50 skills:1 key:9fbf20c316
## 3) Modeles et facettes: youplaboum!


`ggplot2` et le jeu de données `txhousing` ont déjà été chargés. `txhousing` contient des données quant à des ventes immobilières au texas entre 2000 et 2015.


*** =pre_exercise_code
```{r}
require(ggplot2)
data(txhousing)
```

*** = instructions

**Complétez** le code ci-contre pour 

- créer des **facettes** du graphique en fonction de la variable `city`
- faire en sorte que les **échelles** des différentes facettes soient **indépendantes** les unes des autres (voir l'aide de `facet_wrap`...)

*** =sample_code

```{r}
p <- ggplot(txhousing, aes(x=date, y=volume))+
  geom_line()+
  geom_smooth()+
  facet_wrap(________)
plot(p)
```

*** =solution
```{r}
p <- ggplot(txhousing, aes(x=date, y=volume))+
  geom_line()+
  geom_smooth()+
  facet_wrap(~city, scales="free")
plot(p)
```

*** =sct
```{r}
test_error()
test_function("ggplot",c("data","mapping"))
test_function("geom_line")
test_function("geom_smooth")
test_function("facet_wrap",c("facets","scales"))
success_msg("Oui, bravo! Avez-vous remarqué comme la création de facettes affecte l'ensemble du graphique (et notamment le `geom_smooth()`? Vous pouvez fermer cette fenêtre et double-cliquer sur le graphique si vous voulez l'examiner de plus près...")
```


