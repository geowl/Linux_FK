Ход выполнения:
1. Ход выполнения 1 пункта
![Ход выполнения 1 пункта](1.PNG)
2. Ход выполнения 2 пункта
![Ход выполения 2 пункта](2.PNG)
3. Подключить дополнительный репозиторий MySQL. Установить любой пакет
из этого репозитория:
    wget -c https://dev.mysql.com/get/mysql-apt-config_0.8.30-1_all.deb

    sudo dpkg -i mysql-apt-config_0.8.30-1_all.deb

    sudo apt update

    sudo apt install mysql-server
    

4.  wget -c http://ftp.ru.debian.org/debian/pool/main/n/nginx/nginx_1.22.1-9_amd64.deb

    sudo dpkg -i nginx_1.22.1-9_amd64.deb

    sudo apt-get install -f

    sudo dpkg -r nginx nginx-common

5.   Список команд из истории
![](5.PNG)
6. Диаграмма
![](linux_fk.drawio.png)

<h4>Работа с БД: </h4>


DROP database IF EXISTS HumanFriends;

CREATE database HumanFriends;

USE HumanFriends;


SHOW DATABASES;

+--------------------+

| Database           |

+--------------------+

| HumanFriends       |

| information_schema |

| mysql              |

| performance_schema |

| sys                |

+--------------------+

5 rows in set (0,00 sec)

DROP TABLE IF EXISTS HumanFriends;

CREATE TABLE HumanFriends (

    id_human_friend INT AUTO_INCREMENT PRIMARY KEY,

    type_human_friend VARCHAR(255)

);

DROP TABLE IF EXISTS Pets;

CREATE TABLE Pets (

    id_pet INT AUTO_INCREMENT PRIMARY KEY,

    type_pet VARCHAR(255),

    id_human_friend INT,

    FOREIGN KEY (id_human_friend) REFERENCES HumanFriends(id_human_friend)

);


DROP TABLE IF EXISTS PackAnimals;

CREATE TABLE PackAnimals (
    id_pack_animal INT AUTO_INCREMENT PRIMARY KEY,

    type_pack_animal VARCHAR(255),

    id_human_friend INT,

    FOREIGN KEY (id_human_friend) REFERENCES HumanFriends(id_human_friend)

);

DROP TABLE IF EXISTS Cats;

CREATE TABLE Cats (

    id_cat INT AUTO_INCREMENT PRIMARY KEY,

    name VARCHAR(255),

    birth_day DATE,

    commands TEXT,

    id_pet INT,

    FOREIGN KEY (id_pet) REFERENCES Pets(id_pet)

);

DROP TABLE IF EXISTS Dogs;

CREATE TABLE Dogs (

    id_dog INT AUTO_INCREMENT PRIMARY KEY,

    name VARCHAR(255),

    birth_day DATE,

    commands TEXT,

    id_pet INT,

    FOREIGN KEY (id_pet) REFERENCES Pets(id_pet)

);

DROP TABLE IF EXISTS Hamsters;

CREATE TABLE Hamsters (

    id_hamster INT AUTO_INCREMENT PRIMARY KEY,

    name VARCHAR(255),

    birth_day DATE,

    commands TEXT,

    id_pet INT,

    FOREIGN KEY (id_pet) REFERENCES Pets(id_pet)

);

DROP TABLE IF EXISTS Horses;

CREATE TABLE Horses (

    id_horse INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    birth_day DATE,
    commands TEXT,
    id_pack_animal INT,
    FOREIGN KEY (id_pack_animal) REFERENCES PackAnimals(id_pack_animal)
);

DROP TABLE IF EXISTS Camels;

CREATE TABLE Camels (
    
    id_camel INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    birth_day DATE,
    commands TEXT,
    id_pack_animal INT,
    FOREIGN KEY (id_pack_animal) REFERENCES PackAnimals(id_pack_animal)
);

DROP TABLE IF EXISTS Donkeys;

CREATE TABLE Donkeys (

    id_donkey INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(255),
    birth_day DATE,
    commands TEXT,
    id_pack_animal INT,
    FOREIGN KEY (id_pack_animal) REFERENCES PackAnimals(id_pack_animal)
);

SHOW TABLES;

# Вывод:

+------------------------+

| Tables_in_HumanFriends |

+------------------------+

| Camels                 |

| Cats                   |

| Dogs                   |

| Donkeys                |

| Hamsters               |

| Horses                 |

| HumanFriends           |

| PackAnimals            |

| Pets                   |

+------------------------+

<h5>Имена взяты рандомно с подборок</h5>

9 rows in set (0,00 sec)

INSERT INTO HumanFriends (type_human_friend) VALUES ('Pet'), ('PackAnimal');

INSERT INTO Pets (type_pet, id_human_friend) VALUES ('Cat', 1), ('Dog', 1), ('Hamster', 1);

INSERT INTO PackAnimals (type_pack_animal, id_human_friend) VALUES ('Horse', 2), ('Camel', 2), ('Donkey', 2);

INSERT INTO Cats (name, birth_day, commands, id_pet) VALUES ('Shadow', '2023-01-01', 'sit, jump', 1);

INSERT INTO Dogs (name, birth_day, commands, id_pet) VALUES ('Max', '2022-09-10', 'fetch, sit', 2);

INSERT INTO Hamsters (name, birth_day, commands, id_pet) VALUES ('Gizmo', '2023-08-20', 'run', 3);

INSERT INTO Horses (name, birth_day, commands, id_pack_animal) VALUES ('Storm', '2021-07-15', 'run', 2);

INSERT INTO Camels (name, birth_day, commands, id_pack_animal) VALUES ('Dune', '2022-06-30', 'carry', 2);

INSERT INTO Donkeys (name, birth_day, commands, id_pack_animal) VALUES ('Gus', '2021-02-14', 'carry', 3);


SELECT * FROM HumanFriends;

SELECT * FROM Pets;

SELECT * FROM PackAnimals;

SELECT * FROM Cats;

SELECT * FROM Dogs;

SELECT * FROM Hamsters;

SELECT * FROM Horses;

SELECT * FROM Camels;

SELECT * FROM Donkeys;

mysql> SELECT * FROM HumanFriends;

+-----------------+-------------------+

| id_human_friend | type_human_friend |

+-----------------+-------------------+

|               1 | Pet               |

|               2 | PackAnimal        |

+-----------------+-------------------+

2 rows in set (0,00 sec)


mysql> SELECT * FROM Pets;

+--------+----------+-----------------+

| id_pet | type_pet | id_human_friend |

+--------+----------+-----------------+

|      1 | Cat      |               1 |

|      2 | Dog      |               1 |

|      3 | Hamster  |               1 |

+--------+----------+-----------------+

3 rows in set (0,00 sec)


mysql> SELECT * FROM PackAnimals;

+----------------+------------------+-----------------+

| id_pack_animal | type_pack_animal | id_human_friend |

+----------------+------------------+-----------------+

|              1 | Horse            |               2 |

|              2 | Camel            |               2 |

|              3 | Donkey           |               2 |

+----------------+------------------+-----------------+

3 rows in set (0,00 sec)


mysql> SELECT * FROM Cats;

+--------+----------+------------+-----------+--------+

| id_cat | name     | birth_day  | commands  | id_pet |

+--------+----------+------------+-----------+--------+

|      1 | Shadow| 2023-01-01 | sit, jump |      1 |

+--------+----------+------------+-----------+--------+

1 row in set (0,00 sec)

mysql> SELECT * FROM Dogs;

+--------+------+------------+------------+--------+

| id_dog | name | birth_day  | commands   | id_pet |

+--------+------+------------+------------+--------+

|      1 | Max  | 2022-09-10 | fetch, sit |      2 |

+--------+------+------------+------------+--------+

1 row in set (0,00 sec)



mysql> SELECT * FROM Hamsters;

+------------+---------+------------+----------+--------+

| id_hamster | name    | birth_day  | commands | id_pet |

+------------+---------+------------+----------+--------+

|          1 | Gizmo | 2023-08-20 | run      |      3 |

+------------+---------+------------+----------+--------+

1 row in set (0,00 sec)



mysql> SELECT * FROM Horses;

+----------+---------+------------+----------+----------------+

| id_horse | name    | birth_day  | commands | id_pack_animal |

+----------+---------+------------+----------+----------------+

|        1 | Storm | 2021-07-15 | run      |              2 |

+----------+---------+------------+----------+----------------+

1 row in set (0,00 sec)



mysql> SELECT * FROM Camels;

+----------+-------+------------+----------+----------------+

| id_camel | name  | birth_day  | commands | id_pack_animal |

+----------+-------+------------+----------+----------------+

|        1 | Dune | 2022-06-30 | carry    |              2 |

+----------+-------+------------+----------+----------------+

1 row in set (0,00 sec)


mysql> SELECT * FROM Donkeys;

+-----------+--------+------------+----------+----------------+

| id_donkey | name   | birth_day  | commands | id_pack_animal |

+-----------+--------+------------+----------+----------------+

|         1 | Gus | 2021-02-14 | carry    |              3 |

+-----------+--------+------------+----------+----------------+

1 row in set (0,00 sec)

mysql> DELETE FROM Camels;

Query OK, 1 row affected (0,00 sec)

mysql> SELECT * FROM Camels;

Empty set (0,01 sec)

DROP TABLE IF EXISTS HorsesAndDonkeys;

CREATE TABLE HorsesAndDonkeys AS

SELECT id_horse AS id, name, birth_day, commands, 'Horse' AS type FROM Horses

UNION

SELECT id_donkey AS id, name, birth_day, commands, 'Donkey' AS type FROM Donkeys;

DROP TABLE IF EXISTS YoungAnimals;

CREATE TABLE YoungAnimals AS

SELECT id, name, birth_day, commands, type,

       TIMESTAMPDIFF(MONTH, birth_day, CURDATE()) AS age_in_months

FROM (

    SELECT id_cat AS id, name, birth_day, commands, 'Cat' AS type FROM Cats
    UNION ALL
    SELECT id_dog AS id, name, birth_day, commands, 'Dog' AS type FROM Dogs
    UNION ALL
    SELECT id_hamster AS id, name, birth_day, commands, 'Hamster' AS type FROM Hamsters
    UNION ALL
    SELECT id AS id, name, birth_day, commands, type FROM HorsesAndDonkeys
) AS AllAnimals

WHERE TIMESTAMPDIFF(MONTH, birth_day, CURDATE()) BETWEEN 12 AND 36;

DROP TABLE IF EXISTS AllAnimals;

CREATE TABLE AllAnimals AS

SELECT id_cat AS id, name, birth_day, commands, 'Cat' AS type FROM Cats

UNION

SELECT id_dog AS id, name, birth_day, commands, 'Dog' AS type FROM Dogs

UNION

SELECT id_hamster AS id, name, birth_day, commands, 'Hamster' AS type FROM 

Hamsters

UNION

SELECT id AS id, name, birth_day, commands, type FROM HorsesAndDonkeys

UNION

SELECT id AS id, name, birth_day, commands, type FROM YoungAnimals;

mysql> SELECT * FROM AllAnimals;

+----+----------+------------+------------+---------+

| id | name     | birth_day  | commands   | type    |

+----+----------+------------+------------+---------+

|  1 | Shadow    | 2023-01-01 | sit, jump  | Cat     |

|  1 | Max      | 2022-09-10 | fetch, sit | Dog     |

|  1 | Gizmo  | 2023-08-20 | run        | Hamster |

|  1 | Storm  | 2021-07-15 | run        | Horse   |

|  1 | Gus   | 2021-02-14 | carry      | Donkey  |

+----+----------+------------+------------+---------+

5 rows in set (0,00 sec)

