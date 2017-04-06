---
title       : graphR 2 - Mapping et facettes
description : Ces exercices visent a vous familiariser avec les principes du mapping et des facettes, en vous permettant de représenter davantage d'information sur vos graphiques

--- type:NormalExercise lang:r xp:75 skills:1 key:6910f622a9
## 1) Mapping

`ggplot2` et `diamonds` ont déjà été chargés.

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```

*** =instructions

**Complétez** le code ci- contre pour que:

- `p1`, `p2` et `p3` soient trois **nuages de points** représentant le **prix** (`price`) en fonction du **nombre de carats** (`carat`)
- la **couleur** du `geom_point()` de `p1` corresponde à la coupe des diamants (`cut`)
- la **taille** du `geom_point()` de `p2` corresponde à la table des diamants(`table`)
- **les deux conditions précédentes** soient remplies pour le `geom_point()` de `p3` 

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

*** =sct
```{r}
test_error()
test_function("ggplot",c("data","mapping"),index=1)
test_function("ggplot",c("data","mapping"),index=2)
test_function("ggplot",c("data","mapping"),index=3)
test_function("geom_point",c("mapping"),index=1)
test_function("geom_point",c("mapping"),index=2)
test_function("geom_point",c("mapping"),index=3)
success_msg("Très bien! En faisant du **mapping** vous ajoutez des informations supplémentaires à votre graphique uni ou bivarié...")
```

*** =hint
Avez-vous bien fait appel à la fonction `aes()` dans vos appels à `geom_point()`? 

Cette fonction `aes()` peut prendre plusieurs arguments, séparés par une virgule...

--- type:NormalExercise lang:r xp:75 skills:1 key:979e26f73b
## 2) Parametres fixes vs parametres variables

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```


*** =instructions

`ggplot2` et `diamonds` ont déjà été chargés. On reprend le dernier graphique créé, `p3`. 

**Modifiez** le code ci-contre pour que la **forme** des points corresponde à une étoile à 6 branches (voir l'antisèche ggplot2...)


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
success_msg("Oui! Vous pouvez soit définir les paramètres des geoms comme des constantes, ou bien les relier à des variables via le processus de mapping...")
```

*** =hint
Si vous définissez le paramètre comme une **constante**, vous devez le spécifier à l'**extérieur** de la fonction `aes()`...

--- type:MultipleChoiceExercise lang:r xp:50 skills:1 key:c256ad22fc
## 3) Esthetique globale ou de geom

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
        feedback_msgs = c("Non, c'est la couleur de **bordure** des boxplots qui dépend de `cut`",
                          "Non, la couleur des rugs dépend de `cut`!",
                          "Non, la couleur de bordure des boxplots dépend de `cut`...",
                          "Oui, bravo! Les paramètres renseignés **dans l'appel à `ggplot()`** valent pour l'**ensemble** des geoms..."))

```

*** =hint
Portez attention à l'endroit où sont définies les esthétiques (dans `ggplot()` ou dans un `geom_xxx()`?) et au paramètre considéré (couleur de bordure `color` ou couleur de remplissage `fill`?)


--- type:NormalExercise lang:r xp:50 skills:1 key:2c322c7227
## 4) Ajustement de la position


*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```


*** =instructions

`ggplot2` et `diamonds` ont déjà été chargés.

Examinez le code ci-contre et le graphique qu'il renvoie.

**Corrigez** ce code pour que les effectifs des différentes coupes apparaissent les **uns par dessus les autres** et que les hauteurs soient **normalisées**(paramètre `position`... consultez votre antisèche!!)



*** =sample_code
```{r}
p <- ggplot(diamonds, aes(x=carat))+
  geom_histogram(bins=10,aes(fill=cut))
plot(p)
```
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
success_msg("Oui! Avez-vous pris le temps pour bien comprendre comment le paramètre `position` modifiait la façon dont on peut lire le graphique?")
```

*** =hint
Le paramètre de position **n'est pas** une esthétique.

Vous pouvez voir les valeurs possibles pour ce paramètre sur votre **antisèche ggplot** (2ème page, "Position Adjustments")


--- type:NormalExercise lang:r xp:50 skills:1 key:b6f260cf51
## 5) Facettes


`ggplot2` et `diamonds` ont déjà été chargés.

*** =pre_exercise_code
```{r}
require(ggplot2)
data(diamonds)
```

*** =instructions

Complétez le code ci-contre pour produire différentes facettes du même graphique en fonction de la coupe des diamants (en ligne)

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
success_msg("Eh oui, bien joué! Les facettes , c'est trop de la boule!")
```

*** =hint
Avez-vous bien fait en sorte que les facettes soient en ligne et non en colonne dans l'appel à la fonction `facet_grid()`?


