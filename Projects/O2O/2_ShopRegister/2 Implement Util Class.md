
# Implement Util class
1. Thumbnailator
Thumbnailator is a dependency for image processing 

__Configuration__

Add the dependency to `Maven`
https://mvnrepository.com/artifact/net.coobird/thumbnailator/0.4.8

```xml
<!-- https://mvnrepository.com/artifact/net.coobird/thumbnailator -->
<dependency>
    <groupId>net.coobird</groupId>
    <artifactId>thumbnailator</artifactId>
    <version>0.4.8</version>
</dependency>

```

2. Implement `util.ImageUtil`
```java
// We get the current class path from Thread.
String basePath = Thread.currentThread().getContextClassLoader().getResource("").getPath();
// We watermarked a picture and compress it.
// 0.5f is for transparancy
Thumbnails.of(new File("/Users/andaluo/Desktop/Projects/O2O/src/main/resources/test/Veronica.jpg"))
        .size(980, 515).watermark(
        Positions.BOTTOM_RIGHT,
        ImageIO.read(new File(basePath + "test/watermark.jpg")),
        0.5f).outputQuality(0.8f).toFile("/Users/andaluo/Desktop/Projects/O2O/src/main/resources/test/watermarked.jpg");
```

3. Implement PathUtil
![3_O2O_shop-2019-11-14-15-58-46.png](https://raw.githubusercontent.com/Luorinz/images/master/3_O2O_shop-2019-11-14-15-58-46.png)

4. Implement `generateThumbnail` in `ImageUtil`.

```java
/**
    * Generate the thumbnail of a given image, and create all relevant paths.
    *
    * @param thumbnail
    * @param targetAddr
    * @return the relative path of the new file
    */
public static String generateThumbnail(File thumbnail, String targetAddr) {
    // get new file name(random)
    String realFileName = getRandomFileName();
    String extension = getFileExtension(thumbnail);

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
        Thumbnails.of(thumbnail).size(200, 200).watermark(
                Positions.BOTTOM_RIGHT,
                ImageIO.read(watermark),
                0.25f).outputQuality(0.8f).toFile(dest);
    } catch (IOException e) {
        e.printStackTrace();
    }
    return relativePath;
}
```

5. Implement some helper function

```java
    /**
     * Generate random file name with current date time and a random number
     *
     * @return string
     */
    private static String getRandomFileName() {
        // get a num between 10000 and 99999
        int randNum = r.nextInt(89999) + 10000;
        String curTime = sDateFormat.format(new Date());
        return curTime + randNum;
    }

    /**
     * Get the extension of given CommonsMultipartFile
     *
     * @param cFile input file
     * @return A String of file extension
     */
    private static String getFileExtension(File cFile) {
        String originalFileName = cFile.getName();
        return originalFileName.substring(originalFileName.lastIndexOf("."));
    }


    /**
     * Make all relevant directories in the target address
     *
     * @param targetAddr target Address
     */
    private static void makeDirPath(String targetAddr) {
        String realFileParentPath = PathUtil.getImgBasePath() + targetAddr;
        File dirPath = new File(realFileParentPath);
        if (!dirPath.exists()) {
            dirPath.mkdirs();
        }
    }
```

6. Since it's easier to use java.util.File than CommonsMultipartFile, we have to do a tranfer here.

```java
    /**
     * Transfer CommonsMultipartFile to java.util.File
     * @param cFile CommonsMultipartFile, a file object from spring.
     * @return A File object
     */
    public static File transferCommonsMultipartFileToFile(CommonsMultipartFile cFile){
        File newFile = new File(cFile.getOriginalFilename());
        try {
            cFile.transferTo(newFile);
        } catch (IOException e) {
            e.printStackTrace();
            logger.error(e.toString());
        }
        return newFile;
    }
```

