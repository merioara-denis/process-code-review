# Процесс Code review в команде
### Тезисы
- Code review это всегда стресс для автора.
- Автор гораздо легче воспринимает сообщение о ошибке от компьютера.
- У ривьера нет цели оскорбить или самоутвердиться в рамках code review, передача информации без интонации голоса может казаться грубой.
### Материалы
- [Code Review – зачем и как использовать в команде?](https://habr.com/ru/articles/581354/)
- [Пулл-реквесты с эмпатией](https://habr.com/ru/companies/mobileup/articles/340456)
- [Code review по-человечески (часть 1)](https://habr.com/ru/articles/340550/)
- [Code review по-человечески (часть 2)](https://habr.com/ru/articles/342244)
### Цель проведения code review
- Понижение взаимозаменяемость разработчиков (Bus Factor) в проекте.
- Понижение порога входа в проект.
- Выявление дефектов и недоработок.
- Контроль соответствия согласованным правилам команды *(читаемость, возможность развития и удобство работы с кодом)*.
- Повышение квалификации команды.
- Повышение взаимодействия между участниками команды.
- Выявление и автоматизация рутинных проверок *(опечатки, форматирование, требования к написанию кода, циклические зависимость, декомпозиция, тестирование и т.д.)*.
### Список проблем на которое нацелено Code review
- Возможность развития проекта, сохранение гибкости и высокой производительности.
- Контроль качества и согласования реализации.
- Порционное внесение изменений. 
- Снижения уровня стресса при работе в проекте.
- Взаимозаменяемость разработчиков в проекте.
### Решение
- Интеграция чек листов.
	- Чек лист для разработчика
	- Чек лист для ревьювера
- Согласование границ ответственности.
	- После вливания вся команда принимает на себя ответственность поддерживать, развивать и устранять дефекты.
	- Ривьере имеет право вынести решение на согласование ITL (создаётся встреча и добавляется обоснование критичность в рамках PR).
- Автоматизируем всё что можно автоматизировать для уменьшения количества предложений.
### Чек лист для разработчика перед отправкой на ревью:
- Проверить, что размер запроса на слияние не превышает 400 строк.
- Проверить соответствие статическому анализу (статический анализ проверяет опечатки, форматирование, валидацию кода, unit тесты, сборку приложения).
- Проверить, что ревьюверу достаточно информации, в задаче прикреплена ссылка на требования и дизайн, все договорённость внесены в требования.
- Проверить, что реализация соответствует всем указанным в исходной задаче условиям.
- Протестировать задачу локально и убедиться, что она работает, как нужно.    
- Подготовить описание для ревьювера, если какой-то информации в задаче не хватает.    
- Проверить, нужны ли какие-то комментарии в самом коде и добавить при необходимости.
### Чек лист для ревьювера:
- Ознакомиться и понять цель и суть задачи (ознакомиться с требованиями, дизайнам).
- Проверить общую архитектуру и подход к решению (соответствия project-design).
- Проверить реализацию и работоспособность.
- Проверить мелкие детали (имена функций и переменных и т.д.).
- Проверить наличие тестов и документации по необходимости.

### Итоги:
- Любой разработчик (вне зависимость от позиции) должен набрать минимум 2 подтверждения от участников команды.
- При добавление предложения по улучшению обязательно добавлять обоснование в виде ссылки на статью и/или правило в рамках команды.
- При желание предложить аналог реализации присылать запрос на изменение текущего кода с обоснованием почему это улучшит реализацию.

### Требования к запросу на слияние
- Наименование запроса на слияние должно содержать `тип`, `номер задачи` и `название задачи` в формате `{Тип}/{Номер задачи}: {Название задачи}`:
	- `Bugfix/PPTS-123: Исправление отображение даты в комментариях` - для задач на устранение дефектов
	- `Feature/PPTS-123: Разработка редактирования ссылок` - для задач на разработку или изменение функциональности
	- `Subtask/PPTS-123: Добавить отображения типа ссылки` - для ветки разработки в рамках фичи
	*Для ответственных очень важно понимать какая задача приоритетнее и не терять время на выявление приоритетов (по Bugfix есть SLA от клиентов, по Subtask может блокировать разработчика и Feature ждёт тестирование)*.
- В случае обнаружения необходимость доработки длительностью более 1 часа заводиться дополнительная задача на устранение технического долга и к этой задаче разработчик возвращается после завершения слияния (при условии что это не блокирует коллег). Номер задачи указывает в комментариях `TODO` в коде (формат: `TODO: PPTS-123 Добавить покрытие тестами`).
- Один запрос на слияние должен содержать решение одной единственной задачи или часть задачи, допускается один запрос на несколько задач если они мелкие **и** связаны между собой. 
- Все предложения должны быть решены инициатором PR и подтверждены ревьюерам, допускается поставить встречу и согласовать голосом принятие общего решения. При конфликте интересов вопрос должен быть вынесен на ITL команды.
- В рамках запроса на слияние **запрещается внесение изменений** в чужой задаче.
- Рекомендуется: В рамках PR добавить краткое описание почему задача решалась данным способом для внесения ясности в рамках рассмотрения запроса. 
  *(к примеру: цветовая гамма UIKIT расширена нестандартными токенами для поддержки работоспособность и данное решение согласовано с Иванов Иван Иванович)*.
- Чётко формулировать предложение к примеру `Предлагаю заменить map и filter на reduce так как это уменьшит алгоритмическую сложность, увеличит читаемость`.
- Избегать предложений с непонятными формулировками типа `Аналогично`, `Тут тоже`, `Надо прорефакторить`.

### Конечная цель к которой стремится компания
- Возможность переписать продукт **не будет**.
- Остановка разработки до получения идеального решения неприемлемо, допускается формирования технического долга с устранением при следующей итерации
- Продукт должен развиваться и промежуточные решения не должны влиять на его развитие и срок его жизни, любой костыль или стратегическое решение не должны препятствовать возвращению к целевому решению.
- Устранение технического долга необходимо проводить постоянно, накапливание критического технического долга неприемлемо.
