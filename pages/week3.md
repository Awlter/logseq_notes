---
title: week3
---

## questions answers
- Abstract data type is a higher level of abstraction from the concrete primitive data type from a specific language
- array queue V.S doubly linked list queue
  - pus and pop: for array queue, O(1) or O(n) depending on which end of the array as the head; for doubly linked list queue, O(1)
  - A doubly linked list queue may occupies much more space
##
```
class Stack
  def initialize
    @items = []
  end

  def is_empty?
    @items.empty?
  end

  def push(item)
    @items.push(item)
  end

  def pop
    @items.pop
  end

  def peek
    @items.last
  end

  def size
    @items.size
  end
end

def reverse_list(list)
  reversed = []
  stack = Stack.new
  list.each { |item| stack.push(item) }

  while !stack.is_empty?
    reversed << stack.pop
  end
  
  reversed
end

p reverse_list(['s', 'u', 'v'])
```
##
