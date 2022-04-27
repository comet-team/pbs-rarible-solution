Wish Graph
===
**Рекомендуем NFT на основе графа владения**

Мобильное приложение на Android (Kotlin):
https://github.com/comet-team/wish-graph-mobile

Фронт (Node.js):
https://github.com/comet-team/wish-graph-web

Сервер (Python + Flask):
https://github.com/comet-team/wish-graph-model

Сайт крутится тут:
http://5.63.159.42:3000/

Приложение можно скачать тут: 

Содержание
---
+ [**Проблема**](#проблема)  
+ [**Решение**](#решение) 
+ [**Архитектура**](#архитектура) 
+ [**Демонстрация решения**](#демонстрация-решения)
+ [**Направления дальнейшего развития**](#направления-дальнейшего-развития)  

Проблема
---
Из-за резко возросшей популярности NFT рынок переполнен токенами самых разных направлений. Мы задумались над инструментом, который мог бы среди огромного разнообразия NFT выделить наиболее интересные для пользователя.  

Решение
---

На решение нас натолкнула [теория 6-ти рукопожатий](https://ru.wikipedia.org/wiki/Теория_шести_рукопожатий), согласно которой любые два человека на Земле разделены не более чем пятью уровнями общих знакомых. Поэтому мы решили разработать рекомендательную систему, которая будет основана на механизме NFT-знакомств, где знакомство - это факт владения NFT одного автора. С использованием Rarible Protocol мы сможем находить эти знакомства и строить граф для каждого конкретного пользователя. На основе анализа этого графа и будут составляться рекомендации.

К этой идее мы решили подойти с трёх сторон:
+ Сервер, который публикует соответствующий API => техническая реализация идея и основной продукт
+ Мобильное приложение, которое демонстрирует работу API (по адресу кошелька выводит рекомендованные NFT) => реклама api и будущий маркетплейс
+ Сайт, на котором можно посмотреть визуализированный граф, потыкать и посмотреть рекомендации => fan для пользователя

### Причины выбора решения
+ Математический бэкграунд участников команды
+ Более стандартные подходы к рекомендациям уже реализованы (например, на основе просмотров или покупок) 
+ Это может стать инструментом для улучшения социального взаимодействия между пользователями в web3.0 => основа для социальной сети по аналогии с Linkedin
+ Идея предполагает плотное использование Rarible Protocol
+ Перспективы интеграции с NFT-маркетплейсами (в частности, Rarible)
+ Хотелось предложить новую для сферы идею 

### Рынок и ЦА
Проект нацелен на улучшение пользовательского опыта в NFT маркетпейсах, что положительно скажется на их монетизации.
Наш проект мы сможем предложить как крупным маркетплейсам так и связанными с ними стартапам.

### Требования к продукту
+ Отсутвие комиссии за использование на данном этапе
+ Удобное в использовании API
+ Хорошая документация 
+ Сайт и приложение
  + Простой продукт с минимумом кнопок :)
  + Отсутствие криптовалютных терминов 
  + Лаконичный и гибкий дизайн

Архитектура
---
<img src="https://github.com/comet-team/wish-graph-description/blob/main/img/Architecture.png" width="500" />

Принцип построения графа знакомств

<img src="https://github.com/comet-team/wish-graph-description/blob/main/img/API%20structure.png" width="300" />

### API
На данный момент сервер предоставляет только один API эндпоинт для получения списка рекомендованных NFT:

### GET http://5.63.159.42:8081/user_recommend/<wallet_token>
Возвращает список NFT которые можно рекомендовать пользователю

**Parameters**

|          Name | Required |  Type   | Description                                                                                                                                                           |
| -------------:|:--------:|:-------:| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|     `wallet_token` | required | string  | Токен кошелька пользователя.                                                                     |                                                            |

**Response**

```
[
    {
        "account": string,
        "nft": [
            {
                "id": string,
                "url": string
            },
            ...
        ],
        "value": double
    }
]
```

### Интеграция с Rarible Protocol
Сервер использует следующие эндпоинты, предоставляемые API от Rarible:
+ https://api.rarible.com/protocol/v0.1/ethereum/nft/items/byCreator
+ https://api.rarible.org/v0.1/items/

Демонстрация решения
---
[Сайт](https://disk.yandex.ru/i/3QMd8iBouwYQlw)

[Приложение](https://disk.yandex.ru/i/iVbhsky4qRDbBg)

Направления дальнейшего развития
---
Идеи развития проекта:
+ Оптимизировать алгоритмы поиска наиболее релевантных знакомых, чтобы API работала быстрее
+ Расширить варианты рекомендаций. Например, рекомендовать не только конкретные NFT, а ещё и художников
+ Развить созданную API в полноценный аналитический инструмент
+ Добавить привязку рекомендованных NFT к конкретным пользователям - основа для вариации на тему социальных сетей
+ Подключить кастодиальный кошелёк вместо ручного ввода адреса кошелька
+ Добавить в сайт и приложение возможнось покупать nft (доделать базовый функционал маркетплейса)
+ Провести тестирование на разработчиках и пользователях 
