---
title: "Itextpdf给pdf模板填充数据"
date: 2018-06-16T23:04:08+08:00
draft: true
---

<!--more-->
### 添加依赖
```xml
 <dependency>
    <groupId>com.itextpdf</groupId>
    <artifactId>itextpdf</artifactId>
    <version>5.5.13</version>
 </dependency>
 <!--文字-->
 <dependency>
    <groupId>com.itextpdf</groupId>
    <artifactId>itext-asian</artifactId>
    <version>5.2.0</version>
 </dependency>

```
### 直接上代码
```java
public class PdfUtil {

    public static final String TEXT_FONT = "textfont";

    /**
     * 对pdf模板文件填充数据
     *
     * @param filePath pdf文件路径
     * @param outPutFilePath 输出pdf文件路径
     * @param data     需要填充的数据
     */
    public static void fillData(String filePath, String outPutFilePath, Map<String, String> data) {
        if (filePath == null || "".equals(filePath)) {
            throw new IllegalArgumentException("filePath not allowed null");
        }

        if (outPutFilePath== null || "".equals(outPutFilePath)) {
            throw new IllegalArgumentException("outPutFilePath not allowed null");
        }
        if (data == null || data.size() == 0) {
            throw new IllegalArgumentException("must have data");
        }
        PdfReader reader = null;
        PdfStamper stamper = null;
        try {
            // 读取pdf
            reader = new PdfReader(filePath);
            //修改pdf
            FileOutputStream fos = new FileOutputStream(outPutFilePath);
            stamper = new PdfStamper(reader, fos);
            AcroFields acroFields = stamper.getAcroFields();

            // 处理中文 这里的文字属于自带的 itext-asian
            BaseFont baseFont = BaseFont.createFont("STSong-Light", "UniGB-UCS2-H", BaseFont.NOT_EMBEDDED);

            //打印一下需要填充的表单域有哪些字段
            acroFields.getFields().forEach((k, v) -> {
                System.out.println(k);
            });
            // 设置字体并且设置具体的值
            data.forEach((k, v) -> {
                acroFields.setFieldProperty(k, TEXT_FONT, baseFont, null);
                try {
                    acroFields.setField(k, v);
                } catch (IOException | DocumentException e) {
                    log.error(e.getMessage(), e);
                }
            });

            // 如果为false那么生成的PDF文件还能编辑，一定要设为true
            stamper.setFormFlattening(true);
        } catch (IOException | DocumentException e) {
            log.error(e.getMessage(), e);
        } finally {
            if (stamper != null) {
                try {
                    stamper.close();
                } catch (DocumentException | IOException e) {
                    e.printStackTrace();
                }
            }
            if (reader != null) {
                reader.close();
            }
        }
    }
}
```

### 遇到的坑
1. 字体的问题，默认不支持中文，我采用的是使用itext-asian自带的字体，可以使用系统中的字体或者自己下载字体，具体方法可以百度
2. PdfStamper必须在PdfReader前关闭，否则会报错
3. 因为这里是根据pdf模板文件填充数据，所以必须先存在一个带有表单域的pdf文件，
我这边使用`PDF Editor 6 Pro`,具体怎么下载使用因为篇幅有限，大家可以自行百度
4. 其他PDF编辑工具可以使用`Adobe Acrobat`，这也是需要收费的，有时间大家折腾一下
