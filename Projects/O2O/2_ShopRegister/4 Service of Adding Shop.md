# Service Implementation
## Implement `service.ShopService`
```java
public interface ShopService {
    ShopExecution addShop(Shop shop, File shopImg);
}
```

## Implement `service.impl.ShopServiceImpl`

```java
@Override
@Transactional
public ShopExecution addShop(Shop shop, File shopImg) {
    // check null value
    if (shop == null) {
        return new ShopExecution(ShopStateEnum.NULL_SHOP);
    }
    try{
        // initialize the Shop object(time and states related).
        shop.setEnableStatus(0);    // under review
        shop.setCreateTime(new Date());
        shop.setLastEditTime(new Date());
        int effectedNum = shopDao.insertShop(shop);
        if (effectedNum <= 0) {
            throw new RuntimeException("Fail to add shop ");
        } else {
            if (shopImg != null) {
                // save the image
                try{
                    addShopImg(shop, shopImg);
                } catch (Exception e) {
                    throw new RuntimeException("Fail to add shop img " + e.getMessage());
                }
                // update shop_img of the Shop object
                effectedNum = shopDao.updateShop(shop);
                if (effectedNum <= 0) {
                    throw new RuntimeException("Fail to update shop img ");
                }
            }
        }
    } catch (Exception e) {
        throw new RuntimeException("add Shop Error " + e.getMessage());
    }
    return new ShopExecution(ShopStateEnum.CHECK, shop);
}
```

Q: Why do we use `RuntimeException` here?
A: We want to stop the transaction when the exception occurs. Normal Exception won't stop the transaction. 

> Don't forget to add the `@Transactional` annotation!

Spring 事务 -- @Transactional的使用 - 简书
https://www.jianshu.com/p/befc2d73e487


Also, implement the helper function `addShopImg`
```java
private void addShopImg(Shop shop, File shopImg) {
    // get the relative address of the original shop image
    String dest = PathUtil.getShopImagePath(shop.getShopId());

    // generate and set the shop Image
    String shopImgAddr = ImageUtil.generateThumbnail(shopImg, dest);
    shop.setShopImg(shopImgAddr);
}
```
## Implement the separate `exception.ShopOperationException` class
```java
public class ShopOperationException extends RuntimeException{

    private static final long serialVersionUID = -5424163897092094031L;

    public ShopOperationException(String message) {
        super(message);
    }
}
```

Here we need the serialVersionUID in intellij, check this article to auto-generate it.

Intellij IDEA自动生成serialVersionUID【不需要插件】 - D调的华丽 - CSDN博客
https://blog.csdn.net/weixin_38553453/article/details/83340382

Then we replace all RuntimeException to ShopOperationException

## Implement the test
Implement `service.ShopServiceTest`
> Need to add @Service on top of ShopService to run test

Final Code
```java
public class ShopServiceTest extends BaseTest {
    @Autowired
    private ShopService shopService;
    
    @Test
    public void testAddShop() {
        Shop shop = new Shop();
        PersonInfo owner = new PersonInfo();
        Area area = new Area();
        ShopCategory shopCategory = new ShopCategory();
        owner.setUserId(1L);
        area.setAreaId(2);
        shopCategory.setShopCategoryId(1L);
        shop.setOwner(owner);
        shop.setArea(area);
        shop.setShopCategory(shopCategory);
        shop.setShopName("shop102");
        shop.setShopDesc("2");
        shop.setShopAddr("2");
        shop.setPhone("2");
        shop.setCreateTime(new Date());
        shop.setEnableStatus(ShopStateEnum.CHECK.getState());
        shop.setAdvice("1");
        File shopImg = new File("/Users/andaluo/Desktop/Projects" +
                "/O2O/src/main/resources/test/Veronica.jpg");
        ShopExecution se = shopService.addShop(shop, shopImg);
        Assert.assertEquals(ShopStateEnum.CHECK.getState(), se.getState());
    }
}
```

## Debug
1. The PathUtil defines the output path of the images. We should not use `/home/` here since we don't have the right to create files. We should change the path to `/Users/andaluo/Pictures/`. Don't forget the `'/'` in the end.

![4 Service of Adding Shop-2019-11-17-13-28-26.png](https://raw.githubusercontent.com/Luorinz/images/master/4%20Service%20of%20Adding%20Shop-2019-11-17-13-28-26.png)

2. The path of the watermark comes from the class path of the project, which is in the `target` files. Note that the path of plain running and JUnit is different.
`/Users/andaluo/Desktop/Projects/O2O/target/classes/`
`/Users/andaluo/Desktop/Projects/O2O/target/test-classes/test/watermark.jpg`

We have to manually copy and paste the `/classes/test/...` to `/test-classes/test/...`

3. When we are concatenating the complete path of destination, we have to change the current `basePath` to `PathUtil.getBasePath()`, otherwise there will be an error.

4. We should modify the `PathUtil.getShopImagePath`, delete the extra `/` at the head of the path, otherwise there will be duplicate `/`.