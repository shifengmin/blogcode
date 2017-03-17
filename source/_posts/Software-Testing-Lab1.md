layout: article
title: Software Testing Lab1
date: 2017-03-13 18:55:33
tags: 软件测试作业
---
# Software Testing Lab1

在这次实验中，我使用了IntelliJ IDEA作为IDE， 配合Junit4， hamcrest, emma包对自己写的程序进行测试

包的下载安装通过在Maven的pom文件中添加依赖项实现，eclemma为emma在eclipse中的插件， 在IDEA中用自身集成的EMMA替代

添加依赖项的配置代码如下

```maven
    <dependencies>
        <dependency>
            <groupId>org.apache.maven.plugin-tools</groupId>
            <artifactId>maven-plugin-annotations</artifactId>
            <version>3.5</version>
            <scope>provided</scope><!-- annotations are needed only to build the plugin -->
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
        </dependency>
        <dependency>
            <groupId>org.hamcrest</groupId>
            <artifactId>hamcrest-core</artifactId>
            <version>1.3</version>
        </dependency>
    </dependencies>

```
<!-- more -->

需要接受测试的代码如下

```java
/**
 * Created by sfm on 17-3-10.
 */


public class Main {
    public  String judgeTriangleType(int a,int b,int c){
        if(a+b<=c||a+c<=b||b+c<=a||a<=0||b<=0||c<=0){
            return "NotATriangle";
        } else if (a == b && a == c && b == c) {
            return "equilateral";
        } else if (a == b || a == c || b == c) {
            return "isosceles";
        } else {
            return "scalene";
        }
    }
}
```

进行测试用的代码如下

```java

import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;

import java.util.Arrays;
import java.util.Collection;

import static org.junit.Assert.assertEquals;

/**
 * MainTester
 *
 * @author <Authors name>
 * @since <pre>Mar 10, 2017</pre>
 * @version 1.0
 */
@RunWith(Parameterized.class)

public class MainTestPara {


    private int a;
    private int b;
    private int c;
    private String expected;
    private Main proc = null;

    public MainTestPara(int a,int b,int c,String expected){
        this.a = a;
        this.b = b;
        this.c = c;
        this.expected = expected;
    }

    @Before
    public void before() throws Exception {
        System.out.println("Before Testing");
        proc = new Main();
    }


    @Parameterized.Parameters
    public static Collection<Object[]> getData(){
        return Arrays.asList(new Object[][]{
                {1,1,2,"NotATriangle"},
                {1,1,1,"equilateral"},
                {1,2,2,"isosceles"},
                {2,3,4,"scalene"}
        });
    }
    /**
     *
     * Method: judgeTriangleType(int a, int b, int c)
     *
     */
    @Test
    public void testJudgeTriangleType() throws Exception{
        assertEquals(this.expected,proc.judgeTriangleType(a,b,c));
    }

}

```

测试结果和覆盖情况如下

![Results_and_coverage](/images/stlab1.png)
