 ## 1: How many users are there?

select count(id) from users;

Answer :
count(id)
50

 ###### 2: What are the 5 most expensive items?

select title,price from items order by price desc limit 5;

Answer:
title|price
Small Cotton Gloves|9984
Small Wooden Computer|9859
Awesome Granite Pants|9790
Sleek Wooden Hat|9390
Ergonomic Steel Car|9341

 ###### 3: What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)

select title,category,price from items where category='Books' order by price asc limit 1;

Answer:
title|category|price
Ergonomic Granite Chair|Books|1496

###### 4:  Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?

STEP1: 

select user_id from addresses where street='6439 Zetta Hills' and city='Willmouth' and state='WY';

Answer:
user_id
40

STEP2: select * from addresses where user_id ='40';

Answer:

id|user_id|street|city|state|zip

43|40|6439 Zetta Hills|Willmouth|WY|15029

44|40|54369 Wolff Forges|Lake Bryon|CA|31587

OR WE CAN USE THIS TO JOIN IT WITH NAME:
select * from addresses join users on user_id = users.id where user_id='40';

Answer:
43|40|6439 Zetta Hills|Willmouth|WY|15029|40|Corrine|Little|rubie_kovacek@grimes.net
44|40|54369 Wolff Forges|Lake Bryon|CA|31587|40|Corrine|Little|rubie_kovacek@grimes.net

###### 5:  Correct Virginie Mitchell's address to "New York, NY, 10108".

*  5a SELECT id,first_name, last_name from users where first_name='Virginie' and last_name='Mitchell';

Answer:

id|first_name|last_name

39|Virginie|Mitchell

* 5b SELECT * from addresses where user_id =39;

41|39|12263 Jake Crossing|Roxanehaven|NY|34705

42|39|83221 Mafalda Canyon|Bahringerland|WY|24028

 update addresses set city = 'New York', state = 'NY', zip = '10108' where user_id= 39;

*  5c SELECT * from addresses where user_id =39;

41|39|12263 Jake Crossing|New York|NY|10108

42|39|83221 Mafalda Canyon|New York|NY|10108

 ###### 6: How much would it cost to buy one of each tool?

SELECT sum(price) from items where category like '%tool%';

46477

###### 7:  How many total items did we sell?

SELECT SUM(quantity) from orders;

SUM(quantity)

2125

###### 8: How much was spent on books?

SELECT SUM(orders.quantity*items.price) as total_spent_on_books FROM orders JOIN items on orders.item_id = items.id WHERE items.category LIKE '%book%';

Answer:
total_spent_on_books
1081352

###### 9:  Simulate buying an item by inserting a User for yourself and an Order for that User

insert into orders (user_id, item_id, quantity, created_at) values (51, 15, 01, datetime());

Results shows as:

378|51|15|1|2017-03-06 22:11:10