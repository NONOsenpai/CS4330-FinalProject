# Comparisons of References and Values
#### *This document will explain how values are compared, ie. comparing two strings.* 

<br></br>
## References and Values
Comparing two variables and checking if they are 'the same' ca be pretty tricky. For primitive types (int, double, char), a simple == is used. These primitive types only contain the values associated with the variable. However, many comparisons are made on objects (String, Double, CustomObj). These contain much more information about the variable than just its value. For example, in the topic Inheritance and Extension, Cabbage's have a weight and freshness, say you wanted had a few cabbage objects and wanted to see if any are the same. How could you do that? 

Note 1: when talking about 'comparing references' and an object is said to have the 'same reference' as another, this means seeing if two objects point to the same address of 'one' object or the two objects have the same 'identity.' Similar to a duplicate, but the difference is that if you change one, the other is also changed. Life example: duplicates would be identical twins and 'same references' would be two souls trapped in one body (they both have control over the singular body) *and/ or* a person with two nicknames (people *refer* to someone by two different names, but it's still the same person either time).
Note 2: a custom object is a class a programmer makes, ex. Cabbage, Vegetable, etc. A non-custom object is a built-in object, ex. Java: Double, String, etc. Any instance of the word 'object' that is not preceeded by 'custom' is a non-custom/ built-in object.

<br></br>
## Java's Implementation
*The classes may be ignored. Only one function is 'important' but please start with main, as this will go in-depth with java's comparisons.*
```java
public class Vegetable {
    private final String kindOfFood = "Vegetable";
    double weight;
    // other states

    public Vegetable(double weight){
        this.weight = weight;
    }

    public void printWeight(){
        System.out.println(weight);
    } 
    
    public void printKind(){
        System.out.println("Vegetable Class kindOfFood: " + kindOfFood);
    } 
    // other behaviours

public class Cabbage extends Vegetable{
    String kindOfFood = "Cabbage";
    boolean fresh;
    // other states

    public Cabbage(double weight, boolean fresh){
        super(weight);
        this.fresh = fresh;
    }
    
    @Override
    public void printKind(){
        System.out.println("Cabbage Class kindOfFood: " + kindOfFood);
    }
    
    public void printFresh(){
        System.out.println("Cabbage Class fresh: " + fresh);
    }
    
    
    // NEW FUNCTION FOR THIS TOPIC'S DISCUSSION
    public boolean equals(Object other){
        if(!(other instanceof Cabbage))
            return false;
        else{
            Cabbage otherObj = (Cabbage) other;
            return this.weight == otherObj.weight && this.fresh == otherObj.fresh;
        }
    }
    // we need to override the .equals() function in order to compare
    //      every attribute
    
    // other behaviours
}

public static void main(String[] args) {
        Cabbage cabbage1 = new Cabbage(3.3, true);
        Cabbage cabbage2 = new Cabbage(3.4, false);
        Cabbage cabbage3 = new Cabbage(3.3, true);
        Cabbage cabbage4 = new Cabbage(3.3, false);
        
        String str1 = "Hi";
        String str2 = "Hello";
        String str3 = "Hi";
        
        int i = 3;
        int j = 3;
        int k = 2;
        System.out.println("Primitive Comparisons:");
        System.out.println("i = " + i + ", j = " + j + ", k = " + k);
        System.out.println("i == j: " + (i == j));
        System.out.println("i == k: " + (i == k));
        
        System.out.println("\nObject Comparisons:");
        System.out.println("Cabbage1: ");
            System.out.println("\tweight: " + cabbage1.weight);
            System.out.println("\tfresh: " + cabbage1.fresh);
        System.out.println("Cabbage2: ");
            System.out.println("\tweight: " + cabbage2.weight);
            System.out.println("\tfresh: " + cabbage2.fresh);
        System.out.println("Cabbage3: ");
            System.out.println("\tweight: " + cabbage3.weight);
            System.out.println("\tfresh: " + cabbage3.fresh);
        System.out.println("Cabbage4: ");
            System.out.println("\tweight: " + cabbage4.weight);
            System.out.println("\tfresh: " + cabbage4.fresh);
        // we can see from the declarations and these prints that
        //      only cabbage1 and cabbage3 are truly 'equal' or the same
        // let's compare them with ==
        System.out.println("\nComparing objects with ==: ");
        System.out.println("cabbage1 == cabbage 3: " + (cabbage1 == cabbage3));
        System.out.println("cabbage1 == cabbage 2: " + (cabbage1 == cabbage2));
        System.out.println("cabbage1 == cabbage 4: " + (cabbage1 == cabbage4));
        System.out.println("cabbage2 == cabbage 3: " + (cabbage2 == cabbage3));
        System.out.println("cabbage2 == cabbage 4: " + (cabbage2 == cabbage4));
        System.out.println("cabbage3 == cabbage 4: " + (cabbage3 == cabbage4));
        // why are none of these correct??
        // with objects, == checks to see if the variables are pointing to
        //      the same object (explicitly the same: the variables point to 
        //      the same address of the object)
        
        System.out.println("\nComparing objects with == (fixed): ");
        System.out.println("Cabbage cabbage5 = cabbage2;");
        Cabbage cabbage5 = cabbage2;
        System.out.println("cabbage2 == cabbage 5: " + (cabbage2 == cabbage5));
        // Q1: what will this output? what does this mean?
        System.out.println("cabbage5.weight = 5;");
        cabbage5.weight = 5;
        System.out.println("cabbage5.weight = " + cabbage5.weight);
        System.out.println("cabbage2.weight = " + cabbage2.weight);
        System.out.println("cabbage2.weight == cabbage5.weight: " + (cabbage2.weight == cabbage5.weight));
        // Q2: based on your conclusion from Q1, what will these two statements output?
        
        // now let's backtrack
        // we know that cabbage1 and cabbage3 are the same, how do we compare them?
        // now let's backtrack
        // we know that cabbage1 and cabbage3 are the same, how do we compare them?
        // let's learn about .equals()
        System.out.println("\nComparing Strings with str1.equals(str2): ");
        System.out.println("str1 = " + str1 + ", str2 = " + str2 + ", str3 = " + str3);
        System.out.println("str1.equals(str3): " + (str1.equals(str3)));
        System.out.println("str1.equals(str2): " + (str1.equals(str2)));
        System.out.println("str2.equals(str3): " + (str2.equals(str3)));
        // this is a special function developed for String objects
        // all objects have this function, actually, but it doesn't
        //      always work as expected 
        // for Strings, we know we're specifically looking at each character
        //      and the character's order in the string and seeing if str1
        //      has the same string as str3, which it does
        // for custom objects, there needs to be specificity
        //      ex. what makes two objects the same?
        //      typically, this means seeing if the objects are the same instance,
        //          if this is true, then one would have to compare all the variables
        //          ex. Cabbages have weight and fresh (kindOfFood can be ignored)
        
        // fortunately we can use our knowledge of overriding
        //      to make this function do what we want it too
        //      (see the overriden function in Cabbage class)
        // Q3: a. what will these lines output if the function isn't overriden?
        //     b. will any print true? why?
        System.out.println("\nComparing Objects with overidden .equals(): ");
        System.out.println("cabbage1.equals(cabbage3): " + (cabbage1.equals(cabbage3)));
        System.out.println("cabbage1.equals(cabbage2): " + (cabbage1.equals(cabbage2)));
        System.out.println("cabbage1.equals(cabbage4): " + (cabbage1.equals(cabbage4)));
        System.out.println("cabbage2.equals(cabbage3): " + (cabbage2.equals(cabbage3)));
        System.out.println("cabbage2.equals(cabbage4): " + (cabbage2.equals(cabbage4)));
        System.out.println("cabbage3.equals(cabbage4): " + (cabbage3.equals(cabbage4)));
        System.out.println("cabbage2.equals(cabbage5): " + (cabbage2.equals(cabbage5)));
        // Q4: what will cabbage2.equals(cabbage5) output if equals() IS overriden?
        // now this can be a small hassle trying to compare every variable of an object,
        //      but it can be very useful for finding duplicate information
        // however, most programming suggests to have a 'primary key' that
        //      makes objects unqiue; then, one would compare those keys
    }
```

<br></br>
## Swift's Implementation
*The classes may be ignored. Only one function is 'important' but please start after the class declarations, as this will be the main section of learning how to compare variables in Swift.*
```python
class Vegetable{
  private var kindOfFood: String = "Vegetable";
  var weight: Double = 0;
  
  init(weight: Double){
    self.weight = weight;
  }
  
  func printWeight(){
        print(weight);
  } 
  
  func printKind(){
      print("Vegtable Class kindOfFood: " + kindOfFood)
  }
  
}
class Cabbage: Vegetable{
    var kindOfFood: String = "Cabbage";
    var fresh: Bool = true;
  
    init(weight: Double, fresh: Bool){
        super.init(weight: weight)
        self.fresh = fresh;
    }
  
    override func printKind(){
        print("Cabbage Class kindOfFood: " + kindOfFood)
    }
    
    func printFresh(){
        print("Cabbage Class fresh: " + String(fresh));
    }
  
    static func == (lhs: Cabbage, rhs: Cabbage) -> Bool{
        return lhs.weight == rhs.weight && lhs.fresh == rhs.fresh
    }
    
}
var cabbage1 = Cabbage(weight: 3.3, fresh: true);
var cabbage2 = Cabbage(weight: 3.4, fresh: false);
var cabbage3 = Cabbage(weight: 3.3, fresh: true);
var cabbage4 = Cabbage(weight: 3.3, fresh: false);

var str1: String = "Hi"
var str2: String = "Hello"
var str3: String = "Hi"

var i: Int = 3
var j: Int = 3
var k: Int = 4
print("'Primitive' Comparisons with ==: ")
print("i = " + String(i) + ", j = " + String(j) + ", k = " + String(k))
print("i == j: " + String(i == j))
print("i == k: " + String(i == k))
print("j == k: " + String(j == k))

print("\nString Comparisons with ==: ")
print("str1 = " + str1 + ", str2 = " + str2 + ", str3 = " + str3)
print("str1 == str3: " + String(str1 == str3))
print("str1 == str2: " + String(str1 == str2))
print("str2 == str3: " + String(str2 == str3))
# now this is definitely different from java
#  == in swift will compare 'what's expected'
#  we know what to expect when we compare words
#      numbers, booleans, etc. we DON'T know how
#      to compare 'custom' objects

# let's see what happens when we compare the
#  cabbage objects with ==
print("\nCustom Object Comparisons with ==: ")
print("cabbage1: weight = " + String(cabbage1.weight) + ", fresh = " + String(cabbage1.fresh))
print("cabbage2: weight = " + String(cabbage2.weight) + ", fresh = " + String(cabbage2.fresh))
print("cabbage3: weight = " + String(cabbage3.weight) + ", fresh = " + String(cabbage3.fresh))
print("cabbage4: weight = " + String(cabbage4.weight) + ", fresh = " + String(cabbage4.fresh))
# turns out, objects can't == at all!
# but swift has another version: ===
#      let's try that
print("\nCustom Object Comparisons with ===: ")
print("cabbage1 === cabbage3: " + String(cabbage1 === cabbage3))
print("cabbage1 === cabbage2: " + String(cabbage1 === cabbage2))
print("cabbage1 === cabbage4: " + String(cabbage1 === cabbage4))
print("cabbage2 === cabbage3: " + String(cabbage2 === cabbage3))
print("cabbage2 === cabbage4: " + String(cabbage2 === cabbage4))
print("cabbage3 === cabbage4: " + String(cabbage3 === cabbage4))
# now we're getting the same issue with java
# === acts like == in java, when comparing custom objects
# which means it's testing if the objects point to the same address
#      aka. referencing the same object
print("\nCustom Object Comparisons with ===: ")
print("var cabbage5 = cabbage2")
var cabbage5 = cabbage2
print("cabbage2 === cabbage5: " + String(cabbage2 === cabbage5))
# Q5: what will this output? why?
cabbage5.weight = 5
print("cabbage5.weight = " + String(cabbage5.weight))
print("cabbage2.weight = " + String(cabbage2.weight))
print("cabbage2.weight == cabbage5.weight: " + String(cabbage2.weight == cabbage5.weight))
# Q6: based on your conclusion from Q5, what will 
#      these lines output 

# now, java was able to override the equals() method,
#      which means the equivalent *should* be available
#      in swift
# we COULD create an isEqual func to emulate java's
#      but we can actually override == and ===
print("\nCustom Object Comparisons with custom == func: ")
print("cabbage1 == cabbage3: " + String(cabbage1 == cabbage3))
print("cabbage1 == cabbage2: " + String(cabbage1 == cabbage2))
print("cabbage1 == cabbage4: " + String(cabbage1 == cabbage4))
print("cabbage2 == cabbage3: " + String(cabbage2 == cabbage3))
print("cabbage2 == cabbage4: " + String(cabbage2 == cabbage4))
print("cabbage3 == cabbage4: " + String(cabbage3 == cabbage4))
print("cabbage2 == cabbage5: " + String(cabbage2 == cabbage5))
# Q7: what will cabbage2 == cabbage5 output?

# bonus round
# Q8: what will the following lines output
print("'Primitive' and String comparisons with ===:")
print("i = " + String(i) + ", j = " + String(j) + ", k = " + String(k))
print("i === j: " + String(i === j))
print("i === k: " + String(i === k))
print("j === k: " + String(j === k))
print("i = " + String(i) + ", j = " + String(j) + ", k = " + String(k))
print("i == j: " + String(i == j))
print("i == k: " + String(i == k))
print("j == k: " + String(j == k))
# hint: === tests for same reference or 'identity'

# NOTE: this is written with python markdown as swift is not yet supported. Swift comments (// and /**/) are the same as Java's.
#           this is also why -> and && are highlighted in a red block, as they are not used in python.
```


<br></br>
## Comparing
Java and Swift are definitely near opposite ends on comparing references vs. values. Comparing 'primitive' types in Java and Swift will still be the same with the ==; however, Swift has a different interpretation of 'primitive' as noted by:
```python
print("\nString Comparisons with ==: ")
print("str1 = " + str1 + ", str2 = " + str2 + ", str3 = " + str3)
print("str1 == str3: " + String(str1 == str3))
print("str1 == str2: " + String(str1 == str2))
print("str2 == str3: " + String(str2 == str3))
# now this is definitely different from java
#  == in swift will compare 'what's expected'
#  we know what to expect when we compare words
#      numbers, booleans, etc. we DON'T know how
#      to compare 'custom' objects
```
When Java wants to compare (non-custom) objects, it must use the equals() function:
```java
System.out.println("\nComparing Strings with str1.equals(str2): ");
System.out.println("str1 = " + str1 + ", str2 = " + str2 + ", str3 = " + str3);
System.out.println("str1.equals(str3): " + (str1.equals(str3)));
System.out.println("str1.equals(str2): " + (str1.equals(str2)));
System.out.println("str2.equals(str3): " + (str2.equals(str3)));
```
What about custom objects? Custom objects' variables can be compared on their own:
*Java, line 3*
```java
System.out.println("cabbage5.weight = " + cabbage5.weight);
System.out.println("cabbage2.weight = " + cabbage2.weight);
System.out.println("cabbage2.weight == cabbage5.weight: " + (cabbage2.weight == cabbage5.weight));
```
*Swift, line 3*
```python
print("cabbage5.weight = " + String(cabbage5.weight))
print("cabbage2.weight = " + String(cabbage2.weight))
print("cabbage2.weight == cabbage5.weight: " + String(cabbage2.weight == cabbage5.weight))
```
But to compare the whole object, one would need to override equals() in Java and == (or ===) in Swift:
*Java*
```java
public boolean equals(Object other){
    if(!(other instanceof Cabbage))
        return false;
    else{      
        Cabbage otherObj = (Cabbage) other;
        return this.weight == otherObj.weight && this.fresh == otherObj.fresh;
    }
}
```
*Swift*
```python
static func == (lhs: Cabbage, rhs: Cabbage) -> Bool{
    return lhs.weight == rhs.weight && lhs.fresh == rhs.fresh
}
```
Note that Swift requires you to declare the new == as static. Every object of Cabbage has the **same** == function; if they didn't, we'd have to figure out a new way to compare them.

Important takeaway: when creating new classes/ objects, know what kind of comparisons can be made with them and understand how to create a custom compare (overriden function) if needed. It's also important to know that if one decides to override a comparison function, they will not be able to use it for anything but that (aka. might lose compare refernce ability). 


<br></br>
### Practice Your Knowledge!
#### Q1 (Q5 swift)
```java
System.out.println("\nComparing objects with == (fixed): ");
System.out.println("Cabbage cabbage5 = cabbage2;");
Cabbage cabbage5 = cabbage2;
System.out.println("cabbage2 == cabbage 5: " + (cabbage2 == cabbage5));
// Q1: what will this output? what does this mean?
```
Answer:
> This will print out True, because cabbage5 references the same object as cabbage2. They both point to the same address of a cabbage object.
#### Q2 (Q6 swift)
```java
System.out.println("cabbage5.weight = 5;");
cabbage5.weight = 5;
System.out.println("cabbage5.weight = " + cabbage5.weight);
System.out.println("cabbage2.weight = " + cabbage2.weight);
System.out.println("cabbage2.weight == cabbage5.weight: " + (cabbage2.weight == cabbage5.weight));
// Q2: based on your conclusion from Q1, what will these two statements output?
```
Answer:
> The outputs are: 5, 5, and True. Since the objects are now references to a singular object, any changes made by one reference (aka. cabbage2 or cabbage5) are 'also changed' in the other reference (it's not a *true* 'also change,' as they are same object with two different names).
#### Q3 (not in the Swift code examples)
```java
// fortunately we can use our knowledge of overriding
//      to make this function do what we want it too
//      (see the overriden function in Cabbage class)
// Q3: a. what will these lines output if the function isn't overriden?
//     b. will any print true? why?
System.out.println("\nComparing Objects with overidden .equals(): ");
System.out.println("cabbage1.equals(cabbage3): " + (cabbage1.equals(cabbage3)));
System.out.println("cabbage1.equals(cabbage2): " + (cabbage1.equals(cabbage2)));
System.out.println("cabbage1.equals(cabbage4): " + (cabbage1.equals(cabbage4)));
System.out.println("cabbage2.equals(cabbage3): " + (cabbage2.equals(cabbage3)));
System.out.println("cabbage2.equals(cabbage4): " + (cabbage2.equals(cabbage4)));
System.out.println("cabbage3.equals(cabbage4): " + (cabbage3.equals(cabbage4)));
System.out.println("cabbage2.equals(cabbage5): " + (cabbage2.equals(cabbage5)));
```
Answer:
> a. All of them will output false except the last line. Before overriding the function, these are just comparing references, and none of them are the same reference except cabbage5 and cabbage2.

> b. Since cabbage5 and cabbage2 are references, and equals() tests for references, it will print True. 
#### Q4 (Q7 swift)
```java
System.out.println("cabbage2.equals(cabbage5): " + (cabbage2.equals(cabbage5)));
// Q4: what will cabbage2.equals(cabbage5) output if equals() IS overriden?
```
Answer:
> Since cabbage5 and cabbage2 are references, the last line will print True no matter what equals() is comparing (given that equals() is either comparing references or is being overriden to compare specific variables between objects of the same type). 
#### Q8 (not in the Java code examples)
```python
# bonus round
# Q8: what will the following lines output
print("'Primitive' and String comparisons with ===:")
print("i = " + String(i) + ", j = " + String(j) + ", k = " + String(k))
print("i === j: " + String(i === j))
print("i === k: " + String(i === k))
print("j === k: " + String(j === k))
print("str1 = " + str1 + ", str2 = " + str2 + ", str3 = " + str3)
print("str1 === str3: " + String(str1 === str3))
print("str1 === str2: " + String(str1 === str2))
print("str2 === str3: " + String(str2 === str3))
# hint: === tests for same reference or 'identity'
```
Answer:
> These statements will fail when compiling! The === only compares references! Swift's 'primitive' types don't have the ability to 'reference' one another. This is a perk of Swift as compared to Java because of the simplicity. Java has primitive types and classes for their primitive types: ex. primitive int vs. class version Integer. Swift eliminates the complexity of this.
The java 'equivalent' of Q8's 'conundrum' is:
```java
System.out.println("Primitive Comparisons with equals():");
System.out.println("i = " + i + ", j = " + j + ", k = " + k);
System.out.println("i.equals(j): " + (i.equals(j)));
System.out.println("i.equals(k): " + (i.equals(k)));
System.out.println("k.equals(j): " + (k.equals(j)));
```
'Equivalent' meaning: primitive types do not have functions that can be performed on them, so int.equals(int) is illegal (just like int === int is illegal in Swift).










