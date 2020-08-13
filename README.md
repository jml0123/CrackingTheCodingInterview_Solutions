# Cracking the Code Interview Solutions
*This file contains JavaScript solutions to Cracking The Coding Interview (6th Edition)* 
### 1.1 Find unique characters
#### Solution 1 (Using str.sort())
```
function hasUniqueChars(str){
  const arr = str.split('');
  const sorted = arr.sort();
  for (let i = 0; i < sorted.length; i += 2) {
    if (sorted[i] === sorted[i+1]) {
      return false;
    }
  }
  return true;
}
```
```
function hasUniqueChars(str){
  const arr = str.split('')
  const sorted = arr.sort()
  for (let i = 0; i < sorted.length - 1; i += 1) {
    if (sorted[i] === sorted[i+1]) {
      return false
    }
  }
  return true
}
```
```
function hasUniqueChars(str){
  const sorted = str.split("").sort()
  let prev = null;
  let curr = "";
  for (i = 0; i < sorted.length; i++) {
    if(prev === curr) {
      return false
    }
    curr = sorted[i]
    prev = (!sorted[i - 1])? null: sorted[i - 1]
  }
  return true
}
```
#### Solution 2 (Using Set and nested loop to check if chars are equal)
```
function hasUniqueChars(str){
  const chars = str.split("")
  const unique = Array.from(new Set(chars))
  for (char of unique) {
    let count = 0;
    for (c of chars){
      if(c === char){
        count++
      }
      if (count > 1) {
        return false
      }
    }
  }
  return true
}
```
#### Solution 3 (Elegant js solution || Compare set size and string length)
```
const hasUniqueChars = (str) => new Set(str).size === str.length;
```
### 1.2 Check if string is permutation
```
const isPermutation = (str1, str2) => {
 const arr1 = str1.toLowerCase().split('').sort();
 const arr2 = str2.toLowerCase().split('').sort();
 return (arr1.toString() === arr2.toString());
}
```
 

### 1.3 URLify (Replace spaces with ‘%20’)
#### Solution 1 (Split string into array and filter out white spaces to then join)
```
const URLify = (str, n) => {
  return str.split(' ').filter(w => w !== '').join('%20');
}
```
#### Solution 2 (Creates new string, iterates through original and add %20 if whitespace)
```
function createURL(str, strLen){
  let fixed = ""
  let length = 0
  for(char of str) {
    length ++
    if (length > strLen) {
      return fixed
    }
    fixed += (char === " ")? "%20": char
  }
  return fixed
}
```


### 1.4 Check Permutation
#### Solution 1 (Checks to see if there are leftovers)
```
const checkPermutation = (str) => {
  // if odd, there will be 1 letter without a pair
  // if even, all letters should have a pair
  const chars = str.toLowerCase().split("")
  // create a leftovers array that should only equal 1 or 0 if a palindrome can be formed
  const leftovers = []
  for (char of chars) {
    if (!leftovers.includes(char)) {
      leftovers.push(char)
    }
    else {
      let toRemove = leftovers.indexOf(char);
      leftovers.splice(toRemove, 1)
    }
  }
  // if odd
  if (str.length % 2 !== 0) {
    if (leftovers.length === 1) {
      return true
    }
    else {
      return false
    }
  }
  // if even 
  else if (str.length % 2 === 0) {
      if (!leftovers.length) {
      return true
    }
    else {
      return false
    }
  }
}

```
#### Solution 2 (Using a sort to check if subsequent values are equal)
```
const checkPermutationSort = (str) => {
  const chars = str.toLowerCase().split('').sort()
  for (let i = 0; i < chars.length - 1; i+=2) {
    // if even
    if (chars.length % 2 === 0) {
      if (chars[i] !== chars[i+1]) {
        return false
      }
    }
    // odd
    else {
      if (chars[i] !== chars[i+1]) {
        // check next pair
        // but make sure youre not at the end of array
        if (i+2 >= chars.length) {
          return false
        }
        else {
          if (chars[i+1] !== chars[i+2]) {
            return false
          }
        }
      }
    }
  }
  return true
}
```
### 1.5 OneAway (checks if difference between two strings is 1 insertion, deletion, replacement)
#### Solution 1
```
const oneAway = (str1, str2) => {
  const chars1 = str1.toLowerCase().split('')
  const chars2 = str2.toLowerCase().split('')
  const c1Len = chars1.length
  const c2Len = chars2.length

  if (Math.abs(c1Len - c2Len) > 1) {
    return false
  }

  let edits = 0
  let j = 0

  if (c1Len === c2Len) {
    for(let i = 0; i < chars1.length; i++) {
      if (chars1[i] !== chars2[i]) {
        edits++
      }
    }
  }
  else {
    let longerArr = c1Len > c2Len? chars1 : chars2
    let shorterArr = c1Len < c2Len? chars1 : chars2
    for(let i = 0; i < longerArr.length; i++) {
      if (longerArr[i] !== shorterArr[j]) {
        edits++
      }
      else {
        j++
      }
    }
  }

  return edits === 1
}
```
#### Variation of above (exits loop immediately if edits greater than 1)
```
const oneAway = (str1, str2) => {
  const split1 = str1.toLowerCase().split("")
  const split2 = str2.toLowerCase().split("")
  let edits = 0
  let j = 0;
  if (str1.length === str2.length){
    for (i = 0; i < split1.length; i++) {
      if (split1[i] !== split2[i]){
        if (edits > 1) {
          return false
        }
        edits++
      }
    }
  }
  else {
    if (Math.abs(str1.length - str2.length) !== 1) {
       return false
    }
    let longerStr = (str1.length > str2.length)? str1: str2
    let longerArr = (longerStr === str1)? split1: split2
    let shorterArr = (longerStr === str1)? split2: split1
    for (i = 0; i < longerArr.length; i++) {
      if(shorterArr[j] !== longerArr[i]) {
        if (edits > 1) {
          return false
        }
        edits++ 
      }
      else {
        j++
      }
    }
  }
  return edits === 1
}
```
### 1.6 String Compression (iterate through each character and keep track of count)
```
const strCompress2 = (str) => {
  const letters = str.split('')
  let currLetter = letters[0]
  let count = 0
  let compressedStr = ''

  for(let i = 0; i < letters.length; i++) {
    // console.log(letters[i])
    if (currLetter === letters[i]) {
      count++ 
      if (i === letters.length - 1) {
        compressedStr+=`${currLetter}${count}`
      }
    }
    else {
      compressedStr+=`${currLetter}${count}`
      currLetter = letters[i]
      count = 1
    }
  }
  compressedStr+=`${currLetter}${count}`

  return compressedStr.length > str.length ? str : compressedStr
}
```
#### Variation that includes an initial check to see if string is already compressed. Less efficient version due to nested loop
```
const stringCompression = (str) => {
  // Checking to see if string is already 'compressed'
  // aka no repeating characters
  // If so return original string
  const uniqueCheck = Array.from(new Set(str)).sort()
  const chars = str.split("")
  const sortedChars = ([...chars]).sort()
  if (uniqueCheck.toString() === sortedChars.toString()) {
    return str
  }
  // If there are repeating characters
  // Do the algorithm
  let compressed = ""
  let collection = 0
  let currIndex = 0;
  let j;
  for (i = 0; i < chars.length; i++) {
    let currentChar = chars[currIndex]
    j = currIndex;
    while (chars[j] && chars[j] === chars[currIndex]) {
      console.log(chars[j])
      collection++
      j++
    }
    compressed += `${currentChar}${collection}`
    collection = 0;
    currIndex = j
    if (!chars[j]){
      return compressed
    }
  }
  return compressed
}
```
### 1.7 Rotate n X n Matrix
#### Not in place (using deep copy)
```
const rotateMatrix = (matrix) => {
  let currRow = 0;
  let changingCol = matrix[0].length - 1
  // Deep copy the matrix to reference it
  // Not sure if this is "in place"?
  const copy = JSON.parse(JSON.stringify(matrix));
  for (let i = 0; i < matrix.length; i++){
    for (let j = 0; j < copy[i].length; j++) {
        matrix[currRow][changingCol] = copy[i][j]
        currRow++
        if (matrix[currRow]=== undefined){
          currRow = 0;
          break
        }
      }  
    changingCol--
    }  
  return matrix
}

// for length of row move to the next col, if i > length, move down
```
#### In place 
```
const rotateInPlace = (matrix) => {
  const length = matrix.length

  for (layer = 0; layer < Math.floor(length / 2); layer++) {
    const first = layer;
    const last = length - 1 - layer

    for (let i = first; i < last; i++) {
      const offset = i - first;
      const top = 
        matrix[first][i] // saves top

      // left -> top
      matrix[first][i] = 
        matrix[last - offset][first]

      // bottom -> left
      matrix[last - offset][first] = 
        matrix[last][last - offset]

      // right -> bottom
      matrix[last][last - offset] = 
        matrix[i][last]

      // top -> right
      matrix[i][last] = 
        top // right <- saved top
    }
  }
  return matrix
}

```
### 1.8 Zero Matrix (Check to see if row includes matrix, set that row to zero, and add that index to a zero index array, another loop to set whole column to zero)
#### Solution 1
```
const zeroMatrix = (matrix) => {
  const zeroRow = new Array(matrix[0].length)
  zeroRow.fill(0)

  numRows = matrix.length;
  let zeroColIndex;
  let zeroColIndices = []

  for(row = 0; row < numRows; row++) {
    if (matrix[row].includes(0)) {
      zeroColIndex = matrix[row].indexOf(0)
      zeroColIndices.push(zeroColIndex)
      matrix[row] = zeroRow
    }
  }
  matrix.forEach(m => {
    zeroColIndices.forEach(c => {
      m[c] = 0
    })
  })
  return matrix
}
```
#### Solution 2 (create new array, triple nested loop to check for and fill with 0s)
```
const zeroMatrix = (matrix, m, n) => { 
  // m=rows, n=cols
  // create new array to return
  let newMatrix = new Array(m)
  for (let i = 0; i < m; i++) {
    newMatrix[i] = new Array(n)
  }

  for (let r = 0; r < m; r++) {
    for (let c = 0; c < n; c++) {
      if (matrix[r][c] === 0) {
        // fill row
        newMatrix[r].fill(0)
        // fill col
        for (let i = 0; i < m; i++) {
          newMatrix[i][c] = 0;
        }

      }
    }
  }

  // fill remaining nonzero values
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (newMatrix[i][j] !== 0) {
        newMatrix[i][j] = matrix[i][j]
      }
    }
  }
  return newMatrix
}
```