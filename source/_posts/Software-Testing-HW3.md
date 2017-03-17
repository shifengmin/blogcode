layout: article
title: Software Testing HW3
date: 2017-03-14 23:06:24
tags: 软件测试作业
comments: true
---
# Software Testing HW3

## a.
Control Flow Diagram
![Control Flow Diagram](/images/STHW3.png)

<!-- more -->

## b.
Change the code in line 20 from:
```java
int [] primes = new int [MAXPRIMES];```
to:
```java
int [] primes = new int [4];
```

## c.

$$ n = 1 $$


## d.
### Node Coverage
$$ V=\\{1,2,3,4,5,6,7,8,9,10,11\\} $$

### Edge Coverage
$$ E=\\{(1,2),(2,3),(2,8),(3,4),(3,6),(8,9),(6,7),(6,2),(4,5),(9,10),(9,11),(5,6),(7,2),(10, 9)\\} $$

### Prime Path Coverage
$$ P = \\{(1,2,3,4),(1,2,3,4,5,6,7),(1,2,3,4,5,6),(1,2,8,9,10),(1,2,8,9,11)\\} $$

## e.

### Code being tested
```java
/**
 * Created by sfm on 17-3-14.
 */
public class PrintPrimes {
    private final int MAXPRIMES = 100000;

    private boolean isDivisible(int d, int x){
        if(x % d == 0) return true;
        else return false;
    }

    public int[] printPrimes(int n){
        int curPrime;
        int numPrimes;
        boolean isPrime;
        int [] primes = new int [MAXPRIMES];

        primes[0] = 2;
        numPrimes = 1;
        curPrime = 2;
        while(numPrimes<n){
            curPrime++;
            isPrime = true;
            for(int i=0;i<=numPrimes-1;i++){
                if(isDivisible(primes[i],curPrime)){
                    isPrime = false;
                    break;
                }
            }
            if(isPrime){
                primes[numPrimes] = curPrime;
                numPrimes++;
            }
        }

        for(int i=0; i<=numPrimes-1;i++){
            System.out.println("Prime: " + primes[i]);
        }
        return primes;
    }
}


```

### Code for testing

```java
import org.junit.Test;
import org.junit.Before;
import org.junit.After;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;

import java.util.Arrays;
import java.util.Collection;

import static org.junit.Assert.assertArrayEquals;

/**
 * PrintPrimes Tester.
 *
 * @author <Authors name>
 * @since <pre>Mar 14, 2017</pre>
 * @version 1.0
 */

@RunWith(Parameterized.class)


public class PrintPrimesTest {

    private int n;
    private int[] expected = null;
    private PrintPrimes proc = null;

    public PrintPrimesTest(int n, int [] expected){
        this.n = n;
        this.expected = expected;
    }

    @Before
    public void before() throws Exception {
        proc = new PrintPrimes();
    }

    @After
    public void after() throws Exception {
    }


    @Parameterized.Parameters
    public static Collection<Object[]> getData(){
        return Arrays.asList(new Object[][]{
                {1, new int[]{2}},
                {2, new int[]{2,3}},
                {5, new int[]{2,3,5,7,11}}
        });
    }

    /**
     *
     * Method: printPrimes(int n)
     *
     */
    @Test
    public void testPrintPrimes() throws Exception {
//TODO: Test goes here...
        assertArrayEquals(this.expected,proc.printPrimes(n));
    }


    /**
     *
     * Method: isDivisible(int d, int x)
     *
     */
    @Test
    public void testIsDivisible() throws Exception {
//TODO: Test goes here...
/*
try {
   Method method = PrintPrimes.getClass().getMethod("isDivisible", int.class, int.class);
   method.setAccessible(true);
   method.invoke(<Object>, <Parameters>);
} catch(NoSuchMethodException e) {
} catch(IllegalAccessException e) {
} catch(InvocationTargetException e) {
}
*/
    }

}


```

### Results

![Results](/images/STHW3R.png)

