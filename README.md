Grandpa
_Unit testing in `Kotlin` is like a walk by the lake._ 

![Alt text](https://github.com/sudipto80/Grandpa/blob/master/free-cute-cartoon-grandpa-clip-art-jeiws6-clipart.png)

## Why another framework? 
There are some frameworks to do unit testing in Kotlin. For example Kluent and Spek. However these frameworks have a major problem. 
These don't allow gluing together multiple checks and therefore each tests fail at the first occurence of any faliure that might occur. For example consider the following JUnit test 

```java

import static org.junit.jupiter.api.Assertions.assertEquals;

import org.junit.jupiter.api.Test;

public class MyTests {

        @Test
        public void multiplicationOfZeroIntegersShouldReturnZero() {
                MyClass tester = new MyClass(); // MyClass is tested

                // assert statements
                assertEquals("10 x 0 must be 0", 0, tester.multiply(10, 0));
                assertEquals("0 x 10 must be 0", 0, tester.multiply(0, 10));
                assertEquals("0 x 0 must be 0", 0, tester.multiply(0, 0));
        }
}
```
This test will fail should the obvious implementation of `tester.multiply` is wrong yielding a false result for `10x0` even though it produces correct result for `0x0`. And since Kluent and all other such fluent testing interfaces rely on JUnit without a mechanism of message passing in between the phases of an unit test, all of these fail to create a single error message per test fixing which will make sure that the entire test passes irrespective of the number of assert statements in the test. 

## What does `Grandpa` do ?
Grandpa lets you glue your test results inside your unit test phase by phase. So that you can write tests like this 

```kotlin
    @Test
    public void CheckNamesAndSums(){
            val nameCheck = getName()
                                  .LengthIsBetween(3, 6)
                                  .pleaseCheck()
            val intCheckResult = sumOf(numbers)
                                  .shouldBe(36)
                                  .pleaseCheck()
            val anotherStringCheckResult = getGivenName()
                                   .LengthIsBetween(12,34)
                                   .pleaseCheck()
            //Infix function "And" in action!
            val (testPassed, failureMessage) = nameCheck And intCheckResult And anotherStringCheckResult
            assertTrue(failureMessage,testPassed);
  ```
 `Grandpa` relies on [`Extension Functions`](https://kotlinlang.org/docs/reference/extensions.html) and [`Infix`](https://kotlinlang.org/docs/reference/functions.html) functions feature of `Kotlin`

## What are the benefits of testing like Grandpa?
Grandpa helps you 

* Type less 
* Convey your intent 
* Have auto filled your asserts with messages that make sense 

