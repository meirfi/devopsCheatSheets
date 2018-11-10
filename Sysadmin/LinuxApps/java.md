# Java - Understanding Java Garbage Collection
[jvm-hotspot-heap]: images/java-hotspot-heap.png "htop-tree"

![jvm-hotspot][jvm-hotspot-heap]

## Common Heap Related Switches
There are many different command line switches that can be used with Java. This section describes some of the more commonly used switches that are also used in this OBE.

| Switch        | Description   | 
| ------------- |:-------------|
| -Xms|	Sets the initial heap size for when the JVM starts.|
|-Xmx|	Sets the maximum heap size.|
|-Xmn|	Sets the size of the Young Generation.|
|-XX:PermSize|	Sets the starting size of the Permanent Generation.|
|-XX:MaxPermSize|	Sets the maximum size of the Permanent Generation|


### Related Links

- https://codeahoy.com/2017/08/06/basics-of-java-garbage-collection/
- https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html
- https://dzone.com/articles/understanding-garbage-collection-log
- https://stackify.com/what-is-java-garbage-collection/