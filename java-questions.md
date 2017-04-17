## The questions I would ask to interview a JVM engineer

### Chapter 1

- How is char encoded in Java?
	- https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html
    - https://en.wikipedia.org/wiki/UTF-16

- How does class String's public method intern() behave?
	- Java’s String class privately maintains a pool of string objects, where string literals are automatically interned. When the intern() method is invoked on a String object it looks the string contained by this String object in the pool, if the string is found there then the String object from the pool is returned. Otherwise, this String object is added to the pool and a reference to this String object is returned.
    
- How can it be used to cause a memory leak before Java 8?
	- Before Java 8, interned strings are stored in the permGen, which is never GCed.