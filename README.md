# Домашнее задание к занятию "`Введение в Terraform`" - `Мохов Антон`

### Цели задания

1. Установить и настроить Terrafrom.
2. Научиться использовать готовый код.

------

### Чек-лист готовности к домашнему заданию

1. Скачайте и установите **Terraform** версии >=1.12.0 . Приложите скриншот вывода команды ```terraform --version```.
2. Скачайте на свой ПК этот git-репозиторий. Исходный код для выполнения задания расположен в директории **01/src**.
3. Убедитесь, что в вашей ОС установлен docker.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. Репозиторий с ссылкой на зеркало для установки и настройки Terraform: [ссылка](https://github.com/netology-code/devops-materials).
2. Установка docker: [ссылка](https://docs.docker.com/engine/install/ubuntu/). 
------
### Внимание!! Обязательно предоставляем на проверку получившийся код в виде ссылки на ваш github-репозиторий!
------
<img width="1485" height="92" alt="image" src="https://github.com/user-attachments/assets/967f9302-6358-4971-bf38-29a4f9434b85" />


### Задание 1

1. Перейдите в каталог [**src**](https://github.com/netology-code/ter-homeworks/tree/main/01/src). Скачайте все необходимые зависимости, использованные в проекте. 
2. Изучите файл **.gitignore**. В каком terraform-файле, согласно этому .gitignore, допустимо сохранить личную, секретную информацию?(логины,пароли,ключи,токены итд)
3. Выполните код проекта. Найдите  в state-файле секретное содержимое созданного ресурса **random_password**, пришлите в качестве ответа конкретный ключ и его значение.
4. Раскомментируйте блок кода, примерно расположенный на строчках 29–42 файла **main.tf**.
Выполните команду ```terraform validate```. Объясните, в чём заключаются намеренно допущенные ошибки. Исправьте их.
5. Выполните код. В качестве ответа приложите: исправленный фрагмент кода и вывод команды ```docker ps```.
6. Замените имя docker-контейнера в блоке кода на ```hello_world```. Не перепутайте имя контейнера и имя образа. Мы всё ещё продолжаем использовать name = "nginx:latest". Выполните команду ```terraform apply -auto-approve```.
Объясните своими словами, в чём может быть опасность применения ключа  ```-auto-approve```. Догадайтесь или нагуглите зачем может пригодиться данный ключ? В качестве ответа дополнительно приложите вывод команды ```docker ps```.
8. Уничтожьте созданные ресурсы с помощью **terraform**. Убедитесь, что все ресурсы удалены. Приложите содержимое файла **terraform.tfstate**. 
9. Объясните, почему при этом не был удалён docker-образ **nginx:latest**. Ответ **ОБЯЗАТЕЛЬНО НАЙДИТЕ В ПРЕДОСТАВЛЕННОМ КОДЕ**, а затем **ОБЯЗАТЕЛЬНО ПОДКРЕПИТЕ** строчкой из документации [**terraform провайдера docker**](https://library.tf/providers/kreuzwerker/docker/latest).  (ищите в классификаторе resource docker_image )

### Решение

1. <img width="1681" height="320" alt="image" src="https://github.com/user-attachments/assets/71790fd9-13ee-4525-ad24-53882df236d8" />
<img width="1686" height="834" alt="image" src="https://github.com/user-attachments/assets/2f11311a-47f5-4feb-94e8-92a2dbc3626f" />

2. В файле personal.auto.tfvars.

3. <img width="1612" height="886" alt="image" src="https://github.com/user-attachments/assets/959efece-c6b2-4953-b3c4-36308d7febef" />
Ключ result: gc38cG9ay7wRzYnO

4. Отсутствует имя у ресурса docker_image; имя контейнера "1nginx" начинается с цифры; неверная ссылка на ресурс random_password (wrong name + wrong attribute case: resulT вместо result).
5.  <img width="1529" height="1021" alt="image" src="https://github.com/user-attachments/assets/8aab5cb7-29fa-4556-a717-5e4caa2dfdc4" />
<img width="1527" height="87" alt="image" src="https://github.com/user-attachments/assets/c2ff3fa4-06ee-4467-9eb9-0f312079d3a8" />
6. <img width="1852" height="722" alt="image" src="https://github.com/user-attachments/assets/19829650-2b87-4067-9811-0116573828b5" />
<img width="1482" height="141" alt="image" src="https://github.com/user-attachments/assets/934e6bdc-4053-4bf3-b592-5106d8cb9f7a" />
7. <img width="1681" height="1001" alt="image" src="https://github.com/user-attachments/assets/5660bf55-820e-42b1-9719-5e25103af62f" />
<img width="1050" height="69" alt="image" src="https://github.com/user-attachments/assets/2ff9d326-d602-4066-b182-75f71d0e0cf1" />


    <img width="1820" height="921" alt="image" src="https://github.com/user-attachments/assets/84447daa-a1ad-4efe-86ad-2ccd1045d7e8" />
8. Docker-образ nginx:latest не был удалён после terraform destroy, потому что в ресурсе docker_image в файле main.tf установлен параметр keep_locally = true. Согласно официальной документации провайдера kreuzwerker/docker (раздел resource docker_image, атрибут keep_locally): "If set to true, the image will not be removed from the local Docker daemon when the resource is destroyed." Этот параметр предназначен для сохранения образов локально, чтобы избежать повторной загрузки при следующем развёртывании инфраструктуры.







