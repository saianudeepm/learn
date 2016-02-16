
# Garbage Collection
* Aim: Identify memory that is no longer in use.

* Description: The basic problem of garbage collection is to identify the memory which is no-longer needed by the application, and to make it available for other allocations.Memory is determined to be no longer needed by the application, if there is no longer any way for the program to refer to the region of memory in question

* Formalization of problem:
A heap can be thought of as a set of objects, and a distinguished object known as the “root”.Each object has an address, size, and set of references (which are addresses of other objects). Addresses can be thought of as non-negative integers in a contiguous address space (from 0 to some maximum limit N)

```
Class Heap {
	List<MemoryObject>
}

Class MemoryObject{
	int address; // 0 to some max limit N
	int size;
	List<MemoryObject> references;
}
```

In practice, GC heaps are normally implemented using a subset of a real process address space (with potentially non-contiguous “segments”), but we can conceptually map this onto a single contiguous logical address space. 

* Constraints:
A heap has the constraint that no two objects may overlap. That is, 
given any two objects in the heap o1=(a1,s1), and o2=(a2,s2), it is always the case that either a1+s1≤a2
(i.e. a1 occurs entirely before a2) or a2+s2≤a1 (a2 occurs entirely before a1). 

So Heap is a directed graph containing vertices (objects) and edges (references). When there is no path from root to a given object, then it needs to be garbage collected.

## Mark-sweep 
This is a basic GC algo which garbage collects when the avilable memory is full

```
//Mark those objects which still have references. and then sweep all memory objects and free those which have no references.
markSweepCollect(){
	mark(root);
	sweep();
}
//mark the objects which have a path from root.
mark(MemoryObject o){
	if(marked[o]==0)
		marked[o]=1; //mark the object as visited
	for(MemoryObject p in o.references){
		mark(p);
	}
}//mark

/*iterate over all possible memory objects in heap 0-N and if not marked, free the memory and unmark marked objects */
sweep(){
	int i=0;
	while(i<N){
		if(marked[i]==1){
			marked[i]=0;
		}else{
			free(Memory[i]);
		}
		i++;
	}
}

```

[Reference](https://courses.cs.washington.edu/courses/csep521/07wi/prj/rick.pdf)


## Java Garbage Collection Basics
1. Marking
2. Normal Deletion

#### JVM Generations
The information learned from the object allocation behavior can be used to enhance the performance of the JVM. Therefore, the heap is broken up into smaller parts or generations. 
The heap parts are: 
1. Young Generation
2. Old or Tenured Generation
3. Permanent Generation

The Young Generation is where all new objects are allocated and aged. When the young generation fills up, this causes a minor garbage collection. Minor collections can be optimized assuming a high object mortality rate. A young generation full of dead objects is collected very quickly. Some surviving objects are aged and eventually move to the old generation.

Stop the World Event - All minor garbage collections are "Stop the World" events. This means that all application threads are stopped until the operation completes. Minor garbage collections are always Stop the World events.

The Old Generation is used to store long surviving objects. Typically, a threshold is set for young generation object and when that age is met, the object gets moved to the old generation. Eventually the old generation needs to be collected. This event is called a major garbage collection.

Major garbage collection are also Stop the World events. Often a major collection is much slower because it involves all live objects. So for Responsive applications, major garbage collections should be minimized. Also note, that the length of the Stop the World event for a major garbage collection is affected by the kind of garbage collector that is used for the old generation space.

The Permanent generation contains metadata required by the JVM to describe the classes and methods used in the application. The permanent generation is populated by the JVM at runtime based on classes in use by the application. In addition, Java SE library classes and methods may be stored here.

Classes may get collected (unloaded) if the JVM finds they are no longer needed and space may be needed for other classes. The permanent generation is included in a full garbage collection.

[Reference](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html)

