# Cohesion

- Cohesion is a measure of how related and focused the responsibilities of a module are.
- A module is,
    - **Strongly cohesive** if it performs a single task or a group of related tasks.
    - **Weakly cohesive** if it performs multiple unrelated tasks.

## Strong Cohesion

```java
public class Circle {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double getArea() {
        return Math.PI * radius * radius;
    }

    public double getCircumference() {
        return 2 * Math.PI * radius;
    }
}
```

## Weak Cohesion

```java
public class Magic {
    public void printDocument(String document) {
        // ...
    }

    public void sendEmail(String email) {
        // ...
    }

    public void openBrowser(String url) {
        // ...
    }
}
```

# Coupling

- Coupling is a measure of how dependent a module is on other modules.
- A module is,
    - **Loosely coupled** if it is independent of other modules.
    - **Tightly coupled** if it is highly dependent on other modules.

## Loose Coupling

```java
class Report {
    public static Report fromFile(String path) {
        // ...
    }

    public String toDocument() {
        // ...
    }
}

class Printer {
    public static void print(String document) {
        // ...
    }
}

class Main {
    public static void main(String[] args) {
        Report report = Report.fromFile("report.rep");
        Printer.print(report.toDocument());
    }
}
```

## Tight Coupling

```java
class Report {
  public static Report fromFile(String path) {
    // ...
  }

  public void print() {
    Printer.print(this);
  }

  public String toDocument() {
    // ...
  }
}

class Printer {
  public static void print(Report report) {
    String document = report.toDocument();
    // ...
  }
}

class Main {
  public static void main(String[] args) {
    Report report = Report.fromFile("report.rep");
    report.print();
  }
}
```
