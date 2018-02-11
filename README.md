# SST Cloud

[![Travis](https://img.shields.io/travis/silentroach/sst-cloud.svg?style=flat-square&label=travis)](https://travis-ci.org/silentroach/sst-cloud)
[![Coveralls](https://img.shields.io/coveralls/silentroach/sst-cloud.svg?style=flat-square&label=coverage)](https://coveralls.io/r/silentroach/sst-cloud)

Модуль для работы с устройствами через [SST Cloud](https://www.sst-cloud.com).

---

Так сложилось, что ребята прекратили разработку сайта и приложения, [наружу болтается только API](https://api.sst-cloud.com/docs/). Модуль как раз для работы с ним.

У меня дома есть только система контроля протечек, так что поддержка есть только для него. Не стесняйтесь контрибьютить.

---

## Доступ к API

### Высокоуровневый

Пока в процессе, сорян

### Низкоуровневый

```javascript
// импортируем модуль для работы с API
const {API} = require('sst-cloud');

// для работы нужен ключ сессии, который пробрасываем в конструктор
const api = new API(
	// ключ сессии можно получить через авторизацию
	await API.login(/* email */, /* password */)
);

// все остальные методы для получения информации асинхронны
// и возвращают в ответ ту информацию и в том виде, что ее вернул API,
// без дополнительной обработки
const userInfo = await api.user();

console.log(userInfo);
// { pk: 123,
//   username: 'xxx',
//   email: 'xxx',
//   profile: { ... }
// }
```

Методы API (автогенерировано, но генератор пока стыдно выкладывать):

`(static)` `API.login(String email, String password)` ~> `String`

Авторизация ~> Идентификатор сессии

`.user()`

Получение информации о текущем пользователе

`.houses()`

Список домов

`.houseById(Number houseId)`

Информация о доме по его идентификатору

`.networks(Number houseId)`

Список сетей в доме

`.networkById(Number houseId, Number networkId)`

Информация о сети по ее идентификатору

`.devices(Number houseId)`

Список устройств в доме

`.deviceById(Number houseId, Number deviceId)`

Информация об устройстве по его идентификатору

`.sensors(Number houseId, Number deviceId)`

Список беспроводных датчиков, зарегистрированных в устройстве

`.counters(Number houseId, Number deviceId)`

Информация о счетчиках, зарегистрированных на устройстве

