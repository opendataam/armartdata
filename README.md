# Данные о произведениях искусства, связанных с Арменией и хранящихся в российских музеях

Доступны два набора данных:
* Данные проекта [Артефакт](https://ar.culture.ru)
* Данные [Государственного каталога Музейного фонда Российской Федерации](https://opendata.mkrf.ru/opendata/7705851331-museum-exhibits)

В обоих случаях выборки представляют собой первично отфильтрованные данные, так или иначе связанные с Арменией. Связь устанавливалась по признаку наличия тех или иных ключевых слов, а также фамилий - [типичных армянских](https://github.com/sologuboved/arcult/blob/main/wiki_arm_typical_names.json) либо [известных, связанных с искусством](https://github.com/sologuboved/arcult/blob/main/wiki_arm_art_names.json).

Нужно учитывать, что данные не проходили тонкую обработку, поэтому в них могут присутствовать записи, не имеющие никакого отношения к Армении.

В каждом случае данные представлены:
- метаданными (файл json), описывающими те или иные экспонаты
- изображениями, представляющими эти экспонаты (публикуются через [HTTP-сервер](https://downloads.datacoon.app/))

## Данные "Артефакта"

Это небольшая коллекция экспонатов, которые обнаружились в этом проекте. [Метаданные](https://github.com/opendataam/armartdata/blob/master/arcult_metadata.json) в файле JSON структурированы как объект (словарь), где в качестве ключей ID, соответствующий автору, а в качестве значений - массивы (списки) его работ. Пример записи:
```json5
{
...
"abgaryan-n-yu": [
    {
      "id": "633d5f9d1d6c9387d194d731",
      "image": {
        "ctime": "2022-11-22T16:20:24.236Z",
        "defaultUrl": "attachment/original/637cf6c84edb837014c1b722-original.jpg",
        "depth": 8,
        "dims": {
          "h": 2403,
          "w": 1521
        },
        "format": "JPEG",
        "mime": "image/jpeg",
        "mtime": "2022-11-22T16:20:24.236Z",
        "oname": "нарине.jpg",
        "path": "attachment/original/637cf6c84edb837014c1b722-original.jpg",
        "size": 1906913
      },
      "slug": "shokoladnyy-dedushka-tayna-starogo-sunduka",
      "title": {
        "ru": "Шоколадный дедушка. Тайна старого сундука"
      }
    }
  ]
...
}
```
Каждой работе может соответствовать (в случае наличия в источнике) изображение. Изображения находятся по адресу [https://downloads.datacoon.app/arcult/](https://downloads.datacoon.app/arcult/). Ссылки на конкретные изображения строятся по шаблону:
```
https://downloads.datacoon.app/arcult/{ID_АВТОРА}/{SLUG_ИЗОБРАЖЕНИЯ}.{РАСШИРЕНИЕ}
```
Например:
```
https://downloads.datacoon.app/arcult/abgaryan-n-yu/shokoladnyy-dedushka-tayna-starogo-sunduka.jpg
```

## Данные Госкаталога
Эта коллекция больше: в ней более 8000 записей. Метаданные собраны в архивном файле [museum_exhibits.zip](https://github.com/opendataam/armartdata/blob/master/museum_exhibits.zip). В распакованном виде весят ~30МБ и представлены в формате JSON Lines. Описание структуры данных можно найти на [сайте источника](https://opendata.mkrf.ru/opendata/7705851331-museum-exhibits).

Соответствующие изображения находятся по адресу [https://downloads.datacoon.app/govcatalog/](https://downloads.datacoon.app/govcatalog/). Каталог разбит на папки, у каждой из которых в названии id музея, к которому относятся экспонаты.

В метаданных ID музея находится в поле `data.museum.id`. В поле `data.images` находится список ссылок на изображения экспоната, к которому относится запись. В поле `data.images.local_path` можно найти путь к конкретному файлу. Ссылка для скачивания будет строиться по шаблону:
```
https://downloads.datacoon.app/govcatalog/{DATA_IMAGES_LOCAL_PATH}
```
Например:
```
https://downloads.datacoon.app/govcatalog/2565/9881895_0.jpg
```



