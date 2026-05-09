create databae db1

create table stud(
id serial primary key,
name varchar(50) unique,
age int check (age>12),
mark int NOT NULL,
grade char(1),
time timestamp default now()
);


insert into stud (name,age,mark,grade) values('Arun',20,450,'A');
insert into stud (name,age,mark,grade) values('Dev',22,440,'A');
insert into stud (name,age,mark,grade) values('Neha',21,400,'B');

select * from stud;

update stud
set age=19
where name='Neha';

drop table stud;