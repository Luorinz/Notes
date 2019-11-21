# Create `ShopDao`
1. Create a new interface called `ShopDao`, and define some APIs.
![O2O_shop-2019-11-10-15-25-11.png](https://raw.githubusercontent.com/Luorinz/images/master/O2O_shop-2019-11-10-15-25-11.png)

2. Configure the mapping of insertShop from MyBatis.

 ![O2O_shop-2019-11-10-15-50-47.png](https://raw.githubusercontent.com/Luorinz/images/master/O2O_shop-2019-11-10-15-50-47.png)

3. Implement the test. 
> Don't forget the foreign key and add the corresponding record first.

![O2O_shop-2019-11-10-15-51-26.png](https://raw.githubusercontent.com/Luorinz/images/master/O2O_shop-2019-11-10-15-51-26.png)

> Here we can use the internal tool of datasource form Intellij, which is super useful

![O2O_shop-2019-11-10-15-52-5.png](https://raw.githubusercontent.com/Luorinz/images/master/O2O_shop-2019-11-10-15-52-5.png)


4. Implement updateShop dao with dynamic SQL and write the tests.
![O2O_shop-2019-11-10-16-13-19.png](https://raw.githubusercontent.com/Luorinz/images/master/O2O_shop-2019-11-10-16-13-19.png)

> The set<> tag here actually means "SET" in SQL.

![O2O_shop-2019-11-10-16-13-56.png](https://raw.githubusercontent.com/Luorinz/images/master/O2O_shop-2019-11-10-16-13-56.png)
