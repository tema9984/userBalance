# UserBalance
В файле secret папка /secrets прописать свои данные для подключения к postgres
в файле keyApi прописан ключ от freecurrencyapi.net, можно оставить текущий или заменить на свой 
Если нужно указать пароль для редис то это можно сделать в файле secrets/redisPass
Конфигурации в config.json
```

```
Метод начисления средств на баланс. Принимает id пользователя и сколько средств зачислить.
``http://localhost:8081/replenish``
POST
body json: {"user_id":"uid1","balance":1314}

Метод списания средств с баланса. Принимает id пользователя и сколько средств списать.
http://localhost:8081/replenish
POST
body json: {"user_id":"uid1","balance":-1000}

Метод перевода средств от пользователя к пользователю. Принимает id пользователя с которого нужно списать средства, id пользователя которому должны зачислить средства, а также сумму.
http://localhost:8081/transaction
POST
body json: {"user1_id":"ad","user2_id":"add","amount":110}
user1 переводит средства user2

Метод получения текущего баланса пользователя. Принимает id пользователя. Баланс всегда в рублях.
Если этот параметр cureency присутствует, то конвертируем баланс пользователя с рубля на указанную валюту.
http://localhost:8081/balance?id=uid1S&currency=EUR
GET
id - ид пользователя
cureency - валюта для перевода

 метод получения списка транзакций с комментариями откуда и зачем были начислены/списаны средства с баланса
 http://localhost:8081/history?id=ad&sort=asc&column=amount&page=3
 GET
 id - ид пользователя
 sort - если указанно desc то сортировка по убыванию иначе по возрастанию 
 column - если amount то сортировка по сумме операции, если date то по дате операции
