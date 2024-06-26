create table salesman
    -> (
    -> Salesman_id int primary key,
    -> Name varchar(20),
    -> City varchar(20),
    -> Comission decimal(10,2)
    -> );
Query OK, 0 rows affected (0.04 sec)
mysql> desc salesman;

mysql> create table Customer
    -> (
    -> Customer_id int primary key,
    -> Cust_name varchar(20),
    -> City varchar(20),
    -> Grade int,
    -> Salesman_id int,
    -> foreign key(Salesman_id) references salesman(Salesman_id)
    -> );
Query OK, 0 rows affected (0.09 sec)
mysql> desc Customer;

mysql> create table Orders
    -> (
    -> Order_no int primary key,
    -> Purchase_amt decimal(10,2),
    -> Order_date date,
    -> Customer_id int,
    -> Salesman_id int,
| | | | | |

    -> foreign key(Customer_id) references Customer(Customer_id),
    -> foreign key(Salesman_id) references salesman(Salesman_id)
    -> );
Query OK, 0 rows affected (0.07 sec)
mysql> desc Orders;

insert into salesman values(100,"Chaitu","Vijayawada",0.15);
Query OK, 1 row affected (0.02 sec)
mysql> insert into salesman values(101,"Bujji","Bengaluru",0.25);
Query OK, 1 row affected (0.01 sec)
mysql> insert into salesman values(102,"Mani","Vijayawada",0.29);
Query OK, 1 row affected (0.01 sec)
mysql> insert into salesman values(103,"Dhanush","Bengaluru",0.19);
Query OK, 1 row affected (0.01 sec)
mysql> insert into salesman values(104,"Piyush","Chapra",0.22);
Query OK, 1 row affected (0.01 sec)
mysql> select *from salesman;


insert into Customer values(200,"Cariappa","Coorg",5,100);
Query OK, 1 row affected (0.02 sec)
mysql> insert into Customer values(201,"Mary","Bengaluru",9,101);
Query OK, 1 row affected (0.02 sec)
0.15 |
0.25 |
0.29 |
0.19 |
0.22 |

mysql> insert into Customer values(202,"Chellu","Bengaluru",11,102);
Query OK, 1 row affected (0.01 sec)
mysql> insert into Customer values(203,"Sam","Banglore",7,100);
Query OK, 1 row affected (0.02 sec)
mysql> insert into Customer values(204,"Johnwick","Bellary",3,101);
Query OK, 1 row affected (0.01 sec)
mysql> select *from Customer;


insert into Orders values(300,500.15,'2024-02-14',200,100);
Query OK, 1 row affected (0.01 sec)
mysql> insert into Orders values(301,750.55,'2024-02-26',201,100);
Query OK, 1 row affected (0.01 sec)
mysql> insert into Orders values(302,5000.55,'2024-02-29',202,101);
Query OK, 1 row affected (0.01 sec)
mysql> insert into Orders values(303,50.55,'2024-03-01',203,102);
Query OK, 1 row affected (0.01 sec)
mysql> insert into Orders values(304,4750.55,'2024-03-02',204,103);
Query OK, 1 row affected (0.02 sec)
mysql> insert into Orders values(305,4750.55,'2024-03-02',204,104);
Query OK, 1 row affected (0.01 sec)
mysql> select *from Orders;


select count(Customer_id) as Customers_Above_Avg_Grade from Customer where Grade>(select avg(Grade) from Customer where City="Bengaluru")
-> ;


select count(Customer_id) as Customers_Above_Avg_Grade from Customer where Grade>(select avg(Grade) from Customer where City="Banglore");


select s.Name,s.Salesman_id,count(*) as Customer_count from salesman s inner join Customer c on s.Salesman_id=c.Salesman_id group by s.Name,s.Salesma
n_id having count(*)>1;

commit;

(select 'Salesman With Customers' as Status,s.Salesman_id,s.Name,s.City from salesman s inner join Customer c on s.Salesman_id=c.Salesman_id)
-> union
    -> (select 'Salesman Without Customer' as Status,s.Salesman_id,s.Name,s.City
from salesman s left join Customer c on s.Salesman_id=c.Salesman_id where c
.Customer_id is null);


delete from Orders where Salesman_id=100;
select *from Orders;


delete from Customer where Salesman_id=100;
select *from Customer;

delete from salesman where Salesman_id=100;
Query OK, 1 row affected (0.01 sec)
mysql> select *from salesman;



