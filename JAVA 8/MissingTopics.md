# 1. Optional Class
Optional is a container object used to represent a value that may or may not be present, avoiding NullPointerExceptions.

Example:

```java
Copy code
Optional<String> name = Optional.ofNullable("John");
System.out.println(name.orElse("Unknown"));  // Prints "John"
```
# 2. New Date and Time API
Java 8 introduced the java.time package to replace Date and Calendar for better handling of date/time.

Example:

```java
Copy code
LocalDate date = LocalDate.now();
System.out.println(date);  // Prints current date, e.g., "2024-11-25"
```
# 3. Collectors Class
Collectors is a utility class for working with streams, allowing operations like grouping, joining, or summarizing data.

Example:

```java
Copy code
List<String> names = Arrays.asList("John", "Jane", "Mike");
String result = names.stream().collect(Collectors.joining(", "));
System.out.println(result);  // Prints "John, Jane, Mike"
```
# 4. Functional Interfaces
Java 8 introduced functional interfaces, which can have only one abstract method. These are used primarily with lambdas.

Example:

```java
Copy code
@FunctionalInterface
interface MyFunction {
    int apply(int a, int b);
}

public class Example {
    public static void main(String[] args) {
        MyFunction sum = (a, b) -> a + b;
        System.out.println(sum.apply(5, 3));  // Prints "8"
    }
}
```




