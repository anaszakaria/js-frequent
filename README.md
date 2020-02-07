# js-frequent
List of frequently used Javascript functions

- [Array Filter](https://github.com/anaszakaria/js-frequent#array-filter)
  - [Filter array content based on search criteria](https://github.com/anaszakaria/js-frequent#filter-array-content-based-on-search-criteria)
  - [Find unique values in array](https://github.com/anaszakaria/js-frequent#find-unique-values-in-array)
  - [Remove false value - undefined, null and false](https://github.com/anaszakaria/js-frequent#remove-false-value---undefined-null-and-false)
  - [Find differences - returns the values from array that are not present in the other arrays](https://github.com/anaszakaria/js-frequent#find-differences---returns-the-values-from-array-that-are-not-present-in-the-other-arrays)
  - [Sorts an array of object based on an object key provided by a parameter](https://github.com/anaszakaria/js-frequent#sorts-an-array-of-object-based-on-an-object-key-provided-by-a-parameter)
  - [Non recursive flatten deep using a stack](https://github.com/anaszakaria/js-frequent#non-recursive-flatten-deep-using-a-stack)
  - [Find indices of elements in an array](https://github.com/anaszakaria/js-frequent#find-indices-of-elements-in-an-array)
  - [Find boolean value in array - 0, null, undefined will result in false](https://github.com/anaszakaria/js-frequent#find-boolean-value-in-array---0-null-undefined-will-result-in-false)
- [Array Reduce](https://github.com/anaszakaria/js-frequent#array-reduce)
  - [Find the maximum or minimum collection item](https://github.com/anaszakaria/js-frequent#find-the-maximum-or-minimum-collection-item)
  - [Count instance of values in object](https://github.com/anaszakaria/js-frequent#count-instance-of-values-in-object)
  - [Grouping objects by a property](https://github.com/anaszakaria/js-frequent#grouping-objects-by-a-property)
  - [Bonding arrays contained in an array of objects using the spread operator and initial value](https://github.com/anaszakaria/js-frequent#bonding-arrays-contained-in-an-array-of-objects-using-the-spread-operator-and-initial-value)
  - [Remove duplicate items in array](https://github.com/anaszakaria/js-frequent#remove-duplicate-items-in-array)
  - [Function composition enabling pipe functionality](https://github.com/anaszakaria/js-frequent#function-composition-enabling-pipe-functionality)
  - [Flattened array using recursive function](https://github.com/anaszakaria/js-frequent#flattened-array-using-recursive-function)
  - [Filter and Map alternative](https://github.com/anaszakaria/js-frequent#filter-and-map-alternative)
  - [Array to Object conversion](https://github.com/anaszakaria/js-frequent#array-to-object-conversion)
- [Array Sort](https://github.com/anaszakaria/js-frequent#array-sort)
  - [Sort array by value with options (ascending and descending)](https://github.com/anaszakaria/js-frequent#sort-array-by-value-with-options-ascending-and-descending)
- [Object](https://github.com/anaszakaria/js-frequent#object)
  - [Loop through object and get key value pairs](https://github.com/anaszakaria/js-frequent#loop-through-object-and-get-key-value-pairs)
  - [Recursive function - Retrieve nested obj key value](https://github.com/anaszakaria/js-frequent#recursive-function---retrieve-nested-obj-key-value)
  - [Convert object to array](https://github.com/anaszakaria/js-frequent#convert-object-to-array)
  - [Merge object into another object and overwrite the original value if exists](https://github.com/anaszakaria/js-frequent#merge-object-into-another-object-and-overwrite-the-original-value-if-exists)
  - [Find path of nested object](https://github.com/anaszakaria/js-frequent#find-path-of-nested-object)
- [Set](https://github.com/anaszakaria/js-frequent#set)
  - [Set operations - Subset, Union, Intersection, Symmetric Difference and Difference](https://github.com/anaszakaria/js-frequent#set-operations---subset-union-intersection-symmetric-difference-and-difference)
- [Array Destructuring](https://github.com/anaszakaria/js-frequent#array-destructuring)
  - [Tic Tac Toe algorithm comparison](https://github.com/anaszakaria/js-frequent#tic-tac-toe-algorithm-comparison)

## Array Filter

### Filter array content based on search criteria

```
const fruits = ['apple', 'banana', 'grapes', 'mango', 'orange']

function filterItems(array, query) {
  return array.filter(fruit => {
    return fruit.toLowerCase().indexOf(query.toLowerCase()) !== -1
  })
}

console.log(filterItems(fruits, 'ap')) // ['apple', 'grapes']
console.log(filterItems(fruits, 'an')) // ['banana', 'mango', 'orange']
```

### Find unique values in array

```
const words = ['dog', 'cat', 'cat', 'dog', 'chicken', 'dog', 'whale']

const getUniqueWords = array => {
  return array.filter((word, index, srcArray) => {
    return srcArray.indexOf(word) === index
  })
}

console.log(getUniqueWords(words)) // ["dog", "cat", "chicken", "whale"]
```

### Remove false value - undefined, null and false

```
const defArray = [undefined, null, null, 'Whale', 'Tiger', false, 434, '', 32.0]

const removeFalseValue = (array) => {
  return array.filter(Boolean)
}

console.log(removeFalseValue(defArray))
```

### Find differences - returns the values from array that are not present in the other arrays

```
const arrays = [[1, 2, 3, 4, 5], [5, 2, 10]]

const findDifference = (array) => {
  return array.reduce((a, b) => {
    return a.filter(value => {
      return !b.includes(value) // return b.includes(value) - find similar values [5, 2]
    })
  })
}

console.log(findDifference(arrays)) // output: [1, 3, 4]
```

### Sorts an array of object based on an object key provided by a parameter

```
const fruits = [
  { name: 'banana', amount: 2 },
  { name: 'apple', amount: 4 },
  { name: 'pineapple', amount: 2 },
  { name: 'mango', amount: 1 }
]

const sortBy = (key) => {
  return (a, b) => (a[key] > b[key]) ? 1 : ((b[key] > a[key]) ? -1 : 0)
}

console.log(fruits.concat().sort(sortBy('name')))
```

### Non recursive flatten deep using a stack

```
const nestedArray = [1,2,3,[1,2,3,4, [2,3,4]]]

const flatten = array => {
  const stack = [...array]
  const res = []
  while (stack.length) {
    // pop value from stack
    const next = stack.pop()
    if (Array.isArray(next)) {
      // push back array items, won't modify the original array
      stack.push(...next)
    } else {
      res.push(next)
    }
  }
  //reverse to restore input order
  return res.reverse()
}

console.log(flatten(nestedArray)) // [1, 2, 3, 1, 2, 3, 4, 2, 3, 4]
```

### Find indices of elements in an array

```
let indices = []
let array = ['a', 'b', 'a', 'c', 'a', 'd']
let element = 'a'
let itemIndex = array.lastIndexOf(element)

while (itemIndex !== -1) {
  indices.push(itemIndex)
  itemIndex = itemIndex > 0 ? array.lastIndexOf(element, itemIndex - 1) : -1
}

console.log(indices.reverse()) // [0, 2, 4]
```

### Find boolean value in array - 0, null, undefined will result in false

```
const items = [0, null, undefined, 1, -1, '22', 'str']
const booleanItems = items.map(Boolean)

console.log(booleanItems) // [false, false, false, true, true, true, true]
```

## Array Reduce

### Find the maximum or minimum collection item

```
const data = [
  { value: 6 },
  { value: 2 },
  { value: 4 }
]

const minItem = data.reduce((a, b) => { return a.value <= b.value ? a : b }, {})
const maxItem = data.reduce((a, b) => { return a.value >= b.value ? a : b }, {})
console.log(minItem, maxItem) // output: { value: 2 }, { value: 6 }
```

### Count instance of values in object

```
const names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice', 'Jack', 'Tiff', 'Jack', 'Alice']

const countedNames = names.reduce((countObj, name) => {
  if (name in countObj) {
    countObj[name]++
  } else {
    countObj[name] = 1
  }
  return countObj
}, {})

console.log(countedNames) // {Alice: 3, Bob: 1, Tiff: 2, Bruce: 1, Jack: 2}
```

### Grouping objects by a property

```
const people = [
  { name: 'Alice', age: 25, job: 'Programmer' },
  { name: 'John', age: 27, job: 'Programmer' },
  { name: 'Max', age: 27, job: 'Programmer' },
  { name: 'Jane', age: 25, job: 'Engineer' }
]

const groupBy = (objectArray, property) => {
  return objectArray.reduce((acc, obj) => {
    const key = obj[property]
    if (!acc[key]) {
      acc[key] = []
    }
    acc[key].push(obj)
    return acc
  }, {})
}

console.log(groupBy(people, 'job'))
```

### Bonding arrays contained in an array of objects using the spread operator and initial value

```
const person = [
  { name: 'Anna', books: ['Bible', 'Harry Potter'] },
  { name: 'Bob', books: ['War and peace', 'Romeo and Juliet'] },
  { name: 'Alice', books: ['The Lord of the Rings', 'The Shining'] }
]

const bookLists = person.reduce((array, obj) => {
  return [...array, ...obj.books]
}, ['New Book'])

console.log(bookLists) // ["New Book", "Bible", "Harry Potter", "War and peace", "Romeo and Juliet", "The Lord of the Rings", "The Shining"]
```

### Remove duplicate items in array

```
const words = ['a', 'b', 'a', 'b', 'c', 'e', 'e', 'c', 'd', 'd', 'd', 'd']

const removeDuplicate = words.reduce((accumulator, currentValue) => {
  if (accumulator.indexOf(currentValue) === -1) {
    accumulator.push(currentValue)
  }
  return accumulator
}, [])

console.log(removeDuplicate) // ["a", "b", "c", "e", "d"]
```

### Function composition enabling pipe functionality

```
const double = x => x + x
const triple = x => 3 * x
const quadruple = x => 4 * x

const pipeOnce = (fn1, fn2) => (args) => (fn2(fn1(args)));
const pipe = (...func) => func.reduce(pipeOnce);

// Composed functions for multiplication of specific values
const multiply6 = pipe(double, triple);
const multiply9 = pipe(triple, triple);
const multiply16 = pipe(quadruple, quadruple);
const multiply24 = pipe(double, triple, quadruple);

// Usage
console.log(multiply6(6))
console.log(multiply9(9))
console.log(multiply16(16))
console.log(multiply24(10))
```

### Flattened array using recursive function

```
const nestedArray = [1,2,3,[1,2,3,4, [2,3,4]]]

const flattenDeep = array => {
  return array.reduce((acc, val) => Array.isArray(val) ? acc.concat(flattenDeep(val)) : acc.concat(val), [])
}

console.log(flattenDeep(nestedArray)) // [1, 2, 3, 1, 2, 3, 4, 2, 3, 4]
```

### Filter and Map alternative

```
const studentsData = [
  { firstName: 'Safee', lastName: 'Sali', score: 53 },
  { firstName: 'Lionel', lastName: 'Messi', score: 100 },
  { firstName: 'Cristiano', lastName: 'Ronaldo', score: 90 }
]

const topStudents = studentsData.reduce((nameList, student) => {
  if (student.score >= 80) {
    nameList.push(`${student.firstName} ${student.lastName}`)
  }
  return nameList
}, [])

console.log(topStudents) // ['Lionel Messi', 'Cristiano Ronaldo']
```

### Array to Object conversion

```
const stats = [
  {
    name: 'Anas',
    id: 'ID007',
    details: {
      required: {
        message: 'ID is required',
        allowEmpty: true
      }
    },
  },
  {
    name: 'Muaz',
    id: 'ID002',
    details: {
      required: {
        message: 'ID is required',
        allowEmpty: false
      }
    },
  }
]

const keyInfo = stats.reduce((obj, info) => {
  return Object.assign(obj, { [info.id]: info.details })
}, {})

console.log(keyInfo)
```

## Array Sort

### Sort array by value with options (ascending and descending)

```
const info = [
  { name: 'Edward', value: 21 },
  { name: 'Sharpe', value: 37 },
  { name: 'And', value: 45 },
  { name: 'The', value: -12 },
  { name: 'Magnetic', value: 13 },
  { name: 'Zeros', value: 37 }
]

function sortObjectArray(array, key) {
  let argType = ''
  const item = Object.entries(array[0])
  for (const [itemKey, value] of item) {
    if (key === itemKey) {
      argType = value
    }
  }

  const newArray = [...array]

  switch(typeof argType) {
    case 'string':
    newArray.sort((a, b) => {
      var nameA = a.name.toUpperCase() // ignore upper and lowercase
      var nameB = b.name.toUpperCase() // ignore upper and lowercase
      if (nameA < nameB) return -1
      if (nameA > nameB) return 1
      return 0
    })
    break
    case 'number':
    newArray.sort((a, b) => {
      return a.value - b.value
    })
    break
    default:
    console.log('type is not defined')
  }
  return newArray
}

console.log('By value:', sortObjectArray(info, 'value'))
console.log('By name:', sortObjectArray(info, 'name'))

const sortBy = (key, option = 'asc') => {
  return (a, b) => {
    try {
      const objKeys = Object.keys(a)
      if (!objKeys.includes(key)) {
        throw BreakException
      }
    } catch(error) {
      console.log(error)
      if (error !== BreakException) throw error
    }

    try {
      if (typeof a[key] === 'string') {
        if (option === 'asc') return (a[key] > b[key]) ? 1 : ((b[key] > a[key]) ? -1 : 0)
        else return (a[key] < b[key]) ? 1 : ((b[key] < a[key]) ? -1 : 0)
      } else if (typeof a[key] === 'number') {
        if (option === 'asc') return a[key] - b[key]
        else return b[key] - a[key]
      } else {
        throw new Error('Type is not supported: Pass string or number only as argument')
      }
    } catch(error) {
      console.log(error)
    }
  }
}

const infoByValueAsc = [...info]
console.log('By value ascending:', infoByValueAsc.sort(sortBy('value')))

const infoByValueDesc = [...info]
console.log('By value descending:', infoByValueDesc.sort(sortBy('value', 'desc')))

const infoByNameAsc = [...info]
console.log('By name ascending:', infoByNameAsc.sort(sortBy('name')))

const infoByNameDesc = [...info]
console.log('By name descending:', infoByNameDesc.sort(sortBy('name', 'desc')))

console.log('Info:', info) // default array is not mutated
```

## Object

### Loop through object and get key value pairs

```
const calculation = {
  type: 'Numbers',
  section: {
    even: [0, 2, 4, 6, 8],
    odd: [1, 3, 5, 7, 9]
  }
}

const objArray = Object.entries(calculation)
console.log(objArray)

for (const [key, value] of objArray) {
  console.log(key, value)
}
```

### Recursive function - Retrieve nested obj key value

```
const person = {
    firstName: 'Anas',
    lastName: 'Zakaria',
    age: 39,
    address: {
        home: 'Bangi',
        office: 'Putrajaya'
    },
    job: 'Software Developer',
    skills: [
        { frontEnd: ['HTML', 'CSS', 'Javacript'] },
        { backEnd: ['NodeJS', '.Net Core'] },
        { others: ['Git', 'Webpack'] }
    ]
}

function iterateObj(obj, fn) {
    const array = Object.entries(obj)
    for (const [key, value] of array) {
        fn(key, value)
        if (value instanceof Object || value instanceof Array) {
            iterateObj(value, fn)
        }
    }
}

iterateObj(person, (key, value) => {
    if (typeof value !== 'object') {
        console.log(`${key}: ${value}`)
    } else {
        console.log(`${key} -`)
    }
})
```

### Convert object to array

```
const postAuthors = {
  person1: { id: 1, name: 'Antonin Januska', role: 'author' },
  person2: { id: 2, name: 'JK Rowling', role: 'real author' },
}

console.log(Object.values(postAuthors))
```

### Merge object into another object and overwrite the original value if exists

```
const sourceObject = {
  id: 1,
  author: 'Antonin Januska',
  bio: 'Not cool',
  posts: ['a', 'b']
}

Object.assign(sourceObject, { // modify sourceObject
  posts: [],
  topComments: ['Good'],
  bio: 'A very cool person',
})

console.log(sourceObject)

const finalObject = Object.assign({}, sourceObject, { // create new object
  posts: [],
  topComments: [],
  bio: 'A very cool person',
});

console.log(finalObject) // note: sourceObject is a separate object from finalObject in this scenario
```

### Find path of nested object

```
const projects = [
  {
    id: 'DEPT_IT',
    name: 'Information Technology',
    child: [
      { id: 'DB"', name: 'Database' },
      { id: 'MOB', name: 'Mobile Application' },
      {
        id: 'WEB',
        name: 'Web Application',
        child: [
          { id: 'CMIS', name: 'CMIS' },
          { id: 'EQMP', name: 'EQMP' },
        ]
      },
    ]
  },
  {
    id: 'DEPT_ENGINEERING',
    name: 'CEMS'
  }
]

function findPath(str, object, path = []) {
  for (const [key, value] of Object.entries(object)) {
    if (value === str) {
      return [...path, value.id ? value.id : null]
    }
    if (value instanceof Object || value instanceof Array) {
      const newPath = findPath(str, value, [...path, value.id ? value.id: null])
      if (newPath) {
        return newPath.filter(item => item !== null)
      }
    }
  }
  return null
}

const path = findPath('EQMP', projects)
console.log(path) // ["DEPT_IT", "WEB", "EQMP"]
```

## Set

### Set operations - Subset, Union, Intersection, Symmetric Difference and Difference

```
let setA = new Set([1, 2, 3, 4])
let setB = new Set([2, 3])
let setC = new Set([3, 4, 5, 6])

// REMOVE DUPLICATE VALUE IN ARRAY
function removeDuplicate(array) {
    const set = new Set(array)
    return [...set]
}

console.log(removeDuplicate([1, 2, 3, 1, 2, 5, 6, 4, 3, 5]).sort())

// SUBSET
Set.prototype.subSet = function(otherSet) {
  if (this.size > otherSet.size) {
    return false
  } else {
    for (let elem of this) {
      if (!otherSet.has(elem))
      return false
    }
    return true
  }
}

console.log(`setA subset setB: ${setA.subSet(setB)}`) // false
console.log(`setB subset setA: ${setB.subSet(setA)}`) // true
console.log(`setB subset setC: ${setB.subSet(setC)}`) // false

// UNION
Set.prototype.union = function(otherSet) {
  let unionSet = new Set()
  for (let elem of this) {
    unionSet.add(elem)
  }
  for (let elem of otherSet) {
    unionSet.add(elem)
  }
  return unionSet
}

let unionSet = setA.union(setC)
console.log('Union setA > setC: ', unionSet.values()) // {1, 2, 3, 4, 5, 6}

// INTERSECTION
Set.prototype.intersection = function(otherSet) {
  let intersectionSet = new Set()
  for (let elem of otherSet) {
    if (this.has(elem))
    intersectionSet.add(elem)
  }
  return intersectionSet
}

let intersectionSet = setA.intersection(setB)
console.log('Intersection setA > setB: ', intersectionSet.values()) // {2, 3}

// SYMMETRIC DIFFERENCE
Set.prototype.symmetricDifference = function(otherSet) {
  let symmetricDifferenceSet = new Set(this)
  for (var elem of otherSet) {
    if (symmetricDifferenceSet.has(elem)) {
      symmetricDifferenceSet.delete(elem)
    } else {
      symmetricDifferenceSet.add(elem)
    }
  }
  return symmetricDifferenceSet
}

let symmetricDifferenceSet = setA.symmetricDifference(setC)
console.log('Symmetric Difference setA > setC: ', symmetricDifferenceSet) // {1, 2, 5, 6}

// DIFFERENCE
Set.prototype.difference = function(otherSet) {
  let differenceSet = new Set()
  for (let elem of this) {
    if (!otherSet.has(elem))
    differenceSet.add(elem)
  }
  return differenceSet
}

let differenceSet = setA.difference(setB)
console.log('Difference setA > setB: ', differenceSet.values()) // {1, 4}

const numArray = [11, 22, 33, ...setA.difference(setB)]
console.log(numArray) // [11, 22, 33, 1, 4]
```

## Array Destructuring

### Tic Tac Toe algorithm comparison

```
const matched = [
    [0, 1, 2],
    [1, 2, 3],
    [2, 3, 4],
    [0, 2, 4]
]

// WITHOUT DESTRUCTURING
const strArray1 = [null, 'A', 'A', 'A', null, null] // true
const strArray2 = [null, 'B', 'B', null, null, 'B'] // false

function findMatch(array, match) {
    for (var i=0; i<match.length; i++) {
        console.log(array[match[i][0]], array[match[i][1]], array[match[i][2]])
        if (array[match[i][0]] == array[match[i][1]] && array[match[i][0]] == array[match[i][2]]) {
            return 'Found Three \'' + array[match[i][0]] + '\' in Predefined Positions'
        }
    }
    return 'No Match'
}

console.log(findMatch(strArray1, matched)) // true
console.log(findMatch(strArray2, matched)) // false

// DESTRUCTURING
const strArrayDest1 = ['V', 'V', 'V', null, null, null] // true
const strArrayDest2 = ['W', null, 'W', null, 'W', null] // true
const strArrayDest3 = ['X', null, 'X', 'X', null, null] // false

function findMatchDesc(array, match) {
    for (const [index, str] of match.entries()) {
        const [start, middle, end] = match[index]
        console.log(array[start], array[middle], array[end])
        if (array[start] == array[middle] && array[start] == array[end]) {
            return `Found Three \'${array[start]}\' in Predefined Positions`
        }
    }
    return 'No Match'
}

console.log(findMatchDesc(strArrayDest1, matched)) // true
console.log(findMatchDesc(strArrayDest2, matched)) // true
console.log(findMatchDesc(strArrayDest3, matched)) // false
```
