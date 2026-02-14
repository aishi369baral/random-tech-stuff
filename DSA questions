What is an array? 
An array is a contiguous block of memory, used to store elements of the same type which can be accessed via an index.

Why is array access O(1)?
Because arrays use contiguous memory, allowing direct address calculation using index.

What are the disadvantages of arrays?
Fixed size,
Not suitable for dynamic data,
Costly insertion/deletion (O(n)due to shifting).

What is List<T>?
Lists are dynamic collections in .Net that internally uses an array and automatically resizes when needed.

Difference between Array and List<T>
Array is fixed size and faster, List<T> is dynamic and flexible with slight overhead.

Is List<T> internally an array?
Yes. It internally maintains an array and resizes by creating a larger array and copying the elements.

Time Complexity of List<T>.Add()
Amortized O(1)
During resizing O(n) worst case

Why is List<T> preffered in Asp.net Core Apis?
Because Api Payload sizes are dynamic and not known during execution.

What does "handling request payload collections" mean?
Receiving and processing arrays and lists sent in Http request bodies, typically mapped to List<T>.

Examples of request payload collection in Asp.net core?
JSON arrays in request bodies mapped to List<T> in DTOs.
