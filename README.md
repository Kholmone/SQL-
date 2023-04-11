# SQL-
Select ord.order_id, Concat(cus.first_name,' ', cus.last_name)AS 'customers', cus.city, cus.state,ord.order_date,
SUM(ite.quantity) as 'total units',
SUM(ite.quantity * ite.list_price) as 'revenue',
prod.product_name, cat.category_name,stor.store_name, CONCAT(staff.first_name, ' ',staff.last_name) AS 'sales_rep', br.brand_name
From sales.orders as ord
join sales.customers as cus
On ord.customer_id = cus.customer_id
join sales.order_items AS ite
on ord.order_id = ite.order_id
join production.products as prod
on ite.product_id = prod.product_id
JOIN production.categories as cat
ON prod.category_id = cat.category_id
JOIN sales.stores as stor
on ord.store_id = stor.store_id
JOIN sales.staffs as staff
on ord.staff_id = staff.staff_id
join production.brands AS br
on prod.brand_id = br.brand_id
group by 
	ord.order_id, Concat(cus.first_name,' ', cus.last_name), cus.city, cus.state,
	ord.order_date,prod.product_name, cat.category_name,stor.store_name,CONCAT(staff.first_name, ' ',staff.last_name),br.brand_name
