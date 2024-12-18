`In Java, a record is a special kind of class introduced in Java 14 as a preview feature and made stable in Java 16. 
It is designed to act as a data carrier or data transfer object (DTO), which is often used to hold immutable data with minimal boilerplate code. `


A record is essentially a class that automatically provides implementations for key methods, such as:

- equals()
- hashCode()
- toString()
- Getters for all fields
- A constructor to initialize the fields
  
## Key Features of Records:
**Compact Syntax:** Records reduce boilerplate code by automatically generating most of the code you'd typically write for a POJO (Plain Old Java Object), like getters, equals(), hashCode(), and toString().

**Immutability:** By default, fields in a record are final and cannot be changed once they are initialized (making the record immutable).

**Implicit equals(), hashCode(), and toString() Methods:** Java automatically generates these methods based on the fields defined in the record.

Syntax:
```java

public record Person(String name, int age) {
    // You can optionally add additional methods if needed
}
```
In this example:

Person is a record with two fields: name and age.

The constructor for Person is automatically generated, and the fields are implicitly final.

The equals(), hashCode(), and toString() methods are automatically generated based on the fields (name and age).

Using Records:
```java

public class RecordExample {
    public static void main(String[] args) {
        // Create a record instance
        Person person = new Person("Alice", 30);
        
        // Access record fields using getters
        System.out.println("Name: " + person.name());  // Using getter for name
        System.out.println("Age: " + person.age());    // Using getter for age

        // `toString()` method is automatically generated
        System.out.println(person);  // Output: Person[name=Alice, age=30]

        // `equals()` and `hashCode()` are automatically generated
        Person person2 = new Person("Alice", 30);
        System.out.println(person.equals(person2));  // Output: true
        System.out.println(person.hashCode() == person2.hashCode());  // Output: true
    }
}
```
### Advantages of Using Records:

**Reduced Boilerplate:**  Records eliminate the need for writing standard code like constructors, getters, equals(), hashCode(), and toString().

**Immutability by Default:** Fields in a record are final, ensuring immutability.

**Clear Intent:** Records make it clear that the class is meant to be used as a simple data carrier.

### Limitations:
**Immutability:** Fields in a record are final and cannot be modified after creation. This is a limitation if you need mutable objects.

**Inheritance:** Records cannot extend other classes because they implicitly extend java.lang.Record. However, they can implement interfaces.

**No Setter Methods:** Since fields are final, setter methods are not provided.

Example with a More Complex Record:
```java

public record Book(String title, String author, int yearPublished) {
    // Additional methods can be added if needed
    public String description() {
        return title + " by " + author + " (" + yearPublished + ")";
    }
}
```
You can use it like this:

```java

public class RecordExample {
    public static void main(String[] args) {
        Book book = new Book("Java Basics", "John Doe", 2020);
        System.out.println(book.description());  // Output: Java Basics by John Doe (2020)
    }
}
```
In this example, Book is a record that holds details of a book and also includes an additional method description().

### Conclusion:
Java records are a powerful feature that simplifies the creation of data-centric classes. They are especially useful in scenarios where you need an object to hold a fixed set of data, but you don't want to manually write the common boilerplate code typically required for such classes.
