# Java Advanced Concepts

## Table of Contents
- [Generics](#generics)
- [Collections Framework](#collections-framework)
- [Multithreading](#multithreading)
- [Lambda Expressions](#lambda-expressions)
- [Stream API](#stream-api)
- [Exception Handling](#exception-handling)

## Generics
```java
// Generic Class Definition
public class Box<T> {
    private T content;          // Generic type parameter

    public Box(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }
}

// Generic Method
public <T, U> void process(T input, U data) {
    // Process different types
}

// Bounded Type Parameters
public class NumberBox<T extends Number> {
    private T number;

    public double sqrt() {
        // Can use Number methods because of bound
        return Math.sqrt(number.doubleValue());
    }
}

// Wildcard Usage
public void printList(List<?> list) {           // Unknown type
public void addNumbers(List<? extends Number>)  // Upper bound
public void addIntegers(List<? super Integer>)  // Lower bound
```

## Collections Framework
```java
// List Examples
List<String> arrayList = new ArrayList<>();     // Dynamic array
arrayList.add("First");
arrayList.add("Second");

List<Integer> linkedList = new LinkedList<>();   // Doubly-linked list
linkedList.add(1);
linkedList.addFirst(0);                         // Special LinkedList method

// Set Examples
Set<String> hashSet = new HashSet<>();          // Unordered, unique
hashSet.add("Apple");
hashSet.add("Apple");                           // Won't add duplicate

Set<String> treeSet = new TreeSet<>();          // Sorted set
treeSet.add("Banana");
treeSet.add("Apple");                           // Will be sorted

// Map Examples
Map<String, Integer> hashMap = new HashMap<>();  // Key-value pairs
hashMap.put("One", 1);
hashMap.put("Two", 2);

// Thread-safe Collections
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Map<String, Integer> concurrentMap = new ConcurrentHashMap<>();

// Custom Sorting
List<Person> people = new ArrayList<>();
Collections.sort(people, (p1, p2) -> 
    p1.getName().compareTo(p2.getName()));      // Custom comparator

// Queue and Deque
Queue<String> queue = new LinkedList<>();       // FIFO structure
queue.offer("First");                           // Add to end
queue.poll();                                   // Remove from front

Deque<String> deque = new ArrayDeque<>();      // Double-ended queue
deque.addFirst("Start");
deque.addLast("End");
```

## Multithreading
```java
// Thread Creation - Method 1
class MyThread extends Thread {
    public void run() {
        // Thread code here
        System.out.println("Thread running");
    }
}

// Thread Creation - Method 2
class MyRunnable implements Runnable {
    public void run() {
        // Thread code here
    }
}

// Thread Usage
Thread thread1 = new MyThread();
thread1.start();                               // Start thread

Thread thread2 = new Thread(new MyRunnable());
thread2.start();

// Lambda Thread
Thread thread3 = new Thread(() -> {
    // Thread code here
});

// Synchronization
public class Counter {
    private int count = 0;

    public synchronized void increment() {      // Method synchronization
        count++;
    }

    public void complexOperation() {
        synchronized(this) {                    // Block synchronization
            // Critical section
        }
    }
}

// Thread Pool
ExecutorService executor = Executors.newFixedThreadPool(5);
executor.submit(() -> {
    // Task to execute
});
executor.shutdown();

// CompletableFuture
CompletableFuture<String> future = CompletableFuture
    .supplyAsync(() -> "Hello")                // Async operation
    .thenApply(s -> s + " World")             // Chain operations
    .thenAccept(System.out::println);         // Handle result
```

## Lambda Expressions
```java
// Functional Interfaces
@FunctionalInterface
interface Calculator {
    int calculate(int x, int y);
}

// Lambda Usage
Calculator add = (x, y) -> x + y;              // Simple lambda
Calculator multiply = (x, y) -> {              // Multi-line lambda
    System.out.println("Multiplying");
    return x * y;
};

// Built-in Functional Interfaces
Predicate<String> isEmpty = s -> s.isEmpty();  // Returns boolean
Consumer<String> print = s -> System.out.println(s);  // Void return
Function<String, Integer> length = s -> s.length();   // Transform
Supplier<Double> random = () -> Math.random();        // No input

// Method References
List<String> names = Arrays.asList("Alice", "Bob");
names.forEach(System.out::println);            // Static method reference
names.forEach(String::toUpperCase);            // Instance method reference
```

## Stream API
```java
// Creating Streams
Stream<String> stream1 = Stream.of("a", "b", "c");
Stream<Integer> stream2 = Arrays.asList(1,2,3).stream();
Stream<Integer> stream3 = Stream.iterate(0, n -> n + 2);

// Intermediate Operations
List<String> processed = names.stream()
    .filter(s -> s.length() > 3)               // Filter elements
    .map(String::toUpperCase)                  // Transform elements
    .distinct()                                // Remove duplicates
    .sorted()                                  // Sort elements
    .peek(System.out::println)                 // Debug view
    .collect(Collectors.toList());             // Terminal operation

// Terminal Operations
boolean allMatch = numbers.stream()
    .allMatch(n -> n > 0);                     // Check all elements

Optional<Integer> min = numbers.stream()
    .min(Integer::compareTo);                  // Find minimum

// Parallel Streams
long count = numbers.parallelStream()
    .filter(n -> n % 2 == 0)
    .count();

// Collectors
Map<String, List<Person>> byDepartment = people.stream()
    .collect(Collectors.groupingBy(Person::getDepartment));

String joined = strings.stream()
    .collect(Collectors.joining(", "));
```

## Exception Handling
```java
// Custom Exception
public class BusinessException extends Exception {
    public BusinessException(String message) {
        super(message);
    }
}

// Try-Catch-Finally
try {
    // Risky code here
    throw new BusinessException("Error");
} catch (BusinessException e) {
    // Handle specific exception
    logger.error("Business error", e);
} catch (Exception e) {
    // Handle general exception
} finally {
    // Always executed
}

// Try-with-Resources
try (FileReader reader = new FileReader("file.txt");
     BufferedReader br = new BufferedReader(reader)) {
    // Resources automatically closed
    String line = br.readLine();
}

// Optional for Null Handling
Optional<String> optional = Optional.of("value");
String result = optional
    .filter(s -> s.length() > 3)
    .map(String::toUpperCase)
    .orElse("default");

// Exception Handling in Streams
List<String> processed = strings.stream()
    .map(s -> {
        try {
            return processString(s);
        } catch (Exception e) {
            return "error";
        }
    })
    .collect(Collectors.toList());
```

