#  Перенос музыки из ВК в ГуглМузыку

### Необходимые действия
1. Установиться nodejs версии [5] (https://nodejs.org/dist/latest-v5.x/) или выше
2. Получить access_token на сайте VK
3. Что бы было подключено мобильное устройство к гугл аккаунту

### Получение access_token от VK
1. Переходим по ссылке и разрешаем действия http://oauth.vk.com/authorize?client_id=5598052&scope=audio&%20redirect_uri=https://oauth.vk.com/blank.html&display=page&v=5.0&response_type=token
2. Вас перекинет на другую страницу
3. Скопировать токен из адресной строки

### Установка
1. npm i

### Использование
Есть 2 варианта использования:

1. Через email и пароль от google

    ```
    node index.js --token ACCESS_TOKEN --user_id USER_ID --email GOOGLE_EMAIL --password GOOGLE_PASSWORD --name_list NAME_PLAY_LIST
    ```

2. Через получение токена для google

    ```
    node index.js --token ACCESS_TOKEN --user_id USER_ID --google_token GOOGLE_TOKEN --name_list NAME_PLAY_LIST
    ```

### Описание флагов
* ACCESS_TOKEN - вставляем значение, полученное раньше
* USER_ID - айдишник пользователя, у которого берём музыку (не обязательно свой). Айдишник можно взять если перейти на кладку "музыка" в ВК. Он будет в дресной строке. Пример: https://vk.com/audios19811123 -> нам нужны только цифры
* GOOGLE_EMAIL - почта, под которой нужно авторизоваться
* GOOGLE_PASSWORD - пароль для авторизации
* GOOGLE_TOKEN - ниже описано как получить его
* NAME_PLAY_LIST - название плейлиста, куда нужно закачать музыку. P.S. Каждый раз он создаёт новый плейлист

### Получение токена от GOOGLE
Необходимо выполнить **POST** запрос
```JavaScript
    url: 'https://android.clients.google.com/auth'
    content-type: 'application/x-www-form-urlencoded'
    data: {
        accountType: 'HOSTED_OR_GOOGLE',
        Email: EMAIL,
        has_permission: '1',
        add_account: '1',
        Passwd: PASSWORD,
        service: "ac2dm",
        source: "android",
        androidId: 'c2ee043a809496a3',
        device_country: 'us',
        operatorCountry: 'us',
        lang: 'en',
        sdk_version: '17'
    }
```

В объекте ответа пудет поле Token=oauth2rt_1/...
Вот значение **oauth2rt_1/...** нам и понадобится.
