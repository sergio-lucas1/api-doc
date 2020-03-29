---
tags: [Survey]
---

# Enter screen

![](../../assets/images/screens/enter.png)

На данном экране у пользователя есть возможность ввести/вставить [код анкеты(survey code)](../glossary/survey.md?survey-code), который состоит из 7 символов(включают только буквы и цифры).

### Actions:
- Enter code - 

**Состояния:**

1. В момент проверки/валидации блочим ui, показываем лоадер
2. Если код неверный выводим сообщение ошибки.
3. Если код верный. [Ответ с сервера](../../reference/survey/UXReality-Respondent-Android.v1.yaml/paths/~1GetProjectInfo/get)
4. На следующем этапе идет получение [данных по анкете](../../reference/survey/UXReality-Respondent-Android.v1.yaml/paths/~1GetQuestMetadata/get) и инициализация самой анкеты
4. После успешной валидации кода, запрашиваем [permissions](./app-permissions.md) необходимые для дальнейшей работы с приложением
5. Если пользователь отклонил permissions - выводим ошибку, в другом случае переходим к первому вопросу с анкеты
6. 
5. ~~Если пользователь отклонил permissions - выводим ошибку, в другом случае переходим на[ следующий экран](./video.md)~~
