---
title: 去除Html文档中的Html标签
date: 2021-4-29 17:51:33 +0800
categories: [Java, 代码]
tags: [代码, Java]     # TAG names should always be lowercase
---

## 前言

在爬虫爬取网页的Html代码来做简单搜索引擎，需要获取网站标题以及网站内容，其中爬取的网站内容为Html文档格式，可通过以下代码转为纯文本。

## 代码

```java
import java.io.ByteArrayInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.Reader;

import javax.swing.text.html.HTMLEditorKit;
import javax.swing.text.html.parser.ParserDelegator;

/**
 * @author: sadboy
 **/
public class Html2Text extends HTMLEditorKit.ParserCallback{
    private static Html2Text h2t = new Html2Text();
    private Html2Text(){};
    private StringBuffer s;
    private void parse(String str) throws IOException {
        InputStream iin = new ByteArrayInputStream(str.getBytes());
        Reader in = new InputStreamReader(iin);
        s = new StringBuffer();
        ParserDelegator delegator = new ParserDelegator();
        // the third parameter is TRUE to ignore charset directive
        delegator.parse(in, this, Boolean.TRUE);
        iin.close();
        in.close();
    }
    public void handleText(char[] text, int pos) {
        s.append(text);
    }
    public String getText() {
        return s.toString();
    }
    public static String getContent(String str) {
        try {
            h2t.parse(str);
        } catch (IOException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        return h2t.getText();
    }
    public static void main (String[] args) {
        System.out.println(Html2Text.getContent("<h2 id=\"md2x-hello-world\">Hello,World</h2>"));
    }
}
```

