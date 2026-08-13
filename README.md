# Цель: Ознакомление с основными аспектами безопасности, сети и хранилища в Kubernetes и получить практический опыт работы с соответствующими функциями и ресурсами.

<img width="1920" height="1022" alt="image" src="https://github.com/user-attachments/assets/24748474-15d5-452d-ac0b-51876da25d0d" />
|
<img width="431" height="581" alt="image" src="https://github.com/user-attachments/assets/bedf9e3c-72f1-4ee6-a22a-e3629ec84386" />

1. Создаём манифест rbac.yaml в нем описываем сервисный аккаунт. Далее создаем роль с доступом к ресурсам пода, а именно они указаны в verbs и привязываем аккаунт к роли через rolebinding и добавляем тестовый под.

2. Создаём манифест app.yaml c двумя репликами nginx

4. Создаём манифест services.yaml в нём три сервиса(NodePort, ClusterIP, LoadBalancer)

5. Создаём манифест storage.yaml создаём 4 ресурса:
   - PersistentVolume - Физическое объявление диска вот 1G места по пути /data/local-pv на узле доступное как хранилище
   - PersistentVolumeClaim - Приложение мне нужен 1G класс manual.Kubernetes сам ищет среди существующих PersistentVolume подходящий по размеру и классу
   - Тестовый под
   - StorageClass — не диск а рецепт автоматического изготовления дисков встроенный в minikube который сам создаёт PersistentVolume(не надо писать самый первый ресурс по сути kubernetes сам создаем новый диск если не находит подходящий)

Тест сервисного аккаунта:

1. Проверяем ресурс через сервисный аккаунт update и получаем yes как описывали в манифесте

2. Проверяем ресурс через сервисный аккаунт delete и получаем no delete запрещен

3. Пробуем get и получаем ответ

4. Пробуем delete (forbidden)

<img width="1491" height="257" alt="image" src="https://github.com/user-attachments/assets/2ef17d7c-4007-4de2-a241-62096e606d95" />

Тест сети:

1. Выводим полностью все сети и видим что loadBalancer не имеет внешнего айпи и в статусе пендинг

2. Curl тест получился неудачный, пропустил)

3. Чтоб loadbalancer получил externalip нужно в отдельном терминале поднять tunnel что я и продемонстрировал, выводим все сети и получаем externalip.

<img width="1446" height="691" alt="image" src="https://github.com/user-attachments/assets/364a8228-5910-4d40-8ac1-276cb7ac369c" />
|
<img width="1083" height="564" alt="image" src="https://github.com/user-attachments/assets/01fb0c4e-a6ce-46ee-a6b8-49ac60698d86" />


Тест хранилища:

1. Pod вывел hello from pv

2. Pv создан автоматически через fast

<img width="1517" height="296" alt="image" src="https://github.com/user-attachments/assets/026691e4-5f02-4969-913a-4b8889960ba5" />




