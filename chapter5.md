---
title       : graphR 5 - Cartes
description : Ces exercices visent a montrer les fonctions de ggmap, petit cousin de ggplot2, vous permet de créer des cartes...

--- type:NormalExercise lang:r xp:50 skills:1 key:5ce37fe522
## 1) Fond de carte


**** =sample_code
```{r}
require(ggmap)

lyon=c(lat=45.759723, lon=4.842223)

lyon_map=get_map(location=lyon,zoom=13)
ggmap(lyon_map)
```

*** = instructions

**Complétez** le code ci-contre 


*** =solution
```{r}
require(ggmap)

lyon=c(lat=45.759723, lon=4.842223)

lyon_map=get_map(location=lyon,zoom=13)
ggmap(lyon_map)

lyon_map_2=get_map(location=lyon,zoom=13, 
                   maptype="satellite")
ggmap(lyon_map_2)

lyon_map_3=get_map(location=lyon,zoom=13, 
                   maptype="watercolor", source="stamen")
ggmap(lyon_map_3)
```

*** =sct
```{r}
test_object("lyon")
```


