# Lab 5 - Static Analysis using Mypy

###  Submitted by - Kunj Rakesh Patel 202001421


### Code used

```python
    import numpy 
    import django # type: ignore

    from django import forms

    class FibHeap:

        #### Node Class ####
        class Node:
            def __init__(self, key, value):
                # key value degree mark / prev next child parent
                self.key = key
                self.value = value
                self.degree = 0
                self.mark = False
                self.parent = self.child = None
                self.previous = self.next = self

            def issingle(self):
                return self == self.next

            def insert(self, node):
                if node == None:
                    return

                self.next.previous = node.previous
                node.previous.next = self.next
                self.next = node
                node.previous = self


            def remove(self):
                self.previous.next = self.next
                self.next.previous = self.previous
                self.next = self.previous = self

            def addchild(self, node):
                if self.child == None:
                    self.child = node
                else:
                    self.child.insert(node)
                node.parent = self
                node.mark = False
                self.degree += 1

            def removechild(self, node):
                if node.parent != self:
                    raise AssertionError("Cannot remove child from a node that is not its parent")

                if node.issingle():
                    if self.child != node:
                        raise AssertionError("Cannot remove a node that is not a child")
                    self.child = None
                else:
                    if self.child == node:
                        self.child = node.next
                    node.remove()

                node.parent = None
                node.mark = False
                self.degree -= 1
        #### End of Node Class ####

        def __init__ (self):
            self.minnode = None
            self.count = 0
            self.maxdegree = 0

        def isempty(self):
            return self.count == 0

        def insert(self, node):
            self.count += 1
            self._insertnode(node)
            # return node

        def _insertnode(self, node):
            if self.minnode == None:
                self.minnode = node
            else:
                self.minnode.insert(node)
                if node.key < self.minnode.key:
                    self.minnode = node
            # return node

        def minimum(self):
            if self.minnode == None:
                raise AssertionError("Cannot return minimum of empty heap")
            return self.minnode

        def merge(self, heap):
            self.minnode.insert(heap.minnode)
            if self.minnode == None or (heap.minnode != None and heap.minnode.key < self.minnode.key):
                self.minnode = heap.minnode
            self.count += heap.count

        def removeminimum(self):
            if self.minnode == None:
                raise AssertionError("Cannot remove from an empty heap")

            removed_node = self.minnode
            self.count -= 1

            # 1: Assign all old root children as new roots
            if self.minnode.child != None:
                c = self.minnode.child

                while True:
                    c.parent = None
                    c = c.next
                    if c == self.minnode.child:
                        break

                self.minnode.child = None
                self.minnode.insert(c)

            # 2.1: If we have removed the last key
            if self.minnode.next == self.minnode:
                if self.count != 0:
                    raise AssertionError("Heap error: Expected 0 keys, count is " + str(self.count))
                self.minnode = None
                return removed_node

            # 2.2: Merge any roots with the same degree
            logsize = 100
            degreeroots = [None] * logsize
            self.maxdegree = 0
            currentpointer = self.minnode.next

            while True:
                currentdegree = currentpointer.degree
                current = currentpointer
                currentpointer = currentpointer.next
                while degreeroots[currentdegree] != None:
                    other = degreeroots[currentdegree]
                    # Swap if required
                    if current.key > other.key:
                        temp = other
                        other = current
                        current = temp

                    other.remove()
                    current.addchild(other)
                    degreeroots[currentdegree] = None
                    currentdegree += 1

                degreeroots[currentdegree] = current
                if currentpointer == self.minnode:
                    break

            # 3: Remove current root and find new minnode
            self.minnode = None
            newmaxdegree = 0
            for d in range (0,logsize):
                if degreeroots[d] != None:
                    degreeroots[d].next = degreeroots[d].previous = degreeroots[d]
                    self._insertnode(degreeroots[d])
                    if (d > newmaxdegree):
                        newmaxdegree = d

            maxdegree = newmaxdegree

            return removed_node


        def decreasekey(self, node, newkey):
            if newkey > node.key:
                #import code
                #code.interact(local=locals())
                raise AssertionError("Cannot decrease a key to a greater value")
            elif newkey == node.key:
                return

            node.key = newkey

            parent = node.parent

            if parent == None:
                if newkey < self.minnode.key:
                    self.minnode = node
                return
            elif parent.key <= newkey:
                return

            while True:
                parent.removechild(node)
                self._insertnode(node)

                if parent.parent == None:
                    break
                elif parent.mark == False:
                    parent.mark
                    break
                else:
                    node = parent
                    parent = parent.parent
                    continue


    myHeap = FibHeap()

    i = 0
    i435  = 0

    myHeap.insert(i)
    myHeap.insert(0)
    myHeap.insert(765)
    myHeap.insert(i435)
    myHeap.insert(4362)
    myHeap.insert(4235)
    myHeap.insert(134)
    myHeap.insert(12)
    myHeap.insert('a')
    myHeap.insert(6)

    print(myHeap.minimum())
    
```
## Errors shown by mypy

![image](https://user-images.githubusercontent.com/75675988/227493916-ec375b0d-d810-4a13-a3bc-f9ea097b0bbe.png)

This error was shown because the text editor by default used 4 spaces for indentation and a tab was inserted instead of 4 spaces.


![image](https://user-images.githubusercontent.com/75675988/227494470-194ea450-5088-426a-934b-a2d459678148.png)    &emsp;&emsp;&emsp;&emsp;&emsp;         ![image](https://user-images.githubusercontent.com/75675988/227494623-e1d5d10c-f524-4a75-ad79-2bfb986c13e7.png)

An extra tab can be seen in the above code snippet which after changing to spaces removes syntax error prompted at that line.

![image](https://user-images.githubusercontent.com/75675988/227495004-99709fa4-ede2-4f5d-8b28-4ba2c5a43e20.png)

After removal of that error mypy checks further and finds these errors. The top  error is due to missing modules which can be removed by importing the required modules using pip.

Rest of the ![image](https://user-images.githubusercontent.com/75675988/227495187-e4e4a7e8-53bc-47ba-8eb3-8f62a215e3f5.png) are caused due to missing variables and can be removed either by declaring required variables or can be removed by removing commands/ expressions that use these variables. However the second option may not work as these expressions may be integral to working of the code. Hence, the correct approach will be to check if these expressions are required or not, then removing the expressions that are not required and declaring variables for the remaining expressions.

![image](https://user-images.githubusercontent.com/75675988/227495366-757d30dd-a95f-40d1-8302-2a2cc3eae95a.png)

After creating myHeap, i and i435 variables errors caused due to absence of these variables are resolved.

![image](https://user-images.githubusercontent.com/75675988/227495435-932ef2a4-acc6-4fad-8cb2-d1b719be6858.png)

Even after importing the required module we get an import error because even though mypy was able to find the module it was not able to find corresponding type hints.
As here we know that module is installed we can suppress the error by using 

![image](https://user-images.githubusercontent.com/75675988/227495535-848d53e2-343c-49de-b64a-de86040e4df3.png)

And, thus we can identify and remove all errors from our file without executing it using mypy.

![image](https://user-images.githubusercontent.com/75675988/227495627-52c500f2-66d5-4714-b66f-c5ee0bb113fd.png)




