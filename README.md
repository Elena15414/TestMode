[![Build status](https://ci.appveyor.com/api/projects/status/xmaem2dy7jltg7e0/branch/main?svg=true)](https://ci.appveyor.com/project/Elena15414/testmode/branch/main)


Задача №2: тестовый режим

Разработчики интернет-банка, изрядно поворчав, предоставили вам тестовый режим запуска целевого сервиса, в котором открыта программная возможность создания клиентов банка, чтобы вы могли протестировать хотя бы функцию входа.
Важно: ваша задача заключается в том, чтобы протестировать функцию входа через веб-интерфейс с использованием Selenide.
Для удобства вам предоставили документацию, которая описывает возможность программного создания клиентов банка через API. Вот дословно представленное ими описание:
Для создания клиента нужно делать запрос вида:

POST /api/system/users Content-Type: application/json

{ "login": "vasya", "password": "password", "status": "active" }

Возможные значения поля «Статус»:

«active» — пользователь активен,
«blocked» — пользователь заблокирован.
В случае успешного создания пользователя возвращается код 200.
При повторной передаче пользователя с таким же логином будет выполнена перезапись данных пользователя.
Мы уже проходили:

клиент-серверное взаимодействие,
HTTP-методы и коды ответов,
формат данных JSON,
REST-assured. Настоятельно рекомендуется ознакомиться с документацией и примерами на https://rest-assured.io/
Подключается обычным образом в Gradle:
testImplementation 'io.rest-assured:rest-assured:4.3.0' testImplementation 'com.google.code.gson:gson:2.8.6'

Библиотека Gson нужна для того, чтобы иметь возможность сериализовать Java-объекты в JSON. То есть мы не руками пишем JSON, а создаём data-классы, объекты которых и преобразуются в JSON.

Будет лучше, если вынести это в класс-генератор, который по требованию будет создавать рандомного пользователя, сохранять его через API и возвращать вам в тест.

Для активации этого тестового режима при запуске SUT нужно указать флаг -P:profile=test, то есть: java -jar app-ibank.jar -P:profile=test.

Важно: если вы не активируете тестовый режим, любые запросы на http://localhost:9999/api/system/users будут вам возвращать 404 Not Found.

Нужно самостоятельно изучить реакцию приложения на различные комбинации случаев:

наличие пользователя;
статус пользователя;
невалидный логин;
невалидный пароль.

Дополнительно: оцените время, которое затратили на автоматизацию, и время, за которое вы проверили бы те же сценарии вручную, используя для тестирования интерфейса браузер и Postman для доступа к открытому API.

время, затраченное на ручное тестирование (минут): x;

время, затраченное на автоматизацию (минут): y.
