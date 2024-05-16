# Exception Handling

## What is an Exception?

An exception is an event, which occurs during the execution of a method, that disrupts the normal flow of the program's
instructions. When an exception occurs, the method stops executing and an `Exception` object is created and passed to
the JVM. The JVM then tries to find a handler for the exception. If it finds a handler, the handler executes, otherwise
the program terminates.

## Types of Throwable

<img src="images/Throwable%20Hierarchy.png" alt="Throwable Hierarchy"/>

- **Checked Exception**: a checked exception is an exception that is checked at compile time.

  If a method is capable of causing a checked exception, the method must either,
    - Handle the exception
    - Declare it in its `throws` clause.
- **Unchecked Exception**: an unchecked exception is an exception that is not checked at compile time. These are runtime
  exceptions that usually **represent programming errors.**
- **Error**: an error is a serious problem that a reasonable application **should not try to catch.**

## Exception Handling Keywords

- **try**: a block of code that might throw an exception.
- **catch**: a block of code that handles an exception.
- **finally**: a block of code that always executes, regardless of whether an exception is thrown.
- **throw**: a keyword used to throw an exception.
- **throws**: declares that a method might throw an exception.

```java
import java.io.*;

public class ExceptionHandling {
    private FileReader forth(String[] files) throws IOException {
        try {
            String f = files[3];
            System.out.println(f);
            return new FileReader(f);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Array index out of bounds");
        } finally {
            System.out.println("Forth method executed");
        }
    }
}
```

- A method can throw multiple exceptions.
- There can be multiple `catch` blocks for a single `try` block.
- **`catch` is polymorphic**, meaning a `catch` block can catch an exception obj of the same type or a subtype of the
  exception type.
- `catch` blocks are executed in the **order they are written**, so the most specific exception should be caught first.
- `finally` block is **always executed**, even if the method returns a value in the `try`, `catch` blocks.

## Custom Exceptions

- Define a class that extends `Exception` or `RuntimeException` to create a custom exception.
- The custom exception class should have
    - a constructor that takes no arguments
    - a constructor that takes a `String` message

```java
class MyException extends Exception {
    public MyException() {
        super();
    }

    public MyException(String message) {
        super(message);
    }
}
```

## Closing Resources

- Resources like files, sockets, database connections, etc. should be closed after use.

### Using `finally`

```java
import java.io.*;

public class FinallyBlock {
    public static void main(String[] args) {
        BufferedReader br;
        try {
            br = new BufferedReader(new FileReader("file.txt"));
            System.out.println(br.readLine());
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (br != null) {
                    br.close();
                }
            } catch (IOException _) {
            }
        }
    }
}
```

### Using `try-with-resources`

- Introduced in Java 7.
- Automatically closes resources when the `try` block exits.
- Resources must implement the `AutoCloseable` interface.
- The `close()` method of the resource is called automatically.

```java
import java.io.*;

public class TryWithResources {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
            System.out.println(br.readLine());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## IOException Hierarchy

<img src="images/IOException%20Hierarchy.png" alt="IOException Hierarchy"/>