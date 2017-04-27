# Grandpa
_Unit testing in `Kotlin` is like a walk by the lake with Grandpa!._ 

![Alt text](https://github.com/sudipto80/Grandpa/blob/master/free-cute-cartoon-grandpa-clip-art-jeiws6-clipart.png)

## Why another framework? 
There are some frameworks to do unit testing in Kotlin. For example Kluent and Spek. However these frameworks have a major problem. 
These don't allow gluing together multiple checks and therefore each tests fail at the first occurence of any faliure that might occur. For example consider the following JUnit test 

```java

import static org.junit.jupiter.api.Assertions.assertEquals;

import org.junit.jupiter.api.Test;
k
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

## What is `Grandpa`

`Grandpa` is a DSL (Domain Specific Language) for unit testing written using `Kotlin` for `Kotlin`. The main focus of `Grandpa` is simplicity and intention driven unit testing with a focus on very less typing needs. The motto is getting more done with less code. 
Since `Kotlin` as a language provide several ways to communicate the intent of a test developer, it is a natural choice for writing the DSL for unit testing. 

## What does `Grandpa` do ? Show me some code!
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
            //Infix function And in action!
            val (testPassed, failureMessage) = nameCheck And intCheckResult And anotherStringCheckResult
            assertTrue(failureMessage,testPassed);
  }
```
Grandpa will also have back quote version of several methods and extension functions whenever it makes sense. So it will be possible to write checks like this. 

```kotlin
 val aGoodCondition = (2+getRandom())
                               .isPositive()
                               .`should be between` (1 And 5)
                               .pleaseCheck()
``` 
As you can see that this test can be translated to other languages fairly easily by providing duplicate functions with different names for other languages like French for example. 

```kotlin
val aGoodConditionDescribedInFrench = (2 + getRandom())
                                      .`est positif` //Same as isPositive
                                      .`devrait se situer entre` (1 et 5) //Same as `should be between` (1 And 5)
                                      .`s’il vous plaît vérifier`//Same as pleaseCheck
```
I would agree that this test might be verbose but the readability gain is awesome. Also non programmers domain experts can express their idea about correctness very easily (and in their own language). The project `Grandpa` relies on [`Extension Functions`](https://kotlinlang.org/docs/reference/extensions.html) and [`Infix`](https://kotlinlang.org/docs/reference/functions.html) functions feature of `Kotlin`
 

## What are the benefits of testing like Grandpa?
Grandpa helps you 

* Type less 
* Convey your intent 
* Write tests in your language 
* Have auto filled your asserts with messages that make sense 

## A side by side comparison

## Grandpa is friend with everyone!
You love JUnit! You are welcome, You hate it? You are welcome too. The biggest fallacy of unit testing is that we need an unit testing framework for unit testing. How comfortable! Trust me all unit testing framework can just boil down to one function. A function that can assert the truthfulness of a given expression. In JUNit it is `assertTrue`. In NUnit it is `Assert.IsTrue` 

The rationale behind this generalization is that every unit test can be written such that it will be enough to test the truthfulness of an expression or multiple such expressions. Where test frameworks help is that they provide a multitude of overloads of several methods to test the equality and in-equality of several expressions. All that overloads can disappear and you should still be able to unit test with `assertTrue` or equivalent functions in other frameworks. `Grandpa` helps you celebrate this! 

So if you love testing frameworks you can use `Grandpa` with those else you can use `Grandpa` inside your project and just use if conditions. 

## Grandpas Diction!
Grandpa likes English. But feel free to teach him new languages. Extending is really simple and the result is awesome. You can now write your unit tests in your language as shown before. 

Grandpa has several extension methods and their back tick version that improves readability. Here are some of his phrases (This is by no means comprehensive). He really likes to start his phrases with `should`. 

* `shouldBe`
* `shouldNotBe`
* `shouldBeBetween` 
* `shouldNotBeBetween`
* `shouldContain`
* `shouldNotContain`
* `shouldHave`
* `shouldNotHave`
* `shouldNotBeNull`
* `shouldNotBeEmpty`
* `shouldHaveAtLeast`
* `shouldHaveAtMost`
* `shouldBeEquivalentTo`
* `shouldNotBeEquivalentTo`
* `IsMadeOf`
* `IsNotMadeOf`
* `IsPositive`
* `IsGreaterThan`
* `IsGraterThanOrEqualTo`
* `IsLessThan` (And all other operators )

## Grandpa Packages
Functionalities in Grandpa comes in few well structured packages. 

`Grandpa.Numbers` :Functionalities for asserting numeric facts

`Grandpa.Text` : Functionalities for asserting string related facts.

`Grandpa.Date` : Functionalities for asserting date related facts.

`Grandpa.Time` : Functionalities for asserting time related facts.

`Grandpa.Utilities` : Home of several glue functions (created using Extension and Infix functions) 

## Teaching Grandpa New Languages!
You can extend Grandpa by creating a new package based on the existing ones by adding the language markers at the end. For example packages meant for `French` should be marked as `fr` at the end. So when you extend the `Grandpa.Numbers` package for `French` you should name it as `Grandpa.Numbers.fr`. This is just a convention that have been proven useful over the years. 




