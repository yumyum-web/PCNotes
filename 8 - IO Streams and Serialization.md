# I/O Streams

## Streams

An object that either delivers data to its destination or takes data from a source.

### Types of Streams in Java IO

- Input/Output
    - Input stream: a stream that provides input to a program
    - Output stream: a stream that accepts output from a program
- Processing/Ordinary
    - Processing stream: a stream that processes data
    - Ordinary stream: a stream that reads or writes data
- Character/Byte
    - Character-oriented stream: a stream that reads or writes characters
    - Byte-oriented stream: a stream that reads or writes bytes

### Stream Classes

- **InputStream**: abstract class for all input streams
    - **FileInputStream**: reads data from a file
    - **ObjectInputStream**: reads objects from an input stream
- **OutputStream**: abstract class for all output streams
    - **FileOutputStream**: writes data to a file
    - **ObjectOutputStream**: writes objects to an output stream


- **Reader**: abstract class for all readers
    - **FileReader**: reads characters from a file
    - **BufferedReader**: reads text from a character-input stream
- **Writer**: abstract class for all writers
    - **FileWriter**: writes characters to a file
    - **BufferedWriter**: writes text to a character-output stream

## File Processing

Typical file processing steps:

- Open a file
- Check if the file is open
- Read or write data
- Close the file

### Buffering

#### No Buffering

- Reads or writes one byte at a time with a little delay for each byte
- High overhead

```java
/*
 *      Writing to a Text File (No Buffering)
 */

import java.io.*;

public class WriteToFile {
    public static void main(String[] args) {
        try {
            FileWriter writer = new FileWriter("output.txt");
            writer.write("Hello, World!");
            writer.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

#### Buffered I/O

- Reads or writes a block of bytes at a time
- Reduces overhead

```java
/*
 *      Writing to a Text File (Buffered I/O)
 */

import java.io.*;

public class WriteToFile {
    public static void main(String[] args) {
        try {
            BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"));
            writer.write("Hello, World!");
            writer.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

```java
/*
 *      Reading from a Text File (Buffered I/O)
 */

import java.io.*;

public class ReadFromFile {
    public static void main(String[] args) {
        try {
            BufferedReader reader = new BufferedReader(new FileReader("output.txt"));
            String line = reader.readLine();
            System.out.println(line);
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

# Serialization

- Serialization is the process of converting an object into a linear format.
- Mainly used for:
    - Save the state of an object
    - Save data to a file
    - Send an object over a network

> Saving the state of an object can be done using,
> 
> - Serialized objects: the JVM automatically saves the state of an object
> - Plain text: saving the state of an object as a parsable text
>
> Serialization is much safer and easier to use than plain text.

- Serialization saves the entire object graph.
- Either the entire object graph is serialized correctly, or serialization fails.
- An object can not be serialized if,
    - It has not implemented serializable
    - It has a non-serializable instance variable

## transient Keyword

- The `transient` keyword is used to prevent serialization of an instance variable.
- When deserializing `transient` variables will be set to,
  - default values for primitive types
  - `null` for reference types

## Examples

```java
/*
 *      Serializing an Object
 */
 
import java.io.*;

class Person implements Serializable {
    private String name;
    private transient int nic;
    
    public Person(String name) {
        this.name = name;
        this.nic = 0;
    }
}

public class SerializeObject {
    public static void main(String[] args) {
        try {
            Person person = new Person("John");
            FileOutputStream file = new FileOutputStream("person.ser");
            ObjectOutputStream out = new ObjectOutputStream(file);
            out.writeObject(person);
            out.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

```java
/*
 *      Deserializing an Object
 */

import java.io.*;

public class DeserializeObject {
    public static void main(String[] args) {
        try {
            FileInputStream file = new FileInputStream("person.ser");
            ObjectInputStream in = new ObjectInputStream(file);
            Person person = (Person) in.readObject();
            in.close();
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

## Recap

- Chain streams can be used on their own or with connection streams.
- Buffered I/O is more efficient than unbuffered I/O.
- Classes are not serializable by default.
- The `transient` keyword is used to prevent serialization of an instance variable.
- When deserializing, object constructor is not called.
- A subclass of a serializable class is also serializable.
- If a superclass is not serializable, its no-arg constructor will be called when deserializing.
- `flush()` method is used to write any buffered data to the file.
