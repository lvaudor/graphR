---
title       : graphR 2 - Mapping et facettes
description : Ces exercices visent a vous familiariser avec les principes du mapping et des facettes, en vous permettant de repr�senter davantage d'information sur vos graphiques

--- type:NormalExercise lang:r xp:100 skills:1
## 1) Mapping

`ggplot2` et `diamonds` ont d�j� �t� charg�s.

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```


*** =instructions

**Compl�tez** le code ci- contre pour que:

- `p1`, `p2` et `p3` soient trois **nuages de points** repr�sentant le **prix** (`price`) en fonction du **nombre de carats** (`carat`)
- la **couleur** des points de `p1` corresponde � la coupe des diamants (`cut`)
- la **taille** des points de `p2` corresponde � la table des diamants(`table`)
- `p3` remplisse **les deux conditions pr�c�dentes** (couleur fonction de `cut` et taille fonction de `table`)

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

--- type:NormalExercise lang:r xp:100 skills:1
## 2) Parametres fixes vs parametres variables

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```


*** =instructions

`ggplot2` et `diamonds` ont d�j� �t� charg�s. On reprend le dernier graphique cr��, `p3`. 

**Modifiez** le code ci-contre pour que la **forme** des points corresponde � une �toile � 6 branches (voir l'antis�che ggplot2...)


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
success_msg("Oui! Vous pouvez soit d�finir les param�tres des geoms comme des constantes, ou bien les relier � des variables via le processus de mapping...")
```


--- type:MultipleChoiceExercise lang:r xp:50 skills:1
## 3) Esthetique globale ou de geom

Consid�rez les lignes de codes suivantes:

```{r}
p <- ggplot(diamonds, aes(x=cut, y=carat, color=cut))+
  geom_boxplot(fill="grey") +
  geom_rug()
plot(p)
```

Quelle proposition est **vraie**?

*** =instructions

- la **couleur de remplissage** des boxplots d�pend de `cut`
- la **couleur** des "rugs" est grise
- la **couleur de bordure** des boxplots est grise
- la **couleur de remplissage** des boxplots est grise

*** =sct
```{r}
test_mc(correct = 4,
        feedback_msgs = c("Non, c'est la couleur de bordure des boxplots qui d�pend de `cut`",
                          "Non, la couleur des rugs d�pend de `cut`!",
                          "Non, la couleur de bordure des boxplots d�pend de `cut`...",
                          "Oui, bravo! Les param�tres renseign�s dans l'appel � `ggplot()` valent pour l'ensemble des geoms..."))

```

--- type:NormalExercise lang:r xp:50 skills:1
## 4) Ajustement de la position


*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```


*** =instructions

`ggplot2` et `diamonds` ont d�j� �t� charg�s.

Examinez le code ci-contre et le graphique qu'il renvoie.

*** =sample_code
```{r}
p <- ggplot(diamonds, aes(x=carat))+
  geom_histogram(bins=10,aes(fill=cut))
plot(p)
```
**Corrigez** ce code pour que les effectifs des diff�rentes coupes apparaissent les **uns par dessus les autres** et que les hauteurs soient **normalis�s**(param�tre `position`... consultez votre antis�che!!)

*** =solution
```{r}
p <- ggplot(diamonds, aes(x=carat))+
  geom_histogram(bins=10, position="fill",aes(fill=cut))
plot(p)
```
*** =sct
```{r}
test_error()
test_function("ggplot",c("data","mapping"))
test_function("geom_histogram", c("bins","position","mapping"))
success_msg("Oui! Avez-vous pris le temps pour bien comprendre comment le param�tre `position` modifiait la fa�on dont on peut lire le graphique?")
```

--- type:NormalExercise lang:r xp:50 skills:1
## 5) Facettes


`ggplot2` et `diamonds` ont d�j� �t� charg�s.

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```

*** =instructions

Compl�tez le code ci-contre pour produire diff�rentes facettes du m�me graphique en fonction de la coupe des diamants (en ligne)

*** =sample_code
```{r}
p <- ggplot(diamonds, aes(x=carat, y=price, color=cut)) +
  geom_point() +
  ____________
plot(p)
```

*** =solution
```{r}
p <- ggplot(diamonds, aes(x=carat, y=price, color=cut)) +
  geom_point() +
  facet_grid(cut~.)
plot(p)
```

*** =sct
```{r}
test_error()
test_function("ggplot",c("data","mapping"))
test_function("geom_point")
test_function("facet_grid",c("facets"))
success_msg("Eh oui, bien jou�! Les facettes , c'est trop de la boule!")
```

