# Array Manipulation in JavaScript: From Basics to Advanced

### How do you create an empty array in JavaScript?
```javascript
const arr = [1, 2, 3, 4, "Hello", {name: "Vishal"}, [1,2,3], 4];
// const arr2 = new Array();
console.log(arr);
```

### How do you access the first and last elements of an array?
```javascript
const firstElement = arr[0]; // O(1)
const arrLength = arr.length;
const lastElement = arr[arrLength - 1];
console.log(firstElement, arrLength, lastElement);
```

### How do you remove the last element from an array?
```javascript
const lastElement1 = arr.pop(); // O(1)
console.log(arr, lastElement1);
```

### How do you add an element to the end of an array?
```javascript
arr.push(5); // O(1)
console.log(arr);
```

### How do you add an element to the start of an array?
```javascript
arr.unshift(0); // O(N)
console.log(arr);
```

### How do you remove the first element from an array?
```javascript
arr.shift(); // O(N)
console.log(arr);
```

### How do you loop through an array in JavaScript?
```javascript
for (let i = 0; i < arr.length; i++){
    console.log(arr[i]);
}

arr.forEach((x, i) => {
    console.log(x);
});

for (let x of arr){
    console.log(x);
}
```

### Question 1: How do you check if an element exists in an array?
```javascript
const findElement = (arr, target) => {
    for (let x of arr){
        if (x === target){
            return true;
        }
    }
    return false;
}

console.log(findElement(arr, "Hello"));
console.log(findElement(arr, "H"));
console.log(arr.includes("Hello"));
```

### Question 2: How do you find the index of an element in an array?
```javascript
const findElementIndex = (arr, target) => {
    for (let i = 0; i < arr.length; i++){
        if (arr[i] === target){
            return i;
        }
    }
    return -1;
}

console.log(findElementIndex(arr, "Hello"));
console.log(arr.indexOf("Hello"));
```

### How to delete, add & update elements from a specific index?
```javascript
console.log(arr);
arr.splice(1, 3);
console.log(arr);
arr.splice(1, 0, 2, 3, 4, 5, 6);
console.log(arr);
arr.splice(1, 3, 6, 7, 8);
console.log(arr);
```

### `splice()` vs `slice()`
```javascript
const subArr = arr.slice(1, 4); // [start, end)
console.log(subArr);
```

### Shallow Copy of Array
```javascript
const arrB = arr;
arrB.splice(1, 4);
console.log(arrB, arr);
```

### Deep Copy of Array
```javascript
const arrC = [...arr];
const arrD = Array.from(arr);
const arrE = arr.concat();
arrC.splice(1, 4);
arrD.splice(1, 4);
arrE.splice(1, 3);
console.log(arrC, arrD, arrE, arr);
```

### How to concatenate two arrays in JavaScript?
```javascript
const newArr = [...arr, ...arrE];
const newArr2 = arr.concat(arrE);
console.log(newArr, newArr2);
```

### Question 3: How can you check if two arrays are equal?
```javascript
const isArrayEqual = (arr1, arr2) => {
    if (arr1.length !== arr2.length){
        return false;
    }

    for (let i = 0; i < arr1.length; i++){
        if (arr1[i] !== arr2[i]){
            return false;
        }
    }
    return true;

    // One Line solution
    // return arr1.length === arr2.length && arr1.every((ele, i) => arr1[i] === arr2[i]);
}

console.log(isArrayEqual([1, 2, 3], [1, 2, 3]));
```

### Question 4: How to sort an array in ascending and descending order?
```javascript
const x = [1, 4, 6, 0, -9, -5];
x.sort(); // O(NlogN)
console.log(x);

x.sort((a, b) => b - a);
console.log(x);
```

### Question 5: How to reverse an array?
```javascript
x.reverse();
console.log(x);
```

### Map, Filter & Reduce
```javascript
const newMapArr = x.map((ele, i) => ele * ele);
console.log(newMapArr);

const positiveNumbers = x.filter((ele, i) => ele > 0);
console.log(positiveNumbers);

const sumOFArr = positiveNumbers.reduce((acc, ele) => acc + ele);
console.log(sumOFArr);
```

### Flat: [1, 2, 4, 5, 6, 7, 8, 9]
```javascript
const y = [1, 2, [4, 5, [6, 7]], 8, 9];
const flattedArray = y.flat(2);
console.log(flattedArray);
```

### `filter()` vs `find()`
```javascript
const positiveNumber = x.find((ele, i) => ele > 0);
console.log(positiveNumber);
```

# Linked List in JavaScript

## Source Code
```javascript
class Node {
    constructor(data) {
        this.data = data;
        this.next = null;
    }
}

class LinkedList {
    constructor() {
        this.head = null;
        this.size = 0;
    }

    insertAtHead(data) {
        const newNode = new Node(data);
        newNode.next = this.head;
        this.head = newNode;
        this.size++;
    }

    insertAt(index, data) {
        if (index < 0 || index > this.size) {
            return "Invalid Index"
        }

        if (index === 0) {
            this.insertAtHead(data)
            return;
        }

        let newNode = new Node(data)
        let temp = this.head;
        for (let i = 0; i < index - 1; i++) {
            temp = temp.next;
        }

        newNode.next = temp.next;
        temp.next = newNode;

        this.size++;
    }

    print() {
        let result = ""
        let temp = this.head;
        while (temp) {
            result += `${temp.data}->`
            temp = temp.next;
        }
        return result
    }

    removeAtHead() {
        if (this.isEmpty()) {
            return "List is already empty"
        }

        this.head = this.head.next;
        this.size--;
    }

    removeElement(data) {
        if (this.isEmpty()) {
            return "List is already empty"
        }

        let current = this.head, prev = null;
        while (current) {
            if (current.data === data) {
                if (prev === null) {
                    this.head = current.next;
                } else {
                    prev.next = current.next;
                }
                this.size--;
                return current.element
            }
            prev = current;
            current = prev.next;
        }
        return -1;
    }

    searchElement(data) {
        let curr = this.head;
        let index = 0;

        while (curr) {
            if (curr.data === data) {
                return index;
            }
            index++;
            curr = curr.next;
        }
        return -1;
    }

    middleNode() {
        let slow = this.head, fast = this.head;
        while (fast && fast.next) {
            fast = fast.next.next;
            slow = slow.next;
        }
        return slow;
    };

    reverse() {
        let prev = null, curr = this.head, next;
        while (curr) {
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        this.head = prev;
    }

    isCycle() {
        let slow = this.head, fast = this.head;
        while (fast && fast.next) {
            fast = fast.next.next;
            slow = slow.next;

            if (slow === fast) {
                return true;
            }
        }
        return false;
    }

    isEmpty() {
        return this.size === 0;
    }
}

let list = new LinkedList()
list.insertAtHead(43) // 43
list.insertAtHead(50) // 50->43
list.insertAtHead(34) // 34->50->43
list.insertAt(2, 46) // 34->50->46->43
list.removeAtHead() // 50->46->43
list.removeElement(46) // 50->43
list.reverse() // 43->50
console.log(list.isCycle()) // false
console.log(list.middleNode()) // 50
console.log(list.searchElement(50)) //1
console.log(list.print()) // 43->50
```

# Objects in JavaScript

### Creating an object
```javascript
const person = {
    name: "Vishal",
    age: 21,
    isEducator: true,
    skills: ["C++", "JavaScript", "ReactJS"],
    projects: {
        "Frontend Freaks": "Frontend Development Project",
    },
    code: function(){
        return "start coding";
    },
    walk: () => {
        return "start walking";
    }
}
```

### Accessing properties using Dot Operator
```javascript
console.log(person.age); // 21
```

### Accessing properties using []
```javascript
console.log(person["name"]); // Vishal
```

### Checking if a key exists in the object
```javascript
console.log(person.hasOwnProperty("name")) // true
console.log(person.hasOwnProperty("last Name")) // false
```

### Adding, deleting, and updating keys
```javascript
person.name = "Vivek" // Updating name key 
person.location = "New Delhi" // Adding location Key
delete person.projects // Deleting projects key
console.log(person);
```

### Shallow Copy
```javascript
const person2 = person
person2.isEducator = false;
```

### Deep Copy
```javascript
const person3 = Object.assign({}, person)
// Nested Objects still do shallow copy here, there for we use lodash cloneDeep method(out of scope for this course)
person3.skills = null;
```

### Using freeze and seal methods
```javascript
Object.freeze(person) // User can't add or delete or update keys
console.log(person);
console.log(Object.isFrozen(person)) // true
```

```javascript
Object.seal(person) // User can't add or delete keys but can update the value
console.log(Object.isSealed(person)); // true
```

### Keys, Values & Entries
```javascript
console.log(Object.keys(person)) // ["name" , "age", "isEducator", ...]
console.log(Object.values(person)) // ["Vishal", 21, true, ...]
console.log(Object.entries(person)) // [["name", "Vishal"], ["age", 21], ["isEducator", true], ...]
```

### Looping through an Object using for...in
```javascript
for (let key in person) {
    console.log(key + ":", person[key]); // name: Vishal   age: 21, isEducator: true ...
}
```

### Looping through an Object using forEach with Object.keys
```javascript
Object.keys(person).forEach((key) => console.log(key))
```
### How to check if two objects are equal?
```javascript
console.log(Object.is(person, person3))
```

### find count of all players
```javascript
const data = {
    id: 1,
    name: ["P1", "P4"],
    next: {
        id: 2,
        name: ["P3"],
        next: {
            id: 3,
            name: ["P3", "P4", "P5"],
            next: {
                id: 4,
                name: ["P1", "P2", "P4"],
                next: {
                    id: 5,
                    name: ["P2", "P3", "P5"],
                    next: null
                }
            }
        }
    }
};

const playerCount = (data) => {
    if(data === null){
        return {}
    }

    let countPlayer = {}
    for(let player of data.name){
        countPlayer[player] = (countPlayer[player] || 0) + 1;
    }
    const nextPlayerCount = playerCount(data.next);

    for(let key in nextPlayerCount){
        countPlayer[key] = (countPlayer[key] || 0) + nextPlayerCount[key]
    }
    return countPlayer;
}

const countPlayer = playerCount(data);
console.log(countPlayer) // {p1: 2, p4: 3, p3: 3, p2: 2: p5: 2}
```

### Prototype and Inheritance in JavaScript Objects

```javascript
const obj1 = {
    name: "Vishal"
}

const obj2 = {
    age: 21,
    __proto__: obj1
}

console.log(obj2.name);
```

### Question 2: Group Anagrams (LeetCode 49)

```javascript
let anagrams = {};
    for (let i = 0; i < strs.length; i++) {
        const str = strs[i].split("").sort().join("")
        if (!anagrams.hasOwnProperty(str)) {
            anagrams[str] = []
        }

        anagrams[str] = [...anagrams[str], strs[i]];
    }
    return Object.values(anagrams);
```
# Queue in JavaScript

## Queue Implementation Using Array

```javascript
class Queue{
    constructor(){
        this.queue = []
    }

    enqueue(data){
        this.queue.push(data)
    }

    dequeue(){
        return this.isEmpty() ? null : this.queue.shift()
    }

    front(){
        return this.isEmpty() ? null : this.queue.at(0)
    }

    back(){
        return this.isEmpty() ? null : this.queue.at(-1)
    }

    isEmpty(){
        return this.queue.length === 0;
    }

    size(){
        return this.queue.length
    }
}

const queue = new Queue()
queue.enqueue(1)
queue.enqueue(2)
queue.enqueue(3)
console.log(queue.dequeue()) // 1
console.log(queue.front()) // 2
console.log(queue.back()) // 3
console.log(queue.isEmpty()) // false
console.log(queue.size()) // 2
console.log(queue) // Queue { queue: [2, 3]}
```


## Queue Implementation Using Linked List

```javascript
class Node{
    constructor(data){
        this.data = data;
        this.next = null;
    }
}

class QueueLinkedList{
    constructor(){
        this.head = null;
        this.tail = null;
        this.size = 0;
    }

    enqueue(data){
        const newNode = new Node(data);

        if(this.head === null){
            this.head = newNode;
        } else{
            this.tail.next = newNode;
        }
        
        this.tail = newNode;
        this.size++;
    }

    dequeue(){
        if(this.isEmpty()){
            return null;
        }

        const deletedItem = this.head.data;
        this.head = this.head.next;
        this.size--;
        return deletedItem;
    }

    front(){
        return this.isEmpty() ? null : this.head.data;
    }

    back(){
        return this.isEmpty() ? null : this.tail.data;
    }

    isEmpty(){
        return this.size === 0;
    }
}

const queue1 = new QueueLinkedList()
queue1.enqueue(5)
queue1.enqueue(6)
queue1.enqueue(7)
console.log(queue1.dequeue()) // 5
console.log(queue1.front()) // 6
console.log(queue1.back()) // 7
console.log(queue1.size) // 2
console.log(queue1) 
/* QueueLinkedList 
{ 
    head: Node { data: 6, next: Node { data: 7, next: null }}, 
    tail: Node{data: 7, next: null}, 
    size: 2
}
*/
```

## Implement Queue Using Stacks

```javascript
class QueueStack{
    constructor(){
        this.stack1 = []
        this.stack2 = []
    }

    push(x){
        while(this.stack1.length > 0){
            this.stack2.push(this.stack1.pop())
        }

        this.stack1.push(x);

        while(this.stack2.length > 0){
            this.stack1.push(this.stack2.pop())
        }
    };

    pop(){
        if(this.empty()){
            return null;
        }

        return this.stack1.pop()
    };

    peek(){
        return this.empty() ? null : this.stack1.at(-1)
    };

    empty(){
        return this.stack1.length === 0
    };
}
```

## Implement Circular Queue Using Linked List

```javascript
class Node {
    constructor(data) {
        this.data = data;
        this.next = null;
    }
}

class MyCircularQueue {
    constructor(k) {
        this.capacity = k;
        this.head = null;
        this.tail = null;
        this.size = 0;
    }

    enQueue(data) {
        if(this.isFull()){
            return false;
        }

        const newNode = new Node(data);

        if(this.head === null){
            this.head = newNode;
        } else{
            this.tail.next = newNode;
        }
        
        this.tail = newNode;
        this.tail.next = this.head;
        this.size++;
        return true;
    }

    deQueue() {
        if(this.isEmpty()){
            return false;
        }

        if(this.head === this.tail){
            this.head = null;
            this.tail = null;
        } else{
            this.head = this.head.next;
            this.tail.next = this.head;
        }

        this.size--;
        return true;
    }

    Front() {
        return this.isEmpty() ? -1 : this.head.data;
    }

    Rear() {
        return this.isEmpty() ? -1 : this.tail.data;
    }

    isEmpty() {
        return this.size === 0;
    }

    isFull() {
        return this.size === this.capacity;
    }
}
```

# Recursion in JavaScript

### Factorial of a Number

```javascript
function factorial(n){
    if(n === 0)
        return 1;
    return n * factorial(n - 1);
}

console.log(factorial(8));
```

### Sum of Array

```javascript
function sumOfArrays(arr, n){
    if(n === 0){
        return 0;
    }

    return arr[n - 1] + sumOfArrays(arr, n - 1);
}

console.log(sumOfArrays([1, 2, 3, 4, 5], 5));
```

### Fibonacci Number

```javascript
function fibo(n){
    if(n < 2){
        return n;
    }
    return fibo(n - 1) + fibo(n - 2);
}

console.log(fibo(5));
```
# Searching in JavaScript

### Linear Search in JavaScript

```javascript
const arr = [1, 2, 6, 9, 0, -5];

const linearSearch = (arr, target) => {
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] === target) {
            return i;
        }
    }
    return -1;
}

console.log(linearSearch(arr, 8));
console.log(arr.includes(9));
console.log(arr.indexOf(9));
console.log(arr.find((num) => num > 0));
console.log(arr.findIndex((num) => num < 0));
```

### Binary Search In JavaScript

```javascript
const BinarySearch = (arr, target) => {
    let start = 0, end = arr.length - 1;
    while (start <= end) {
        let mid = Math.floor((start + end) / 2);

        if (arr[mid] === target) {
            return mid;
        }

        else if (arr[mid] > target) {
            end = mid - 1;
        }

        else {
            start = mid + 1;
        }
    }

    return -1;
}

console.log(BinarySearch([1, 4, 6, 9, 12, 15], 8));
```

### Binary Search using Recursion

```javascript
const BinarySearchRecur = (arr, target) => {
    return BinarySearchUtil(arr, target, 0, arr.length);
}

const BinarySearchUtil = (arr, target, start, end) => {
    if (start > end)
        return -1;

    let mid = Math.floor((start + end) / 2);

    if (arr[mid] === target) {
        return mid;
    }

    else if (arr[mid] > target) {
        return BinarySearchUtil(arr, target, start, mid - 1);
    }

    else {
        return BinarySearchUtil(arr, target, mid + 1, end);
    }
}
```

### Find floor and ceil value of X in an array 

```javascript
const floorCeil = (arr, target) => {
    let start = 0, end = arr.length;
    let floor = -1, ceil = -1;
    while(start <= end){
        let mid = Math.floor((start + end)/2);

        if(arr[mid] === target){
            floor = mid;
            ceil = mid;
            return [ceil, mid]
        }

        else if(arr[mid] > target){
            ceil = mid;
            end = mid - 1;
        }

        else {
            floor = mid;
            start = mid + 1;
        }
    }

    return [ceil, floor]
}
```

# Map, WeakMap, Set, WeakSet in JavaScript

## Set in JavaScript:

```javascript
// Creating a Set
const mySet = new Set();

// Adding values to the Set
mySet.add(1);
mySet.add("hello");
mySet.add(true);

// Checking if a value exists
console.log(mySet.has(1)); // true

// Removing a value
mySet.delete("hello");

// Iterating through the Set
for (const value of mySet) {
    console.log(value);
}

// Size of the Set
console.log(mySet.size); // 2

// Clearing the Set
mySet.clear();
```

## Map in JavaScript

```javascript
// Creating a Map
const myMap = new Map();

// Adding key-value pairs to the Map
myMap.set("name", "Vishal");
myMap.set("age", 21);

// Getting a value using a key
console.log(myMap.get("name")); // Vishal

// Checking if a key exists
console.log(myMap.has("age")); // true

// Removing a key-value pair
myMap.delete("age");

// Iterating through the Map
for (const [key, value] of myMap) {
    console.log(key, value);
}

// Size of the Map
console.log(myMap.size); // 1

// Clearing the Map
myMap.clear();
```

## Weak Map in JavaScript

```javascript
let obj = { key: 'value' };

// Creating a WeakMap
let weakMap = new WeakMap();
weakMap.set(obj, 'metadata');

// Checking if the object still exists in the WeakMap
console.log(weakMap.has(obj)); // true

// Removing the strong reference to the object
obj = null;

// At this point, the object is no longer strongly referenced
// The WeakMap's weak reference will allow the object to be garbage collected
console.log(weakMap.has(obj)); // false
```

# Sorting In JavaScript

### Sort an Array
```javascript
const arr = [-2, -7, 1000, 5]
console.log(arr.sort()) // -2, -7, 1000, 5
console.log(arr.sort((a, b) => a - b)) // -7, -2 , 5, 1000
console.log(arr.sort((a, b) => b - a)) // 1000, 5, -2, -7

const strArr = ["mango", "apple", "banana"]
console.log(strArr.sort()) // "apple", "banana", "mango"
```

### Sort a String
```javascript
const str = "Vishal"
console.log(str.split("").sort().join("")) // "Vahils
```

### Bubble Sort In JavaScript
```javascript
const bubbleSort = (arr) => {
    let swapped;
    do {
        swapped = false;
        for (let i = 0; i < arr.length - 1; i++) {
            if (arr[i] > arr[i + 1]) {
                [arr[i], arr[i + 1]] = [arr[i + 1], arr[i]]
                swapped = true;
            }
        }
    } while (swapped)
    return arr;
}

console.log(bubbleSort(arr)) // -7, -2 , 5, 1000
```

### Selection Sort in JavaScript
```javascript
const selectionSort = (arr) => {
    for (let i = 0; i < arr.length - 1; i++) {
        let minIndex = i;
        for (let j = i + 1; j < arr.length; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        [arr[minIndex], arr[i]] = [arr[i], arr[minIndex]]
    }
    return arr;
}

console.log(selectionSort(arr)) // -7, -2 , 5, 1000
```

### Insertion Sort In JavaScript
```javascript
const insertionSort = (arr) => {
    for(let i=1; i<arr.length; i++){
        let current = arr[i];
        let j = i-1;
        while(j >= 0 && arr[j] > current){
            arr[j+1] = arr[j];
            j--;
        }
        arr[j+1] = current;
    }
    return arr;
}

console.log(insertionSort(arr)) // -7, -2 , 5, 1000
```

### Merge Sort in JavaScript 
```javascript
const mergeSort = (arr) => {
    if (arr.length < 2) {
        return arr;
    }
    let mid = Math.floor(arr.length / 2);
    let left = mergeSort(arr.slice(0, mid))
    let right = mergeSort(arr.slice(mid))
    return merge(left, right)
}

const merge = (left, right) => {
    const result = []
    let leftIndex = 0, rightIndex = 0;
    while (leftIndex < left.length && rightIndex < right.length) {
        if (left[leftIndex] < right[rightIndex]) {
            result.push(left[leftIndex])
            leftIndex++;
        }
        else {
            result.push(right[rightIndex])
            rightIndex++;
        }
    }

    while (leftIndex < left.length) {
        result.push(left[leftIndex])
        leftIndex++;
    }

    while (rightIndex < right.length) {
        result.push(right[rightIndex])
        rightIndex++;
    }

    return result;
}

const arr1 = [29, 10, 8, 16, 37, 14, 4, 45]
console.log(mergeSort(arr1))
```
### Merge Sort in JavaScript (Space Optimised)

```javascript
const mergeSortInplace = (arr, low, high) => {
    if (low < high) {
        let mid = Math.floor((low + high) / 2);
        mergeSortInplace(arr, low, mid)
        mergeSortInplace(arr, mid + 1, high)
        mergeInplace(arr, low, mid, high)
    }
}

const mergeInplace = (arr, low, mid, high) => {
    const result = []
    let leftIndex = low, rightIndex = mid + 1;
    while (leftIndex <= mid && rightIndex <= high) {
        if (arr[leftIndex] < arr[rightIndex]) {
            result.push(arr[leftIndex])
            leftIndex++;
        }
        else {
            result.push(arr[rightIndex])
            rightIndex++;
        }
    }

    while (leftIndex <= mid) {
        result.push(arr[leftIndex])
        leftIndex++;
    }

    while (rightIndex <= high) {
        result.push(arr[rightIndex])
        rightIndex++;
    }

    for (let i = low; i <= high; i++) {
        arr[i] = result[i - low];
    }
}

const arr1 = [29, 10, 8, 16, 37, 14, 4, 45]
console.log(mergeSortInplace(arr1, 0, arr.length - 1))
console.log(arr1)
```

### Quick Sort in JavaScript

```javascript
const quickSort = (arr) => {
    if(arr.length < 2){
        return arr;
    }
    let pivotIndex = Math.floor(Math.random() * arr.length);
    let left = [], right = [];
    for(let i=0; i<arr.length; i++){
        if(i === pivotIndex)
            continue;

        if(arr[i] < arr[pivotIndex]){
            left.push(arr[i])
        }
        else{
            right.push(arr[i])
        }
    }

    return [...quickSort(left), arr[pivotIndex], ...quickSort(right)]
}

console.log(quickSort(arr1))
```
# Stack In JavaScript

## Stack Implementation Using Array
```javascript
class Stack{
    constructor(){
        this.stack = []
    }

    push(item){
        this.stack.push(item)
    }

    pop(){
        if(this.isEmpty()){
            return null;
        }
        return this.stack.pop()
    }

    peek(){
        if(this.isEmpty()){
            return null;
        }
        return this.stack[this.stack.length - 1]
    }

    isEmpty(){
        return this.stack.length === 0
    }

    size(){
        return this.stack.length;
    }
}

const stack = new Stack()
stack.push(10)
stack.push(12)
stack.push(13)
stack.push(15)
stack.push(17)
stack.pop()
console.log(stack.peek())
console.log(stack)
```

## Stack Implementation Using Linked List

```javascript
class Node {
    constructor(data) {
        this.data = data;
        this.next = null;
    }
}

class StackLinkedList {
    constructor() {
        this.top = null;
        this.size = 0;
    }

    push(data) {
        const newNode = new Node(data);
        newNode.next = this.top;
        this.top = newNode;
        this.size++;
    }

    pop() {
        if (this.isEmpty()) {
            return "List is already empty"
        }
        const item = this.top.data;
        this.top = this.top.next;
        this.size--;
        return item;
    }

    peek(){
        return this.top.data;
    }

    isEmpty() {
        return this.size === 0;
    }
}

const stack1 = new StackLinkedList()
stack1.push(10)
stack1.push(12)
stack1.push(14)
console.log(stack1.pop())
console.log(stack1.peek())
console.log(stack1)
```
# String In JavaScript

### Length of a String
```javascript
let firstName = "Vaishali";
console.log(firstName.length);
```

### Access String Element
```javascript
console.log(firstName.charAt(2)); // i
console.log(firstName[2]); // i
console.log(firstName.charCodeAt(2)); // 115 (Ascii Code)
```

### Check Presence of Character
```javascript
console.log(firstName.includes("r")); // false (& if present it return true)
console.log(firstName.indexOf("i")); // 2 (& if not present it return -1)
console.log(firstName.lastIndexOf("i")); // 7 
```

### Compare Two Strings
```javascript
let anotherName = "Vishal";
console.log(firstName.localeCompare(anotherName)); // -1 (& if strings are equal it return 0)
```

### Replace Substring
```javascript
const str = "Vishal is Best Frontend Developer. Vishal is Best Developer. ";
console.log(str.replace("Vishal", "Sujit")); // "Sujit is Best Frontend Developer. Vishal is Best Developer. "
console.log(str.replaceAll("Vishal", "Sujit")); // "Sujit is Best Frontend Developer. Sujit is Best Developer. "
```

### Substring of a String
```javascript
console.log(str.substring(6, 30)); 
console.log(str.slice(-10, -1));
```

### Split and Join
```javascript
console.log(str.split(""));
const subString = str.split(" ");
console.log(subString.join(" "));
```

### String Start and End
```javascript
console.log(str.startsWith("Vishal")); // true
console.log(str.endsWith("Developer")); // true
```

### Trim and Case Conversion
```javascript
const trimStr = str.trim();
const trimStrStart = str.trimStart();
const trimStrEnd = str.trimEnd();
console.log(trimStr, trimStr.length);
console.log(str.toLowerCase());
console.log(str.toUpperCase());
```

### Convert Number and Object to String
```javascript
const num = 123;
console.log(num, num.toString());

const obj = {
    name: "Vishal",
    course: "DSA with Vishal"
};
console.log(obj, JSON.stringify(obj));
```

### Concatenate Strings
```javascript
const lastName = "Rajput";
console.log(firstName + lastName);
console.log(`${firstName} ${lastName} is a Best Developer`);
console.log(firstName.concat(lastName, " is a", " Best"));
```
