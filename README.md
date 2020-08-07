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
