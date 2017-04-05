---
title       : graphR 4 - Statistiques et modeles
description : Ces exercices visent a montrer les fonctions de ggplot2 qui permettent d'ajouter des informations statistiques ou des modeles de regression � vos graphiques

--- type:NormalExercise lang:r xp:50 skills:1 
## 1) Rajout d'un nuage de points montrant les moyennes


`ggplot2` et `diamonds` ont d�j� �t� charg�s.

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```

*** = instructions

**Compl�tez** le code ci-contre pour rajouter des **points bleus** montrant les moyennes de prix par coupe de diamant

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
success_msg("Oui! Visiblement, le prix d'un diamant est peu corr�l� � la perfection de sa coupe!")
```


--- type:MultipleChoiceExercise lang:r xp:50
## 2) Des mod�les par milliers?

**Examinez** le code suivant:

```{r}
p <- ggplot(diamonds, aes(x=carat, y=price)) +
  geom_point(aes(color=cut), alpha=0.1)+
  geom_smooth(method="lm", aes(linetype=clarity))
plot(p)
```
*** =instructions

Au vu de ces commandes, **combien de droites de r�gression** s'attendrait-on � voir sur le graphique correspondant?

- 5, autant que de niveaux de `cut`
- 8, autant que de niveaux de `clarity`
- 1, i.e. un mod�le global pour l'ensemble des donn�es
- 40, i.e. le nombre de niveaux de `cut` multipli� par le nombre de niveaux de `clarity`

*** =sct
```{r}
test_mc(correct = 2,
        feedback_msgs = c("Non, `cut` ne joue que sur la couleur des points",
                          "Oui! 8 niveaux, cela fait un graphique d�j� bien assez compliqu� comme �a!!",
                          "Non, `clarity` fait partie des esth�tiques de `geom_smooth`.",
                          "Ouhla, non! `cut` ne joue que sur la couleur des points..."))

```

--- type:NormalExercise lang:r xp:50 skills:1 
## 3) Modeles et facettes: youplaboum!


`ggplot2` et le jeu de donn�es `txhousing` ont d�j� �t� charg�s. `txhousing` contient des donn�es quant � des ventes immobili�res au texas entre 2000 et 2015.


*** =pre_exercise_code
```{r}
require(ggplot2)
data(txhousing)
```

*** = instructions

**Compl�tez** le code ci-contre pour 

- cr�er des **facettes** du graphique en fonction de la variable `city`
- faire en sorte que les **�chelles** des diff�rentes facettes soient **ind�pendantes** les unes des autres (voir l'aide de `facet_wrap`...)

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
test_function("geom_point",c("col"))
test_function("geom_smooth")
test_function("facet_wrap",c("facets","scales"))
```


