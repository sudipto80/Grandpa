
# Grandpa
_Unit testing is like a walk by the lake._ 

![Alt text](https://github.com/sudipto80/Grandpa/blob/master/free-cute-cartoon-grandpa-clip-art-jeiws6-clipart.png)




```kotlin
fun Triple<Int,Boolean,String>.shouldBe(other :Int, prev : Triple<Int,Boolean,String>? = null)
        :Triple<Int,Boolean,String>
{
    if(prev!=null)
    {
        if(this?.first == other)
        {
            return Triple(this.first,prev.second && true , prev.third);
        }
        else
        {
            return Triple(this.first,prev.second && false,
                    prev?.third + "[The number should be $other but it is $this]");
        }
    }
    else
        return this.first.shouldBe(other);
}
```

