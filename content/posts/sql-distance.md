---
title: "Расстояние между двумя координатами"
date: 2017-04-23T10:46:09+03:00
tags: ["кодим"]
draft: false
---
{{< abzac />}}Доброго времени суток, коллеги и гости. Как то понадобилось мне узнать расстояние между двумя географическими координатами, причем наиболее легким и незамысловатым путем, еще и запросом в MySQL.
<!--more-->
{{< abzac />}}Долго бродил я по сети натыкаясь на разные рецепты. И наткнулся на официальный мануал от Google(сейчас уже ссылку не найду), который дал мне вот такую формулу:
{{< codecaption lang="sql" title="SQL" >}}
SELECT 
    id,
    (6371 *
        acos(
            cos(radians(37)) *
            cos(radians(lat)) *
            cos(radians(lng) - radians(-122)) +
            sin(radians(37)) *
            sin(radians(lat))
        )
    ) AS distance
FROM markers
HAVING distance < 25
ORDER BY distance
LIMIT 0,20;
{{< /codecaption >}}

{{< abzac />}} В этом SQL-запросе находится 20 ближайших локаций в радиусе 25 километров для координаты (37, -122). Если необходимо искать в милях, замените в запросе 6371 на 3959. Такой запрос дает относительно неплохую точность, позволяя при этом не углубляться более сложными методами, такими как например Point в MySQL.
Вот такой короткий пост в этом году, надеюсь рецепт этот поможет многим!
Спасибо за внимание! Спишемся.
