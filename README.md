# Blind SQL injection with time delays and information retrieval
[RUS] Автоматизируем подбор blind sql, специально для Web_Security_Academy PortSwigger
Поиск  длинны пароля, а так же сам пароль от admin account .
И так, что мы имеем...
- Открытую уязвимость blind sql, проверка через подмену запроса (с содержанием печенек, в нашем случае на лабе, TrackingId=)

![изображение](https://user-images.githubusercontent.com/112577182/205280024-fd59c249-ed4e-4d84-b79c-851da865f73c.png)

- Все действия можно проводить в BurpSuite, но так как I dont have enough money for Burp Suite Edition
решено написать скрипт. Чтобы не переберать всё руками и наконец-то solved this f&c&k lab.

- Наша задача отсечь все ответы, которые после get запроса на сайт будут отвечать сразу же, так как в нашем случае иньекция использует pg_sleep(10)
Сами иньекции: 
1) Длинна пароля '%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
2) Сам пароль: '%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='a')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--
