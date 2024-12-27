# Retain Cycle in dealloc Method: An Objective-C Bug

This repository demonstrates a subtle but critical error in Objective-C:  incorrect use of retain/release (or strong/weak) within a custom `dealloc` method.  Accidental retention of an object during deallocation can create a retain cycle, leading to memory leaks and unexpected crashes.

The `bug.m` file showcases the problematic code.  The `bugSolution.m` file presents the corrected version.

**Understanding the Issue:**
When an object's `dealloc` method is called, the system expects the object's reference count to be reduced to zero to release the memory. However, if you accidentally retain another object within `dealloc`, you prevent the reference count from reaching zero, creating a retain cycle. This cycle is especially difficult to identify because the retain occurs during the very process of object destruction.

**How to avoid this:**
Never retain or increase the retain count of any object in the dealloc method. Instead, remove the object's reference from the self object, and the object's memory will be deallocated properly when the reference count becomes 0.