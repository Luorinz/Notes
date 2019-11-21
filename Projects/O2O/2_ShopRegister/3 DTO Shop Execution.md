# DTO and Shop Execution

## What is DTO?
java 深入了解DTO及如何使用DTO - 起风了 - CSDN博客
https://blog.csdn.net/liuchaoxuan/article/details/81175515

## Why do we use DTO in our project?
How do we know if we insert a shop record successfully?
Since we want to know the status of a insert operation, it's better we use another class rather than a `Shop` instance itself to represent the result of calling a service here.

## Implement `enums.ShopStateEnum`

```java
public enum ShopStateEnum {
    CHECK(0, "Under reviewing"),
    OFFLINE(-1, "Illegal Shop"),
    SUCCESS(1, "Successful Operated"),
    PASS(2, "Review passed"),
    INNER_ERROR(-1001, "System Error"),
    NULL_SHOPID(-1002, "NULL Error")
    ;

    private int state;
    private String stateInfo;

    private ShopStateEnum(int state, String stateInfo) {
        this.state = state;
        this.stateInfo = stateInfo;
    }

    /**
     * Given the state num, Get the corresponding ShopStateEnum object
     * @param state integer
     * @return a enum object.
     */
    public static ShopStateEnum stateOf(int state) {
        for (ShopStateEnum stateEnum: values()) {
            if (stateEnum.getState() == state) return stateEnum;
        }
        return null;
    }

    public int getState() {
        return state;
    }

    public String getStateInfo() {
        return stateInfo;
    }
```


## Implement `dto.ShopExecution`

```java
public class ShopExecution {
    // state of the result
    private int state;

    // the explanation of current state
    private String stateInfo;

    // the number of the results(Shop)
    private int count;

    // The Shop object we are operating on(Insert/Update/Delete)
    private Shop shop;

    // The Shop List we are operating on(Read)
    private List<Shop> shopList;

    // Default constructor
    public ShopExecution() {

    }

    // Constructor when the execution fails
    public ShopExecution(ShopStateEnum stateEnum) {
        this.state = stateEnum.getState();
        this.stateInfo = stateEnum.getStateInfo();
    }

    // Constructor when the execution successes(one shop)
    public ShopExecution(ShopStateEnum stateEnum, Shop shop) {
        this.state = stateEnum.getState();
        this.stateInfo = stateEnum.getStateInfo();
        this.shop = shop;
    }

    // Constructor when the execution successes(List of shops)
    public ShopExecution(ShopStateEnum stateEnum, List<Shop> shopList) {
        this.state = stateEnum.getState();
        this.stateInfo = stateEnum.getStateInfo();
        this.shopList = shopList;
    }
}
```
Then add the getters and setters.