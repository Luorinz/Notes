# Verification code
## 1. Configuration
Maven Repository: com.github.penggle » kaptcha
https://mvnrepository.com/artifact/com.github.penggle/kaptcha

### 1.1 Add the dependency to `pom.xml`.

### 1.2 Add servlet mapping to `WEB-INF/web.xml`.

```xml
    <!--  Kaptcha-->
    <servlet>
        <servlet-name>Kaptcha</servlet-name>
        <servlet-class>com.google.code.kaptcha.servlet.KaptchaServlet</servlet-class>
        <!--      Define the style of the kaptcha-->
        <!--has border or not-->
        <init-param>
            <param-name>kaptcha.border</param-name>
            <param-value>no</param-value>
        </init-param>
        ......
    </servlet>
```

Configuration
```
kaptcha.border: no
kaptcha.textproducer.font.color: red
kaptcha.image.width: 135
kaptcha.textproducer.char.string: ACDEFHKPRSTWX345679
kaptcha.image.height: 50
kaptcha.textproducer.font.size: 43
kaptcha.noise.color: black
kaptcha.textproducer.char.length: 4
kaptcha.textproducer.font.names: Arial
```

### 1.3 Add Katcha component to `shopoperation.html`
```html
<!--Kaptcha verification code-->
<li class="align-top">
    <div class="item-content">
        <div class="item-media"><i class="icon icon-form-comment"></i></div>
        <div class="item-inner">
            <div class="item-title label">Verification Code</div>
            <input type="text" id="j_kaptcha" placeholder="Verification Code">

            <div class="item-input">
                <!--src="../Kaptcha" taken from Servlet we mapped in web.xml                                    -->
                <img id="kaptcha_img" alt="Click to refresh" title="Refresh"
                        onclick="changeVerifyCode(this)" src="../Kaptcha"/>
            </div>
        </div>
    </div>
</li>
```

### 1.4 Modify JavaScript Files
Implement `resources/js/common/common.js`
```js
function changeVerifyCode(img) {
    img.src = "../Kaptcha?" + Math.floor(Math.random() * 100);
}
```

Add the kaptcha related part to the js code in `shopoperation` before the `ajax` part.

```js
// Vericifation Code handler
var verifyCodeActual = $('#j_kaptcha').val();
if (!verifyCodeActual) {
    $.toast('Please enter the verification code.');
    return;
}
formData.append('verifyCodeActual', verifyCodeActual);
```

Add the `commom.js` to the `shopoperation.html`
```html
<script type="text/javascript" src='../resources/js/common/common.js' charset="utf-8"></script>
```

### 1.5 Configure the Servlet mapping in `web.xml`
```xml
<servlet-mapping>
    <servlet-name>Kaptcha</servlet-name>
    <url-pattern>/Kaptcha</url-pattern>
</servlet-mapping>
```

Debug: Here we also need to add another tag `<absolute-ordering/>`, otherwise we won't be able to start the application.

## 2. Improvement
### 2.1 Refresh Kaptcha each time we fail

Add the logic to `shopoperator.js` in `$ajax({...})`
```js
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
        $('#kaptcha_img').click();
    }
});
```


### 2.2 Implement `CodeUtil.java`
```java
public class CodeUtil {
    public static boolean checkVerifyCode(HttpServletRequest request) {
        String verifyCodeExpected = (String) request.getSession().getAttribute(Constants.KAPTCHA_SESSION_KEY);
        String verifyCodeActual = HttpServletRequestUtil.getString(request, "verifyCodeActual");
        if (verifyCodeActual == null || ! verifyCodeActual.equals(verifyCodeExpected)) {
            return false;
        }
        return true;
    }
}
```

Add Verify code check in the controller. Modify `ShopManagementController`, add the check in the head of `registerShop`
```java
if (!CodeUtil.checkVerifyCode(request)) {
    modelMap.put("success", false);
    modelMap.put("errMsg", "Wrong Verification Code.");
    return modelMap;
}
```

