## Sure! Let's create a series of examples using Java Streams and Lambda expressions to perform various operations on a list of `Employee` objects. We'll cover `Collectors`, `groupingBy`, `filter`, `max`, `min`, `sorting`, `reverse`, `limit`, `skip`, and `flatMap`.

### Employee Class
First, let's define the `Employee` class:

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Map;
import java.util.stream.Collectors;
import java.util.Comparator;
import java.util.Optional;

class Employee {
    private int id;
    private String name;
    private String department;
    private double salary;

    public Employee(int id, String name, String department, double salary) {
        this.id = id;
        this.name = name;
        this.department = department;
        this.salary = salary;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getDepartment() {
        public double getSalary() {
        return salary;
    }

    @Override
    public String toString() {
        return "Employee{id=" + id + ", name='" + name + "', department='" + department + "', salary=" + salary + "}";
    }
}
```

### Sample Data
Let's create a list of employees:

```java
List<Employee> employees = new ArrayList<>();
employees.add(new Employee(1, "Alice", "HR", 70000));
employees.add(new Employee(2, "Bob", "IT", 80000));
employees.add(new Employee(3, "Charlie", "Finance", 90000));
employees.add(new Employee(4, "David", "IT", 75000));
employees.add(new Employee(5, "Eve", "HR", 85000));
```

### Examples

#### 1. Collectors
Collect all employee names into a list:

```java
List<String> employeeNames = employees.stream()
    .map(Employee::getName)
    .collect(Collectors.toList());
System.out.println(employeeNames);
```

#### 2. GroupingBy
Group employees by department:

```java
Map<String, List<Employee>> employeesByDepartment = employees.stream()
    .collect(Collectors.groupingBy(Employee::getDepartment));
System.out.println(employeesByDepartment);
```

#### 3. Filter
Filter employees with a salary greater than 75000:

```java
List<Employee> highEarners = employees.stream()
    .filter(e -> e.getSalary() > 75000)
    .collect(Collectors.toList());
System.out.println(highEarners);
```

#### 4. Max
Find the employee with the highest salary:

```java
Optional<Employee> highestEarner = employees.stream()
    .max(Comparator.comparingDouble(Employee::getSalary));
highestEarner.ifPresent(System.out::println);
```

#### 5. Min
Find the employee with the lowest salary:

```java
Optional<Employee> lowestEarner = employees.stream()
    .min(Comparator.comparingDouble(Employee::getSalary));
lowestEarner.ifPresent(System.out::println);
```

#### 6. Sorting
Sort employees by salary:

```java
List<Employee> sortedBySalary = employees.stream()
    .sorted(Comparator.comparingDouble(Employee::getSalary))
    .collect(Collectors.toList());
System.out.println(sortedBySalary);
```

#### 7. Reverse Sorting
Sort employees by salary in reverse order:

```java
List<Employee> sortedBySalaryDesc = employees.stream()
    .sorted(Comparator.comparingDouble(Employee::getSalary).reversed())
    .collect(Collectors.toList());
System.out.println(sortedBySalaryDesc);
```

#### 8. Limit
Get the top 3 highest earners:

```java
List<Employee> topEarners = employees.stream()
    .sorted(Comparator.comparingDouble(Employee::getSalary).reversed())
    .limit(3)
    .collect(Collectors.toList());
System.out.println(topEarners);
```

#### 9. Skip
Skip the first 2 employees and collect the rest:

```java
List<Employee> skippedEmployees = employees.stream()
    .skip(2)
    .collect(Collectors.toList());
System.out.println(skippedEmployees);
```

#### 10. FlatMap
Assume each employee has a list of projects. Flatten the list of projects:

```java
class Project {
    private String name;

    public Project(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return name;
    }
}

class EmployeeWithProjects extends Employee {
    private List<Project> projects;

    public EmployeeWithProjects(int id, String name, String department, double salary, List<Project> projects) {
        super(id, name, department, salary);
        this.projects = projects;
    }

    public List<Project> getProjects() {
        return projects;
    }
}

List<EmployeeWithProjects> employeesWithProjects = new ArrayList<>();
employeesWithProjects.add(new EmployeeWithProjects(1, "Alice", "HR", 70000, List.of(new Project("Project A"), new Project("Project B"))));
employeesWithProjects.add(new EmployeeWithProjects(2, "Bob", "IT", 80000, List.of(new Project("Project C"))));
employeesWithProjects.add(new EmployeeWithProjects(3, "Charlie", "Finance", 90000, List.of(new Project("Project D"), new Project("Project E"))));

List<Project> allProjects = employeesWithProjects.stream()
    .flatMap(e -> e.getProjects().stream())
    .collect(Collectors.toList());
System.out.println(allProjects);
```

These examples cover various operations using Java Streams and Lambda expressions. Feel free to ask if you have any questions or need further assistance!


You can use Java Streams and Lambda expressions to count the occurrences of each character in a string. Here's an example:

```java
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

public class CharacterCount {
    public static void main(String[] args) {
        String input = "hello world";

        Map<Character, Long> characterCount = input.chars()
            .mapToObj(c -> (char) c)
            .collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));

        System.out.println(characterCount);
    }
}
```

### Explanation:
- **input.chars()**: Converts the string into an IntStream of character codes.
- **mapToObj(c -> (char) c)**: Maps each character code to a Character object.
- **collect(Collectors.groupingBy(Function.identity(), Collectors.counting()))**: Groups the characters by themselves and counts the occurrences of each character.

This will output a map with each character and its count:

```
{ =1, r=1, d=1, e=1, h=1, l=3, o=2, w=1}
```

Feel free to ask if you have any questions or need further assistance!


## Sure! Here's an example of using Java Lambda expressions with a `LinkedHashMap`. We'll create a `LinkedHashMap`, populate it with some data, and then use lambda expressions to perform various operations.

### Example: Using Lambda Expressions with LinkedHashMap

```java
import java.util.LinkedHashMap;
import java.util.Map;

public class LinkedHashMapExample {
    public static void main(String[] args) {
        // Create a LinkedHashMap and populate it with some data
        LinkedHashMap<String, Integer> map = new LinkedHashMap<>();
        map.put("Alice", 30);
        map.put("Bob", 25);
        map.put("Charlie", 35);
        map.put("David", 28);

        // Print the original map
        System.out.println("Original LinkedHashMap:");
        map.forEach((key, value) -> System.out.println(key + ": " + value));

        // Filter entries with values greater than 28
        System.out.println("\nFiltered LinkedHashMap (values > 28):");
        map.entrySet().stream()
            .filter(entry -> entry.getValue() > 28)
            .forEach(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));

        // Sort the map by values
        System.out.println("\nSorted LinkedHashMap by values:");
        map.entrySet().stream()
            .sorted(Map.Entry.comparingByValue())
            .forEach(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));

        // Find the entry with the maximum value
        System.out.println("\nEntry with the maximum value:");
        map.entrySet().stream()
            .max(Map.Entry.comparingByValue())
            .ifPresent(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));

        // Find the entry with the minimum value
        System.out.println("\nEntry with the minimum value:");
        map.entrySet().stream()
            .min(Map.Entry.comparingByValue())
            .ifPresent(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));
    }
}
```

### Explanation:
- **map.forEach((key, value) -> System.out.println(key + ": " + value))**: Prints all entries in the `LinkedHashMap`.
- **filter(entry -> entry.getValue() > 28)**: Filters entries with values greater than 28.
- **sorted(Map.Entry.comparingByValue())**: Sorts the entries by their values.
- **max(Map.Entry.comparingByValue())**: Finds the entry with the maximum value.
- **min(Map.Entry.comparingByValue())**: Finds the entry with the minimum value.

This example demonstrates how to use lambda expressions and streams to perform various operations on a `LinkedHashMap`.

Feel free to ask if you have any questions or need further assistance!

## Sure! Here's a Java code snippet that uses lambda expressions to find and print the first non-repeating character in a string:

```java
import java.util.LinkedHashMap;
import java.util.Map;
import java.util.function.Function;
import java.util.stream.Collectors;

public class FirstNonRepeatingChar {
    public static void main(String[] args) {
        String input = "swiss";
        
        Character result = input.chars()
            .mapToObj(c -> (char) c)
            .collect(Collectors.groupingBy(Function.identity(), LinkedHashMap::new, Collectors.counting()))
            .entrySet()
            .stream()
            .filter(entry -> entry.getValue() == 1)
            .map(Map.Entry::getKey)
            .findFirst()
            .orElse(null);
        
        System.out.println("First non-repeating character: " + result);
    }
}
```

This code uses a `LinkedHashMap` to maintain the order of characters and `Collectors.groupingBy` to count the occurrences of each character. It then filters the entries to find the first character with a count of 1.

Feel free to try it out! If you have any questions or need further assistance, let me know.


## Here's an example of how you can use `ExecutorService` to print even and odd numbers using two separate threads in Java:

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Semaphore;

public class EvenOddUsingExecutorService {
    private static final int MAX = 10;
    private static final Semaphore evenSemaphore = new Semaphore(1);
    private static final Semaphore oddSemaphore = new Semaphore(0);

    public static void main(String[] args) {
        ExecutorService executorService = Executors.newFixedThreadPool(2);

        Runnable printEven = () -> {
            for (int i = 2; i <= MAX; i += 2) {
                try {
                    evenSemaphore.acquire();
                    System.out.println("Even: " + i);
                    oddSemaphore.release();
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }
        };

        Runnable printOdd = () -> {
            for (int i = 1; i <= MAX; i += 2) {
                try {
                    oddSemaphore.acquire();
                    System.out.println("Odd: " + i);
                    evenSemaphore.release();
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }
        };

        executorService.submit(printEven);
        executorService.submit(printOdd);

        executorService.shutdown();
    }
}
```

In this example:
- Two `Semaphore` objects are used to control the order of execution between the even and odd number printing threads.
- The `evenSemaphore` is initialized with a permit of 1, allowing the even thread to start first.
- The `oddSemaphore` is initialized with a permit of 0, so the odd thread waits until the even thread releases a permit.
- The `ExecutorService` is used to manage the threads.

This ensures that the even and odd numbers are printed in the correct order. Feel free to try it out and let me know if you have any questions!

## Here's a simple example of how you can use two threads to print even and odd numbers in Java:

```java
public class EvenOddThread {
    private static final int MAX = 10;
    private static final Object lock = new Object();
    private static boolean evenTurn = true;

    public static void main(String[] args) {
        Thread evenThread = new Thread(new EvenPrinter());
        Thread oddThread = new Thread(new OddPrinter());

        evenThread.start();
        oddThread.start();
    }

    static class EvenPrinter implements Runnable {
        @Override
        public void run() {
            for (int i = 2; i <= MAX; i += 2) {
                synchronized (lock) {
                    while (!evenTurn) {
                        try {
                            lock.wait();
                        } catch (InterruptedException e) {
                            Thread.currentThread().interrupt();
                        }
                    }
                    System.out.println("Even: " + i);
                    evenTurn = false;
                    lock.notify();
                }
            }
        }
    }

    static class OddPrinter implements Runnable {
        @Override
        public void run() {
            for (int i = 1; i <= MAX; i += 2) {
                synchronized (lock) {
                    while (evenTurn) {
                        try {
                            lock.wait();
                        } catch (InterruptedException e) {
                            Thread.currentThread().interrupt();
                        }
                    }
                    System.out.println("Odd: " + i);
                    evenTurn = true;
                    lock.notify();
                }
            }
        }
    }
}
```

In this example:
- Two threads (`evenThread` and `oddThread`) are created to print even and odd numbers, respectively.
- A shared `lock` object is used to synchronize the threads.
- The `evenTurn` boolean variable ensures that the threads take turns printing numbers.
- The `synchronized` block and `wait()`/`notify()` methods are used to manage the coordination between the threads.

Feel free to try it out and let me know if you have any questions!


## How to design unique, consitnent, durable, checksum keys in java

Designing unique, consistent, durable, and checksum keys in Java involves several steps. Here’s a structured approach to achieve this:

### 1. **Unique Keys**

To ensure uniqueness, you can use UUIDs (Universally Unique Identifiers). Java provides a built-in class for generating UUIDs.

```java
import java.util.UUID;

public class UniqueKeyGenerator {
    public static String generateUUID() {
        return UUID.randomUUID().toString();
    }

    public static void main(String[] args) {
        String uniqueKey = generateUUID();
        System.out.println("Unique Key: " + uniqueKey);
    }
}
```

### 2. **Consistent Keys**

Consistency can be achieved by following a specific format or pattern for your keys. For example, you can use a combination of a prefix, timestamp, and a unique identifier.

```java
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.UUID;

public class ConsistentKeyGenerator {
    public static String generateConsistentKey() {
        String prefix = "KEY";
        String timestamp = new SimpleDateFormat("yyyyMMddHHmmss").format(new Date());
        String uniqueID = UUID.randomUUID().toString().substring(0, 8);
        return prefix + "_" + timestamp + "_" + uniqueID;
    }

    public static void main(String[] args) {
        String consistentKey = generateConsistentKey();
        System.out.println("Consistent Key: " + consistentKey);
    }
}
```

### 3. **Durable Keys**

Durability can be ensured by storing the keys in a persistent storage like a database or a file system. Here’s an example of storing keys in a file.

```java
import java.io.FileWriter;
import java.io.IOException;
import java.util.UUID;

public class DurableKeyGenerator {
    public static String generateDurableKey() {
        return UUID.randomUUID().toString();
    }

    public static void saveKeyToFile(String key, String filePath) throws IOException {
        try (FileWriter writer = new FileWriter(filePath, true)) {
            writer.write(key + "\n");
        }
    }

    public static void main(String[] args) {
        String durableKey = generateDurableKey();
        System.out.println("Durable Key: " + durableKey);
        try {
            saveKeyToFile(durableKey, "keys.txt");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 4. **Checksum Keys**

To ensure data integrity, you can generate a checksum for your keys using hashing algorithms like SHA-256.

```java
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.util.UUID;

public class ChecksumKeyGenerator {
    public static String generateChecksumKey() throws NoSuchAlgorithmException {
        String key = UUID.randomUUID().toString();
        MessageDigest digest = MessageDigest.getInstance("SHA-256");
        byte[] hash = digest.digest(key.getBytes());
        StringBuilder hexString = new StringBuilder();
        for (byte b : hash) {
            String hex = Integer.toHexString(0xff & b);
            if (hex.length() == 1) hexString.append('0');
            hexString.append(hex);
        }
        return key + "_" + hexString.toString();
    }

    public static void main(String[] args) {
        try {
            String checksumKey = generateChecksumKey();
            System.out.println("Checksum Key: " + checksumKey);
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
        }
    }
}
```

### Summary

By combining these techniques, you can generate keys that are unique, consistent, durable, and include a checksum for data integrity. Here’s a quick recap:

1. **Unique Keys**: Use UUIDs.
2. **Consistent Keys**: Follow a specific format or pattern.
3. **Durable Keys**: Store keys in persistent storage.
4. **Checksum Keys**: Use hashing algorithms to generate checksums.

Would you like more details on any specific part of this process?




## Mono and Flux for File processing

Using Project Reactor's `Flux` and `Mono` for file processing in a reactive way can be very efficient. Here’s an example of how you can use these classes to read and write files in a reactive manner.

### Example: Reading a File with `Flux`

This example demonstrates how to read a file line by line using `Flux`.

```java
import reactor.core.publisher.Flux;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.stream.BaseStream;

public class FileReadingExample {
    public static void main(String[] args) {
        Path path = Paths.get("example.txt");

        Flux<String> fileLines = Flux.using(
            () -> Files.lines(path),
            Flux::fromStream,
            BaseStream::close
        );

        fileLines.subscribe(
            line -> System.out.println("Read line: " + line),
            error -> System.err.println("Error: " + error),
            () -> System.out.println("File reading completed.")
        );
    }
}
```

### Example: Writing to a File with `Mono`

This example demonstrates how to write a string to a file using `Mono`.

```java
import reactor.core.publisher.Mono;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;
import java.util.Collections;

public class FileWritingExample {
    public static void main(String[] args) {
        Path path = Paths.get("output.txt");
        String content = "Hello, World!";

        Mono<Void> writeFile = Mono.fromRunnable(() -> {
            try {
                Files.write(path, Collections.singleton(content), StandardOpenOption.CREATE, StandardOpenOption.APPEND);
            } catch (Exception e) {
                throw new RuntimeException(e);
            }
        });

        writeFile.subscribe(
            null,
            error -> System.err.println("Error: " + error),
            () -> System.out.println("File writing completed.")
        );
    }
}
```

### Explanation

1. **Reading a File with `Flux`**:
   - `Flux.using`: This method is used to create a `Flux` from a resource that needs to be cleaned up after use. In this case, it’s a stream of lines from a file.
   - `Files.lines(path)`: This method returns a stream of lines from the file.
   - `Flux::fromStream`: Converts the stream into a `Flux`.
   - `BaseStream::close`: Ensures the stream is closed after use.
   - `subscribe`: Subscribes to the `Flux` to process each line, handle errors, and signal completion.

2. **Writing to a File with `Mono`**:
   - `Mono.fromRunnable`: Creates a `Mono` from a `Runnable` that writes content to a file.
   - `Files.write`: Writes the content to the file.
   - `subscribe`: Subscribes to the `Mono` to handle completion and errors.

By using `Flux` and `Mono`, you can handle file processing in a reactive and efficient manner. Would you like more details on any specific part of this process?


## parellel and parellel stream file processing example

Using parallel streams in Java can significantly improve the performance of file processing tasks by leveraging multiple CPU cores. Here’s an example of how to use parallel streams for file processing:

### Example: Reading a File with Parallel Streams

This example demonstrates how to read a file line by line using parallel streams.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.Stream;

public class ParallelFileReadingExample {
    public static void main(String[] args) {
        Path path = Paths.get("example.txt");

        try (Stream<String> lines = Files.lines(path)) {
            List<String> processedLines = lines.parallel()
                                               .map(line -> processLine(line))
                                               .collect(Collectors.toList());

            processedLines.forEach(System.out::println);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static String processLine(String line) {
        // Simulate processing
        return line.toUpperCase();
    }
}
```

### Example: Writing to a File with Parallel Streams

This example demonstrates how to write multiple lines to a file using parallel streams.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.nio.file.StandardOpenOption;
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class ParallelFileWritingExample {
    public static void main(String[] args) {
        Path path = Paths.get("output.txt");
        List<String> lines = Arrays.asList("Hello, World!", "Parallel Streams in Java", "File Processing Example");

        List<String> processedLines = lines.parallelStream()
                                           .map(line -> processLine(line))
                                           .collect(Collectors.toList());

        try {
            Files.write(path, processedLines, StandardOpenOption.CREATE, StandardOpenOption.APPEND);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static String processLine(String line) {
        // Simulate processing
        return line.toUpperCase();
    }
}
```

### Explanation

1. **Reading a File with Parallel Streams**:
   - `Files.lines(path)`: Reads all lines from the file as a stream.
   - `lines.parallel()`: Converts the stream to a parallel stream.
   - `map(line -> processLine(line))`: Processes each line in parallel.
   - `collect(Collectors.toList())`: Collects the processed lines into a list.
   - `processedLines.forEach(System.out::println)`: Prints each processed line.

2. **Writing to a File with Parallel Streams**:
   - `lines.parallelStream()`: Converts the list of lines to a parallel stream.
   - `map(line -> processLine(line))`: Processes each line in parallel.
   - `collect(Collectors.toList())`: Collects the processed lines into a list.
   - `Files.write(path, processedLines, StandardOpenOption.CREATE, StandardOpenOption.APPEND)`: Writes the processed lines to the file.

### Benefits of Parallel Streams

- **Performance**: Parallel streams can significantly improve performance by utilizing multiple CPU cores.
- **Simplicity**: Parallel streams provide a simple and declarative way to process data in parallel.

By using parallel streams, you can efficiently process large files in Java. Would you like more details on any specific part of this process?

## Callable and Runnable Example

Sure! In Java, both `Callable` and `Runnable` are interfaces used to represent tasks that can be executed by a thread or an executor service. However, they have some differences:

- **`Runnable`**: This interface has a single method `run()` that does not return a result and cannot throw a checked exception.
- **`Callable`**: This interface has a single method `call()` that returns a result and can throw a checked exception.

Here's a simple example to illustrate both:

### Runnable Example
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class RunnableExample {
    public static void main(String[] args) {
        Runnable task = () -> {
            System.out.println("Executing Runnable Task");
        };

        ExecutorService executor = Executors.newSingleThreadExecutor();
        executor.submit(task);
        executor.shutdown();
    }
}
```

### Callable Example
```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class CallableExample {
    public static void main(String[] args) {
        Callable<String> task = () -> {
            return "Executing Callable Task";
        };

        ExecutorService executor = Executors.newSingleThreadExecutor();
        Future<String> future = executor.submit(task);

        try {
            String result = future.get();
            System.out.println(result);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            executor.shutdown();
        }
    }
}
```

In the `Runnable` example, the task simply prints a message. In the `Callable` example, the task returns a string, and we retrieve this result using the `Future` object.

Do you have any specific use cases in mind for these interfaces?


## submit , invoke example

Sure! Let's look at examples of using `submit` and `invoke` methods with `ExecutorService` in Java.

### Using `submit`
The `submit` method is used to submit a task for execution and returns a `Future` representing the pending result of the task.

```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class SubmitExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newSingleThreadExecutor();

        Callable<String> task = () -> {
            return "Task executed using submit";
        };

        Future<String> future = executor.submit(task);

        try {
            String result = future.get();
            System.out.println(result);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            executor.shutdown();
        }
    }
}
```

### Using `invokeAll`
The `invokeAll` method is used to execute a collection of tasks and returns a list of `Future` objects representing the results of all tasks.

```java
import java.util.Arrays;
import java.util.List;
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class InvokeAllExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);

        List<Callable<String>> tasks = Arrays.asList(
            () -> "Task 1 executed using invokeAll",
            () -> "Task 2 executed using invokeAll",
            () -> "Task 3 executed using invokeAll"
        );

        try {
            List<Future<String>> futures = executor.invokeAll(tasks);

            for (Future<String> future : futures) {
                System.out.println(future.get());
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            executor.shutdown();
        }
    }
}
```

### Using `invokeAny`
The `invokeAny` method is used to execute a collection of tasks and returns the result of one of the successfully completed tasks (the first one to complete successfully).

```java
import java.util.Arrays;
import java.util.List;
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class InvokeAnyExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);

        List<Callable<String>> tasks = Arrays.asList(
            () -> "Task 1 executed using invokeAny",
            () -> "Task 2 executed using invokeAny",
            () -> "Task 3 executed using invokeAny"
        );

        try {
            String result = executor.invokeAny(tasks);
            System.out.println(result);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            executor.shutdown();
        }
    }
}
```

In these examples:
- `submit` is used to submit a single task and get its result.
- `invokeAll` is used to execute multiple tasks and get the results of all tasks.
- `invokeAny` is used to execute multiple tasks and get the result of the first successfully completed task.

Do you have any specific scenarios where you plan to use these methods?

## Future vs Completable Future  example

Sure! `Future` and `CompletableFuture` are both used for asynchronous programming in Java, but `CompletableFuture` provides more capabilities and flexibility. Here are examples to illustrate the differences:

### Using `Future`
`Future` is a simple interface that represents the result of an asynchronous computation. It provides methods to check if the computation is complete, to wait for its completion, and to retrieve the result.

```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class FutureExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newSingleThreadExecutor();

        Callable<String> task = () -> {
            Thread.sleep(1000);
            return "Task executed using Future";
        };

        Future<String> future = executor.submit(task);

        try {
            // some other work
            String result = future.get(); // Blocking call
            System.out.println(result);
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        } finally {
            executor.shutdown();
        }
    }
}
```

### Using `CompletableFuture`
`CompletableFuture` is a more advanced class that implements `Future` and `CompletionStage`. It provides a wide range of methods for composing, combining, and handling asynchronous tasks.

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutionException;

public class CompletableFutureExample {
    public static void main(String[] args) {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            return "Task executed using CompletableFuture";
        });

        future.thenAccept(result -> {
            System.out.println(result);
        }).exceptionally(ex -> {
            ex.printStackTrace();
            return null;
        });

        // Do some other work
        try {
            future.get(); // Blocking call to ensure the main thread waits for the completion
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }
    }
}
```

### Key Differences:
1. **Flexibility**: `CompletableFuture` provides more methods for chaining and combining tasks, handling exceptions, and more.
2. **Non-blocking**: `CompletableFuture` methods like `thenAccept` and `exceptionally` allow you to handle results and exceptions without blocking the main thread.
3. **Completion**: `CompletableFuture` can be manually completed using methods like `complete` and `completeExceptionally`.

Do you have a specific use case in mind where you need to choose between `Future` and `CompletableFuture`?

