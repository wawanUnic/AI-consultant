# MySQL database

### Database - port 7766, Admin - port 7767

Working not from root

Create a folder for work
```
mkdir mysql
cd mysql
```

Create a docker-compose.yml file
```
version: '3.9'
services:
  mysql-server:
    image: mysql/mysql-server
    container_name: mysql-server
    restart: always
    ports:
      - 7766:3306
  mysql-adminer:
    image: adminer
    container_name: mysql-adminer
    restart: always
    ports:
      - 7767:8080
networks:
  default:
    name: mysql
```

Run the container assembly:
```
sudo docker-compose up -d
```

Go into the container and create a user (enter the password that this container issued in the logs, for example, vD*_tp076%ubI#,7B1,MxoA017 - you can see this in dozzle)
```
sudo docker exec -it mysql-server mysql -u root -p
    ALTER USER 'root'@'localhost' IDENTIFIED BY 'new_password';
    FLUSH PRIVILEGES;
    EXIT
```

Re-enter the container with the new password and create a new user
```
sudo docker exec -it mysql-server mysql -u root -p
    CREATE USER 'master01'@'%' IDENTIFIED BY 'pass01';
    GRANT ALL PRIVILEGES ON . TO 'master01'@'%' WITH GRANT OPTION;
    FLUSH PRIVILEGES;
    EXIT
```

Using the adminer service (or the HeidiSQL program), create the n8n_base database, and in it the NeroBY_table1 table
```
CREATE TABLE `NeroBY_table1` (
	`id` INT NOT NULL AUTO_INCREMENT,
	`page` TEXT NULL,
	`value` TEXT NULL,
	PRIMARY KEY (`id`)
)
COLLATE='utf8mb4_0900_ai_ci'
;
SELECT `DEFAULT_COLLATION_NAME` FROM `information_schema`.`SCHEMATA` WHERE `SCHEMA_NAME`='n8n_base';
SHOW TABLE STATUS FROM `n8n_base`;
SHOW FUNCTION STATUS WHERE `Db`='n8n_base';
SHOW PROCEDURE STATUS WHERE `Db`='n8n_base';
SHOW TRIGGERS FROM `n8n_base`;
SELECT *, EVENT_SCHEMA AS `Db`, EVENT_NAME AS `Name` FROM information_schema.`EVENTS` WHERE `EVENT_SCHEMA`='n8n_base';
SELECT * FROM `information_schema`.`COLUMNS` WHERE TABLE_SCHEMA='n8n_base' AND TABLE_NAME='NeroBY_table1' ORDER BY ORDINAL_POSITION;
SHOW INDEXES FROM `NeroBY_table1` FROM `n8n_base`;
SELECT * FROM information_schema.REFERENTIAL_CONSTRAINTS WHERE   CONSTRAINT_SCHEMA='n8n_base'   AND TABLE_NAME='NeroBY_table1'   AND REFERENCED_TABLE_NAME IS NOT NULL;
SELECT * FROM information_schema.KEY_COLUMN_USAGE WHERE   TABLE_SCHEMA='n8n_base'   AND TABLE_NAME='NeroBY_table1'   AND REFERENCED_TABLE_NAME IS NOT NULL;
SHOW CREATE TABLE `n8n_base`.`NeroBY_table1`;
SELECT tc.CONSTRAINT_NAME, cc.CHECK_CLAUSE FROM `information_schema`.`CHECK_CONSTRAINTS` AS cc, `information_schema`.`TABLE_CONSTRAINTS` AS tc WHERE tc.CONSTRAINT_SCHEMA='n8n_base' AND tc.TABLE_NAME='NeroBY_table1' AND tc.CONSTRAINT_TYPE='CHECK' AND tc.CONSTRAINT_SCHEMA=cc.CONSTRAINT_SCHEMA AND tc.CONSTRAINT_NAME=cc.CONSTRAINT_NAME;
/* Открытие сеанса «server12» */
SHOW CREATE TABLE `n8n_base`.`NeroBY_table1`;
```

Copy this table under the name NeroBY_table2
```
SELECT 1 FROM `n8n_base`.`NeroBY_table2`;
/* Ошибка SQL (1146): Table 'n8n_base.NeroBY_table2' doesn't exist */
CREATE TABLE `n8n_base`.`NeroBY_table2` (
	`id` INT(10) NOT NULL AUTO_INCREMENT,
	`page` TEXT NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	`value` TEXT NULL DEFAULT NULL COLLATE 'utf8mb4_0900_ai_ci',
	PRIMARY KEY (`id`) USING BTREE
)
 COLLATE 'utf8mb4_0900_ai_ci' ENGINE=InnoDB ROW_FORMAT=Dynamic;
SHOW DATABASES;
SELECT `DEFAULT_COLLATION_NAME` FROM `information_schema`.`SCHEMATA` WHERE `SCHEMA_NAME`='n8n_base';
SHOW TABLE STATUS FROM `n8n_base`;
SHOW FUNCTION STATUS WHERE `Db`='n8n_base';
SHOW PROCEDURE STATUS WHERE `Db`='n8n_base';
SHOW TRIGGERS FROM `n8n_base`;
SELECT *, EVENT_SCHEMA AS `Db`, EVENT_NAME AS `Name` FROM information_schema.`EVENTS` WHERE `EVENT_SCHEMA`='n8n_base';
SELECT * FROM `information_schema`.`COLUMNS` WHERE TABLE_SCHEMA='n8n_base' AND TABLE_NAME='NeroBY_table1' ORDER BY ORDINAL_POSITION;
SHOW INDEXES FROM `NeroBY_table1` FROM `n8n_base`;
SELECT * FROM information_schema.REFERENTIAL_CONSTRAINTS WHERE   CONSTRAINT_SCHEMA='n8n_base'   AND TABLE_NAME='NeroBY_table1'   AND REFERENCED_TABLE_NAME IS NOT NULL;
SELECT * FROM information_schema.KEY_COLUMN_USAGE WHERE   TABLE_SCHEMA='n8n_base'   AND TABLE_NAME='NeroBY_table1'   AND REFERENCED_TABLE_NAME IS NOT NULL;
SHOW CREATE TABLE `n8n_base`.`NeroBY_table1`;
SELECT tc.CONSTRAINT_NAME, cc.CHECK_CLAUSE FROM `information_schema`.`CHECK_CONSTRAINTS` AS cc, `information_schema`.`TABLE_CONSTRAINTS` AS tc WHERE tc.CONSTRAINT_SCHEMA='n8n_base' AND tc.TABLE_NAME='NeroBY_table1' AND tc.CONSTRAINT_TYPE='CHECK' AND tc.CONSTRAINT_SCHEMA=cc.CONSTRAINT_SCHEMA AND tc.CONSTRAINT_NAME=cc.CONSTRAINT_NAME;
```
