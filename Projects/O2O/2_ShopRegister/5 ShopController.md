# Shop Controller

## Implement `util.HttpServletRequestUtil`
1. Implement `getInt(request, fieldName)`
```java
/**
    * Extract and parse a integer filed of a http request
    * @param request http request
    * @param key name of the field
    * @return an integer if success, -1 if error.
    */
public static int getInt(HttpServletRequest request, String key) {
    try {
        return Integer.decode(request.getParameter(key));
    } catch (Exception e) {
        return -1;
    }
}
```

2. Implement `getLong(request, fieldName)`

```java
/**
    * Extract and parse a long filed of a http request
    * @param request http request
    * @param key name of the field
    * @return a long if success, -1L if error.
    */
public static long getLong(HttpServletRequest request, String key) {
    try {
        return Long.parseLong(request.getParameter(key));
    } catch (Exception e) {
        return -1L;
    }
}
```

3. Implement `getDouble(request, fieldName)`

```java
    /**
     * Extract and parse a double filed of a http request
     * @param request http request
     * @param key name of the field
     * @return a doueble if success, -1D if error.
     */
    public static double getDouble(HttpServletRequest request, String key) {
        try {
            return Double.parseDouble(request.getParameter(key));
        } catch (Exception e) {
            return -1D;
        }
    }
```

4. Implement `getBoolean(request, fieldName)`

```java
/**
    * Extract and parse a boolean filed of a http request
    * @param request http request
    * @param key name of the field
    * @return a boolean if success, false if error.
    */
public static boolean getBoolean(HttpServletRequest request, String key) {
    try {
        return Boolean.parseBoolean(request.getParameter(key));
    } catch (Exception e) {
        return false;
    }
}
```

5. Implement `getString(request, fieldName)`
```java
/**
    * Extract and parse a String filed of a http request
    * @param request http request
    * @param key name of the field
    * @return a string if success, null if error.
    */
public static String getString(HttpServletRequest request, String key) {
    try {
        String res = request.getParameter(key);
        if (res != null) {
            res = res.trim();
        }
        if ("".equals(res)) {
            res = null;
        }
        return res;
    } catch (Exception e) {
        return null;
    }
}
```

## Implement `web.shopadmin.ShopManagementController`

1. Implement `registerShop`

> Super long and awkward, will improve it later.

```java
/**
 * The controller of the shop. Works like a Servlet.
 */
@Controller
@RequestMapping("/shopadmin")
public class ShopManagementController {
    @Autowired
    private ShopService shopService;

    @RequestMapping(value = "/registershop", method = RequestMethod.POST)
    @ResponseBody
    private Map<String, Object> registerShop(HttpServletRequest request) {
        Map<String, Object> modelMap = new HashMap<>();

        // read and transfer the corresponding information of the Shop.

        String shopStr = HttpServletRequestUtil.getString(request, "shopStr");
        ObjectMapper mapper = new ObjectMapper();
        Shop shop = null;
        try {
            shop = mapper.readValue(shopStr, Shop.class);
        } catch (Exception e) {
            modelMap.put("success", false);
            modelMap.put("errMsg", e.getMessage());
            return modelMap;
        }
        CommonsMultipartFile shopImg = null;
        CommonsMultipartResolver commonsMultipartResolver = new CommonsMultipartResolver(
                request.getSession().getServletContext()
        );
        if (commonsMultipartResolver.isMultipart(request)) {
            MultipartHttpServletRequest multipartHttpServletRequest = (MultipartHttpServletRequest) request;
            shopImg = (CommonsMultipartFile)multipartHttpServletRequest.getFile("shopImg");
        } else {
            modelMap.put("success", false);
            modelMap.put("errMsg", "empty image");
            return modelMap;
        }

        // register the shop

        if (shop != null && shopImg != null) {
            PersonInfo owner = new PersonInfo();
            owner.setUserId(1L);
            shop.setOwner(owner);
            // need to convert CommonsMultipartFile to File
            File shopImgFile = new File(PathUtil.getImgBasePath() + ImageUtil.getRandomFileName());
            try {
                shopImgFile.createNewFile();
            } catch (IOException e) {
                modelMap.put("success", false);
                modelMap.put("errMsg", e.getMessage());
                return modelMap;
            }
            try {
                inputStreamToFile(shopImg.getInputStream(), shopImgFile);
            } catch (IOException e) {
                modelMap.put("success", false);
                modelMap.put("errMsg", e.getMessage());
                return modelMap;
            }
            ShopExecution se = shopService.addShop(shop, shopImgFile);
            if (se.getState() == ShopStateEnum.CHECK.getState()) {
                modelMap.put("success", true);
            } else {
                modelMap.put("success", false);
                modelMap.put("errMsg", se.getStateInfo());
            }
            return modelMap;
        } else {
            modelMap.put("success", false);
            modelMap.put("errMsg", "The shop is empty");
            return modelMap;
        }

    }
```

2. Implement `inputStreamToFile`
Here we need to implement a helper function `inputStreamToFile`, to convert `CommonsMultipartFile` to `File`.
```java
private static void inputStreamToFile(InputStream ins, File file) {
    OutputStream os = null;
    try {
        os = new FileOutputStream(file);
        int bytesRead = 0;
        byte[] buffer = new byte[1024];
        while ((bytesRead = ins.read(buffer)) != -1) {
            os.write(buffer, 0, bytesRead);
        }
    } catch (Exception e) {
        throw new RuntimeException("Convert InputStream to File Error" + e.getMessage());
    } finally {
        try {
            if (os != null) os.close();
            if (ins != null) ins.close();
        } catch (IOException e) {
            throw new RuntimeException("Close stream error" + e.getMessage());
        }
    }
}
```

3. Debug
We need to change `ImageUtil.getRandomFileName()` from `static` to `public`.

## Improve the implementation of ShopController

1. Delete `inputStreamToFile`. Everytime we want to use the `ShopService`, we have to build a new empty file to convert input stream to file. To save resources, we want to implement that in the service layar.



2. Change the `ShopService.addShop` to `ShopExecution addShop(Shop shop, InputStream shopImgInputStream, String fileName);`

3. Change the corresponding part in `ShopServiceImpl`.

```java
    @Override
    @Transactional
    public ShopExecution addShop(Shop shop, InputStream shopImgInputStream, String fileName) {
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
                throw new ShopOperationException("Fail to add shop ");
            } else {
                if (shopImgInputStream != null) {
                    // save the image
                    try{
                        addShopImg(shop, shopImgInputStream, fileName);
                    } catch (Exception e) {
                        throw new ShopOperationException("Fail to add shop img " + e.getMessage());
                    }
                    // update shop_img of the Shop object
                    effectedNum = shopDao.updateShop(shop);
                    if (effectedNum <= 0) {
                        throw new ShopOperationException("Fail to update shop img ");
                    }
                }
            }
        } catch (Exception e) {
            throw new ShopOperationException("add Shop Error " + e.getMessage());
        }
        return new ShopExecution(ShopStateEnum.CHECK, shop);
    }
```

And the helper function, too.
```java
private void addShopImg(Shop shop, InputStream shopImgInputStream, String fileName) {
    // get the relative address of the original shop image
    String dest = PathUtil.getShopImagePath(shop.getShopId());

    // generate and set the shop Image
    String shopImgAddr = ImageUtil.generateThumbnail(shopImgInputStream, fileName, dest);
    shop.setShopImg(shopImgAddr);
}
```

4. Change the `ImageUtil`
```java
    /**
     * Generate the thumbnail of a given image, and create all relevant paths.
     *
     * @param thumbnailInputStream
     * @param targetAddr
     * @return the relative path of the new file
     */
    public static String generateThumbnail(InputStream thumbnailInputStream, String fileName, String targetAddr) {
        // get new file name(random)
        String realFileName = getRandomFileName();
        String extension = getFileExtension(fileName);

        // create the relevant paths
        makeDirPath(targetAddr);

        // specify file name
        String relativePath = targetAddr + realFileName + extension;
        logger.debug("current relative address = " + relativePath);
        String completePath = PathUtil.getImgBasePath() + relativePath;
        logger.debug("current complete address = " + completePath);

        // add watermark to the given file
        File dest = new File(completePath);
        File watermark = new File(basePath + "test/watermark.jpg");
        System.out.println(basePath + "test/watermark.jpg");
        try {
            Thumbnails.of(thumbnailInputStream).size(200, 200).watermark(
                    Positions.BOTTOM_RIGHT,
                    ImageIO.read(watermark),
                    0.25f).outputQuality(0.8f).toFile(dest);
        } catch (IOException e) {
            e.printStackTrace();
        }
        return relativePath;
    }
```



5. change the `controller.registerShop`
```java
@RequestMapping(value = "/registershop", method = RequestMethod.POST)
@ResponseBody
private Map<String, Object> registerShop(HttpServletRequest request) {
    Map<String, Object> modelMap = new HashMap<>();

    // read and transfer the corresponding information of the Shop.

    String shopStr = HttpServletRequestUtil.getString(request, "shopStr");
    ObjectMapper mapper = new ObjectMapper();
    Shop shop = null;
    try {
        shop = mapper.readValue(shopStr, Shop.class);
    } catch (Exception e) {
        modelMap.put("success", false);
        modelMap.put("errMsg", e.getMessage());
        return modelMap;
    }
    CommonsMultipartFile shopImg = null;
    CommonsMultipartResolver commonsMultipartResolver = new CommonsMultipartResolver(
            request.getSession().getServletContext()
    );
    if (commonsMultipartResolver.isMultipart(request)) {
        MultipartHttpServletRequest multipartHttpServletRequest = (MultipartHttpServletRequest) request;
        shopImg = (CommonsMultipartFile)multipartHttpServletRequest.getFile("shopImg");
    } else {
        modelMap.put("success", false);
        modelMap.put("errMsg", "empty image");
        return modelMap;
    }

    // register the shop

    if (shop != null && shopImg != null) {
        PersonInfo owner = new PersonInfo();
        owner.setUserId(1L);
        shop.setOwner(owner);

        ShopExecution se = null;
        try {
            se = shopService.addShop(shop, shopImg.getInputStream(), shopImg.getOriginalFilename());
            if (se.getState() == ShopStateEnum.CHECK.getState()) {
                modelMap.put("success", true);
            } else {
                modelMap.put("success", false);
                modelMap.put("errMsg", se.getStateInfo());
            }
        } catch (IOException e) {
            modelMap.put("success", false);
            modelMap.put("errMsg", e.getMessage());
            return modelMap;
        }
        return modelMap;
    } else {
        modelMap.put("success", false);
        modelMap.put("errMsg", "The shop is empty");
        return modelMap;
    }

}

```

## Debug
Q: Why do we hardcode a PersonInfo here?
A: Because we want to use person information in the session of the request. Here we havn't implemented it yet.