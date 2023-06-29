Базы данных Васёв А.В.

## Задание 1
### Опишите не менее семи таблиц, из которых состоит база данных:

    какие данные хранятся в этих таблицах;
    какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.

### Приведите решение к следующему виду:

Сотрудники (

    идентификатор, первичный ключ, serial,
    фамилия varchar(50),
    ...
    идентификатор структурного подразделения, внешний ключ, integer).

```java
CREATE TABLE division_type (
id BIGSERIAL NOT NULL             		-- Первичный ключ
,name_division_type TEXT NOT NULL               -- Подразделение
);

ALTER TABLE division_type ADD CONSTRAINT pk_division_type$id PRIMARY KEY (id);

CREATE TABLE division (
id BIGSERIAL NOT NULL			        -- Первичный ключ
,name_division TEXT NOT NULL 			-- Наименование подразделения
,division_type_id BIGINT NOT NULL 	        -- ИД таблицы тип подразделения
);

ALTER TABLE division ADD CONSTRAINT pk_division$id PRIMARY KEY (id);
ALTER TABLE division ADD CONSTRAINT fk_division$division_type_id FOREIGN KEY (division_type_id) REFERENCES division_type(id);

CREATE TABLE branch (
id BIGSERIAL NOT NULL 			        -- Первичный ключ
,address TEXT NOT NULL 				-- Адрес
);

ALTER TABLE branch ADD CONSTRAINT pk_branch$id PRIMARY KEY (id);

CREATE TABLE project (
id BIGSERIAL NOT NULL			        -- Первичный ключ
,name_project TEXT NOT NULL 			-- Проект
);

ALTER TABLE project ADD CONSTRAINT pk_project$id PRIMARY KEY (id);

CREATE TABLE post (
id BIGSERIAL NOT NULL			       -- Первичный ключ
,name_post TEXT NOT NULL 		       -- Должность
);

ALTER TABLE post ADD CONSTRAINT pk_post$id PRIMARY KEY (id);

CREATE TABLE employee (
id BIGSERIAL NOT NULL 			       -- Первичный ключ
,fio TEXT NOT NULL 			       -- ФИО сотрудника
,post_id BIGINT NOT NULL		       -- ИД таблицы должность
,salary FLOAT NOT NULL 			       -- Оклад
,date_of_employment TIMESTAMP NOT NULL         -- Дата найма
,division_id BIGINT NOT NULL 		       -- ИД таблицы подразделение
,branch_id BIGINT NOT NULL 		       -- ИД таблицы филиал
);

ALTER TABLE employee ADD CONSTRAINT pk_employee$id PRIMARY KEY (id);
ALTER TABLE employee ADD CONSTRAINT fk_employee$post_id FOREIGN KEY (post_id) REFERENCES post(id);
ALTER TABLE employee ADD CONSTRAINT fk_employee$division_id FOREIGN KEY (division_id) REFERENCES division(id);
ALTER TABLE employee ADD CONSTRAINT fk_employee$branch_id FOREIGN KEY (branch_id) REFERENCES branch(id);

CREATE TABLE employee_project (
id BIGSERIAL NOT NULL 			      -- Первичный ключ
,employee_id BIGINT NOT NULL 		      -- ИД таблицы сотрудники
,project_id BIGINT NOT null		      -- ИД таблицы проекты
);

ALTER TABLE employee_project ADD CONSTRAINT pk_employee_project$id PRIMARY KEY (id);
ALTER TABLE employee_project ADD CONSTRAINT fk_employee_project$employee_id FOREIGN KEY (employee_id) REFERENCES employee(id);
ALTER TABLE employee_project ADD CONSTRAINT fk_employee_project$project_id FOREIGN KEY (project_id) REFERENCES project(id);
```

![alt text](https://github.com/rus42/DB/blob/main/Task_1.png)
