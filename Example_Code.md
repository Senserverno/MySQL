#1
select distinct product.type,laptop.model,laptop.speed
from laptop,product
where type = 'laptop' and laptop.speed < all (select speed from pc)

#2
Select distinct product.maker,printer.price
from product
join printer 
on (product.model = printer.model)
where printer.color = 'y' and 
printer.price = (select min(price) from printer where color = 'y')

#3
select distinct maker
from product
join pc
on product.model = pc.model
where speed >= 750 and maker in
(select maker from product 
join laptop
on product.model = laptop.model
where speed >= 750)


#4
select model
from (select model,price
from pc
union 
select model,price
from laptop
union 
select model,price
from printer
) t1
where price = (select max(price)
from(select price
from pc
union 
select price
from laptop
union 
select price
from printer)t2)



select distinct product.maker from product
where model in (Select model from pc
where ram = (select min(ram) from pc) and speed = (select max(speed) from pc where ram = (select min(ram) from pc) )
)
and maker in (SELECT maker
FROM product
WHERE type='printer'
)





