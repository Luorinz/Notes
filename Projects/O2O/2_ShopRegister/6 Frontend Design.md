# Front-end design
## SUI Mobile
1. Description
SUI Mobile 是一套基于 Framework7 开发的UI库。它非常轻量、精美，只需要引入我们的CDN文件就可以使用，并且能兼容到 iOS 6.0+ 和 Android 4.0+，非常适合开发跨平台Web App。

轻量的UI库
SUI Mobile 非常轻量，核心库压缩Gzip后的JS、CSS网络传输体积总共只有52K，却提供了20+个常用的组件。

对于只有HTML&CSS的组件，你只需要复制HTML代码既可以使用。他的大部分JS组件都是独立的 Zepto 插件，并且提供了 Zepto/jQuery 风格的API，你将会非常熟悉这种方式。

Link: http://m.sui.taobao.org/

2. Directly copy the source code from the demo http://m.sui.taobao.org/demos/, and change the `css` and `js` to 
```html
<link rel="stylesheet" href="//g.alicdn.com/msui/sm/0.6.2/css/sm.min.css">
<link rel="stylesheet" href="//g.alicdn.com/msui/sm/0.6.2/css/sm-extend.min.css">


<script type='text/javascript' src='//g.alicdn.com/sj/lib/zepto/zepto.min.js' charset='utf-8'></script>
<script type='text/javascript' src='//g.alicdn.com/msui/sm/0.6.2/js/sm.min.js' charset='utf-8'></script>
<script type='text/javascript' src='//g.alicdn.com/msui/sm/0.6.2/js/sm-extend.min.js' charset='utf-8'></script>
```
from tutorial http://m.sui.taobao.org/getting-started/.

3. Modify the code to meet our needs.
eg. Normal case
```html
<!-- Shop name -->
<li>
    <div class="item-content">
        <div class="item-media"><i class="icon icon-form-name"></i></div>
        <div class="item-inner">
            <div class="item-title label">Name</div>
            <div class="item-input">
                <input type="text" id="shop-name" placeholder="Shop Name">
            </div>
        </div>
    </div>
</li>
```
eg. text area
```html
<!--Shop description, text area-->
<li class="align-top">
    <div class="item-content">
        <div class="item-media"><i class="icon icon-form-comment"></i></div>
        <div class="item-inner">
            <div class="item-title label">Description</div>
            <div class="item-input">
                <textarea id="shop-desc" placeholder="Description"></textarea>
            </div>
        </div>
    </div>
</li>
```
## Back-end modification
1. Modify the file path, move `index.html` to `WEB-INF/html/shop/shopoperation.html`. In this way we cannot visit the inner resource directly.

2. Implement `web.shopadmin.ShopAdminController`
```java
@Controller
@RequestMapping(value="shopadmin", method={RequestMethod.GET})
public class ShopAdminController {
    /**
     * Map the address shopadmin/shopoperation to shop/shopoperation.html
     * Since we have already defined the prefix and suffix in Spring,
     * We only need to return a plain text.
     * @return the router destination
     */
    @RequestMapping(value = "/shopoperation")
    public String shopOperation() {
        return "shop/shopoperation";
    }
}
``` 
Test the router at `http://localhost:8080/shopadmin/shopoperation`. It's a bit different from Eclipse. It's the `ViewResolver` that defines the mapping to the `WEB-INF`.

## JavaScript Design
1. Modify `submit` and `return` in the `shopoperation.html`.

```html
<div class="col-50"><a href="#" class="button button-big button-fill button-danger">Back</a></div>
<div class="col-50"><a href="#" class="button button-big button-fill button-success" id="submit">Submit</a>
```

2. Implement `resources/js/shooperation.js`.

```js
$(function() {
    var initUrl = '/o2o/shopadmin/getshopinitinfo';
    var registerShopUrl = '/o2o/shopadmin/registershop';
    getShopInintInfo();
    alert(initUrl); //test
    function getShopInintInfo() {
        $.getJSON(initUrl, function(data){
            if (data.success) {
                var tempHtml = '';
                var tempAreaHtml= '';
                data.shopCategoryList.map(function (item, index) {
                    tempHtml += '<option data-id=">' + item.shopCategoryId + '">'
                    + item.shopCategoryName + '</option>';
                });
                data.areaList.map(function(item, index) {
                    tempAreaHtml += '<option data-id="' + item.areaId + '">' + item.areaName
                    + '</option>';
                });

                $('#shop-category').html(tempHtml);
                $('#area').html(tempAreaHtml);
            }

        });
        $('#submit').click(function () {
            var shop = {};
            shop.shopName = $('#shop-name').val();
            shop.shopAddr = $('#shop-addr').val();
            shop.phone = $('#shop-phone').val();
            shop.shopDesc = $('#shop-desc').val();
            shop.shopCategory = {
                shopCategoryId: $('#shop-category').find('option').not(function () {
                    return !this.selected;
                }).data('id')
            };
            shop.area = {
                areaId:$('#area').find('option').not(function () {
                    return !this.selected;
                }).data('id')
            };
            var shopImg = $('shop-img')[0].files[0];
            var formData = new FormData();
            formData.append('shopImg', shopImg);
            formData.append('shopStr', JSON.stringify(shop));
            $.ajax({
                url: registerShopUrl,
                type: 'POST',
                data: formData,
                contentType: false,
                processData: false,
                cache: false,
                success: function (data) {
                    if (data.success) {
                        $.toast('Submit Successfully!');
                    } else {
                        $.toast('Submit Error! ' + data.errMsg);
                    }
                }
            });
        });
    }
});
```

`$(function(){/*...*/});`是`$(document).ready(function(){/*...*/})`的简写形式，是在DOM加载完成后执行的回调函数，并且只会执行一次。
```js
$( document ).ready(function() {
   console.log( "ready!" );
});   
 
$(function() {
   console.log( "ready!" );
});
```
在一个页面中不同的js中写的`$(function(){/*...*/});`函数，会根据js的排列顺序依次执行。 

3. Add JS reference to the `shopoperation.js`.

```js
<script type="text/javascript" src='../resources/js/shop/shopoperation.js' charset="utf-8"></script>
```

## Finish getShopInitInfo()
1. Implement `dao.ShopCategoryDao` interface
```java
public interface ShopCategoryDao {
    List<ShopCategory> queryShopCategory(@Param("ShopCategoryCondition")
                                                 ShopCategory shopCategoryCondition);
}
```

2. Implement mapper `mapper/ShopCategoryDao.xml`
```xml
<mapper namespace="com.luorinz.o2o.dao.ShopCategoryDao">
    <select id="queryShopCategory" resultType="com.luorinz.o2o.entity.ShopCategory">
        SELECT
        shop_category_id,
        shop_category_name,
        shop_category_desc,
        shop_category_img,
        priority,
        create_time,
        last_edit_time,
        parent_id
        FROM
        tb_shop_category
        <where>
            <if test="shopCategoryCondition.parent != null">
                AND parent_id = #{shopCategoryCondition.parent.shopCategoryId}
            </if>
        </where>
        ORDER BY priority DESC
    </select>
</mapper>
```
> DEBUG: Don't add aditional ','!

mybatis动态sql中的where标签的使用 - 现役码农的博客 - CSDN博客
https://blog.csdn.net/wobuaizhi/article/details/81874664

Here we can add additional "AND/OR" at the head of statement. Mybatis can automatically handle the grammer.

3. add a new record and write the test
```java
    @Test
    public void testQueryShopCategory() {
        List<ShopCategory> shopCategoryList = shopCategoryDao.queryShopCategory(new ShopCategory());
        Assert.assertEquals(3, shopCategoryList.size());
        ShopCategory test1 = new ShopCategory();
        ShopCategory testParent = new ShopCategory();
        testParent.setShopCategoryId(1L);
        test1.setParent(testParent);
        shopCategoryList = shopCategoryDao.queryShopCategory(test1);
        Assert.assertEquals(1, shopCategoryList.size());
    }
```

4. Implement the Service layar.

`Service.ShopCategoryService`

```java
public interface ShopCategoryService {
    List<ShopCategory> getShopCategoryList(ShopCategory shopCategoryCondition);
}
```

`Service.ShopCategoryServiceImpl`
```java
@Service
public class ShopCategoryServiceImpl implements ShopCategoryService{
    @Autowired
    private ShopCategoryDao shopCategoryDao;

    @Override
    public List<ShopCategory> getShopCategoryList(ShopCategory shopCategoryCondition) {
        return shopCategoryDao.queryShopCategory(shopCategoryCondition);
    }
}
```

5. Add corresponding function to controller `web/shopadmin/ShopManagementController`.

First add 2 Service object, then implement the function.

```java
    @Autowired
    private ShopCategoryService shopCategoryService;

    @Autowired
    private AreaService areaService;

    @RequestMapping(value = "/getshopinitinfo", method = RequestMethod.GET)
    @ResponseBody
    private Map<String, Object> getShopInitInfo() {
        Map<String ,Object> modelMap = new HashMap<>();
        List<ShopCategory> shopCategoryList = new ArrayList<>();
        List<Area> areaList = new ArrayList<>();
        try {
            shopCategoryList = shopCategoryService.getShopCategoryList(new ShopCategory());
            areaList = areaService.getAreaList();
            modelMap.put("shopCategoryList", shopCategoryList);
            modelMap.put("areaList", areaList);
            modelMap.put("success", true);
        } catch (Exception e) {
            modelMap.put("success", false);
            modelMap.put("errMsg", e.getMessage());
        }
        return modelMap;
    }
```

Add another limitation to mapper
```xml
<where>
    <if test="shopCategoryCondition != null">
        AND parent_id IS NOT NULL
    </if>
    ...
</where>
```



6. DEBUG
Modify js file to correctly router.
```js
...
var initUrl = '/shopadmin/getshopinitinfo';
var registerShopUrl = '/shopadmin/registershop';
...
```