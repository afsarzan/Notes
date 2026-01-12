### Java nuances
---
- List<integers> numbers -> and numbers.remove(element) , it removes that particular element; but when we change List to Collection<Integer> then it will remove from indexed position not that particular element -> **issue** wehn overrriding , we should  not chnage the type of the parameters 
- Arrays.asList is fixed and cannot have .add() or .remove() method and uses the same memory as original , extremely fast f(o(1)) , you can use set(index,value) or array[index] = value to update. better to use List.of() to have better add and set immutable versions
- 
- 
