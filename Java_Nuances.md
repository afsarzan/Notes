### Java nuances
---
- List<integers> numbers -> and numbers.remove(element) , it removes that particular element; but when we change List to Collection<Integer> then it will remove from indexed position not that particular element -> **issue** wehn overrriding , we should  not chnage the type of the parameters 
- Arrays.asList is fixed and cannot have .add() or .remove() method and uses the same memory as original , extremely fast f(o(1)) , you can use set(index,value) or array[index] = value to update. better to use List.of() to have better add and set immutable versions
- names.map(String::toUpperCase).forEach( name-> ...) // bad idea , shared mutability is devils work, Code behaves not work. Make sure lambdas are pure and do not mutate a shared variable from within the functional pipeline: ise toList() 
- Lambda functions should be pure. Pure function does not have any side-effects, Two rules for Pure functions
  1) The function does not modify anything in a away  the change is visible outside
  2) The funciton does not depend on anything that may change anything from outside.
- Immutable can be shared or can safely be duplicated
- List.copyOf() returns an immutable collection 
