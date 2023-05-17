# MaxLang Quick Start 
## -- All New Design, All For DevOps 

MaxLang is the dedicated programming language for automating the DevOps tasks, which is implemented and maintained by SpotMax team.

## Primitive Data Types
### Number
In Maxlang, it is not necessary to distinguish the numerical value's type, such as integer and float. Maxlang can recoginze and convert values automatically. 
```
a = 11
b = 100
a + b
```
a = 10
b = 1.2
a + b
```
### String
A string value is quoted by " or ` .
```
a = "Hello World"
a
```
a = `Hello World!
     I love China!`
a
```
a = "Hello"
b = `World`
a+" "+ b
```
### Boolean
The boolean value is either "true" or "false".
```
a = true;
a
```
2 > 3
```
### Function
Function is treated as the basic data type and the first class citizen in Maxlang. If you are familiar with Lisp, you can treat it as the function in Lisp.

In Maxlang, function can be used as the arguments or the return value of other functions.

```
add = fn(x,y){x+y}
add(1,1)
```
sub = fn(x,y){
         return x-y;
       }
sub(2,1)
```
The following example is about how you can implement "Command Patter" (GoF) very easily by leveraging Maxlang's function.
```
cmdPattern = fn(x, y){y(x)}
cmdPattern(10, fn(x){x*10}) 

```
cmdPattern(10, fn(x){x/10})
```
## Statements
### Conditional statement
The typical conditional statements, "if" and "if-else" are both supported in Maxlang.
```
if (true) {
    "TRUE"
}else{
    "FALSE"
}
```
### Loop statement

For loop structure, currently, only "while" statement is supported. The "break" and "continue" statements are supported, which can be used in the loop structure to change the execution flow.
```
i = 1;
sum = 0;
while (i < 10) {
    sum = sum + i;
    i = i + 1
}
sum 
```
i = 1
sum = 0
while (i<10) {  
    if (i/2 * 2 != i) { /* 2 + 4 + 6 + 8 */
        i = i + 1
        continue
    }
    sum = sum + i
    i = i+1
}
sum
```
## Collections
### Array
The elements in an array can be any primitive type object, even a function, also the different type of the elements could be mixed in an array. 

The index of an array starts from 0.
```
myArray = [1,2, fn(x,y){x+y}, "Hello ", "World"]
```
myArray[2](myArray[0],myArray[1])
```
myArray[2](myArray[3],myArray[4])
```
#### Built-in functions for array

##### len (  < array > )
Get the number of the elements in the array.
```
arr = [1,2,3,4,5]
```
len(arr)
```
##### first ( < array > )
Get the first element of the array
```
first(arr)
```
##### last ( < array > )
Get the last element of the array
```
last(arr)
```
##### rest (< array >)
return a new array with removing the first element 
```
rest(arr)
```
The following example is to travel an array with the built-in functions.
```
nums = [1,2,3,4,5,6,7,8,9,10]
sum = 0
while(len(nums)>0){
    sum = sum + first(nums)
    nums = rest(nums)
}
sum
```
### HashTable
Like the mainstream programming language, HashTable is the collection of the key-value pairs. 

In a key-value pair :

The key can be a primitive object except a function. 

The value be a primitive object, a collection or a hashtable. 
```
dic = {1:"one","one":1,"inc":fn(x){x+1}, "arr":[1,2,3,5], "table":{2:"two","sub":fn(x){x-1}}}
```
dic[1]
```
dic["inc"](dic["one"])
```
#### Built-in functions for Hashtable
##### keys (< hashtable >)
Get the keys of a hashtable.
```
keys(dic)
```
##### values (< hashtable >)
Get the values of a hashtable
```
values(dic)
```
### Built-in functions
#### Conversion
##### ntos (< number >)
Convert a numeric value to the related string value.
```
"result = " + ntos(100)
```
"result = " + ntos(10.19)
```
##### ston (< string >)
Convert a string value to the related numeric value.
```
1 + ston("10")
```
1 + ston("11.11")
```
#### JSON query
For one simple example is more expressive than thousands of the words, I'd like to use several simple examples to explain how the built-in functions work.
```
json=`{"name":"sam", 
        "skills": { 
                    "coding":["C","Java","php"], 
                     "habits":["eating","sleeping"],
                     "scores":[80,90,100]
                    }
       }`

```
jpath("skills.coding.[1]", json)
```
jpath("skills",json)["coding"][2]
```
## MaxLang is growing fast, still more to come!