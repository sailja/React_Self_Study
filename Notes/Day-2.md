# How to create a react project

- Open terminal
- Go to folder where you want to create project
- run `npx create-react-app@<react-version> <project name>` for now use version 5 and hit enter
  It will take some time to create project
- Open the project on VS code

You can see the node-modules folder having all the required packages installed.
All the Assets for the project like all the images or index file in the public folder

To start a react project we can use the start script in the package.json file.

- open terminal
- go to the project folder
- run `npm run start` or `npm start`
- you can see your application running in localhost:3000

# Review of Essential Javascript for react

React is a JS library therefore we need a good understanding of JS fundamentals

## Destructuring Objects and Arrays

Destructuring is very very useful when we want to get some object out of an object or an array.

```
const books =
     {
    id: 1,
    title: 'The Lord of the Rings',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    pages: 1216,
    translations: {...},
    reviews: {...}
  }

const title = book.title;
const author = book.author;
```

In the above example we can see that in order to get a particular value from an object we use the `.` operator. to get all the data in the above manner can be cumbersome. Here destructuring comes to the rescue.

```
const {title, author, hasMovieAdaptation, reviews} = books;

```

With destructuring we can get all the data from books object in a single line of code. All we have to do is specify the property name that we want to get. one thing to keep in mind is that the variable name should match the property names mentioned in the object.
Similarly we can destructure arrays using the below mentioned syntax;

```
const array = [1, 2, 3];
const [value1, value2, value3] = array;
```

here value1 is 1 value 2 is 2 and value3 is 3.

## Rest and Spread operator

For arrays if we want to get all the array values except the first in another array . we can use the below syntax

```
const array = [1, 2, 3,4, 5, 6];
const [first, ...otherValues] = array;
```

output: first - 1
otherValues - [2, 3, 4, 5, 6];

If we want to use the `... operator` (Rest operator) to destructure an array. It should always be the last one.

Similarly we have the spread operator. The spread operator basically does the opposite of rest operator. The rest operator clubs all the remaining values to another array. The spread operator takes out all the values (basically spreads an array). Below is the synctax for spread operator.

```
const array = [1, 2,3];
const newArray = [...array,4,5];

output -> newArray = [1, 2, 3, 4, 5];
```

### Spread operator on objects

```
const book = {
    id: 1,
    title: 'The Lord of the Rings',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    pages: 1216,
    translations: {...},
    reviews: {...}
  }

const updatedBook = {...book, publicationData: '01-01-2010'}

Output -> updatedBook = {
    id: 1,
    title: 'The Lord of the Rings',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    pages: 1216,
    translations: {...},
    reviews: {...},
    publicationData: '01-01-2010'
  }

```

we can also use spread operator to update a property in an object. For example if we want to update the pages property in the book object all we have to do is.

```
const updatedBook ={
    ...book,
    pages: 1222
};

output -> updatedBook = {
    id: 1,
    title: 'The Lord of the Rings',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  }

```

## Template Literals

Template literals are ES6 jS feature that allows us to create JS string that contains some JS variables/ expression inside of a string. we use back ticks for template literals

```
const book = {
    id: 1,
    title: 'The Lord of the Rings',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  }
 const summary = `${book.title} is book-6`;
 output -> 'The Lord of the Rings is book-6'
```

basically if we want to add any dynamic value in a string we use template literals. We can use the variable(dynamic value) inside `${}` in the string.

## Ternaries instead of if/else statements

There are 3 parts in a ternary operator. Condition, true value and false value.

```
Syntax:

condition ? true : false;
example:

const a  = 2;
const b = 3;
 a+b > 6 ? 'It is greater' : 'it is less';

 output => It is less.
```

Basically in the condition we define what we want to check. true value is what we want to do if the condition is true and in the false value we add what we want to do if the condition is false.

## Arrow functions

Arrow functions is a new ES6 feature used to write quick and short one line functions.
Below example explains the difference in arrow function and normal function.

```
//Normal function
function getYear(str) {
    return str.split("-")[0];
}

//Arrow function
const getYear = (str) => str.split("-")[0];

```

for single line code we dont need {} or return. But for longer code we need them.

```

const getYearMonth = (str) => {
    const year = str.split("-")[0];
    const month = str.split("-")[1];
    return {year, month};
}
```

## Short-circuiting and logical operators

In Js some operators such as && or || have featue called short-circuiting. It means that in certain conditions the operator will immediately return the first value and not even look at the second value.

&& - this short circuits when the first value is true the operator will return the second value immediately. if the first value is false it will return the first value and not look into the second value

example:

```
true && 'some content' ----> some content
false && 'some content' ----> false

```

This also works with truthy and falsy value

falsy value = 0, '', null, undefined
truthy value = everything other than falsy value.

|| - this short circuits whenever the first operand is true and wil return the first value.
But if the first value is false it will return the second value

```
true || 'some content' ----> true
false || 'some content' ---> some content
0 || 'some content' ---> some content
'truthy value' || 'some content' ---> truthy value

```

?? - nullish coelising operator works very similar to || operator but it does short circuit for the false value.

```
0 ?? 'some content' ---> 0
undefined ?? 'some content' ---> some content
```

## Optional chaining

```
const object = [{count: 1, book: 'book 1', review: 10}, {count: 10, book: 'book 2'}, {count: 5, book: 'book 3'}]

const getCount =(book){
const count = book.count;
const review = book.review;

return count + review
}

console.log(getCount(object[0])); //11
console.log(getcount(object[1])); // we get error here because object[1] does not have review
```

In JS to avoid this error we can use optional chaning to avoid undefined error. optional chaining is basically using a `?` before `.` operator in an object to check if the value exists

```
const object = [{count: 1, book: 'book 1', review: 10}, {count: 10, book: 'book 2'}, {count: 5, book: 'book 3'}]

const getCount =(book){
const count = book?.count;
const review = book?.review;

return count + review
}

console.log(getCount(object[0])); //11
console.log(getcount(object[1])); // NaN : here the output is not correct but we won't get hard error because we used optional chaining in review variable.
to get correct value we can simply use nullish coelishing in book?.review

const review = book?.review ?? 0; Here if book.review is undefined 0 gets set to review
```

## Array Map method

This is an array function which returns a new array with same length as the original array based on the operation performed.

```
const books = [
   {
    id: 1,
    title: 'The Lord of the Rings',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
   {
    id: 2,
    title: 'The Lord of the Rings 2',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
   {
    id: 3,
    title: 'The Lord of the Rings 3',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  }
]

const updated = books.map(element => {
  return {
    id: element.id,
    title: element.title
  }
})

Output --->
console.log(updated);
[
   {
    id: 1,
    title: 'The Lord of the Rings'
  },
   {
    id: 2,
    title: 'The Lord of the Rings 2'
  },
   {
    id: 3,
    title: 'The Lord of the Rings 3'
  }
]
```

Here the output length is same as the original array length but the content only consists of the id and name as we have returned in the map function.

## Array Filter method

Array filter method basically returns a new array having values that satisfy the condition mentioned in the filter method.

Baically filters an array based on the condition.

```
const books = [
   {
    id: 1,
    title: 'The Lord of the Rings'
  },
   {
    id: 2,
    title: 'The Lord of the Rings 2'
  },
   {
    id: 3,
    title: 'The Lord of the Rings 3'
  }
]


const filteredBooks = books.filter(el => el.id === 1);
console.log(filteredBooks);

Output --->

[{
    id: 1,
    title: 'The Lord of the Rings'
}]
```

In the above example a new array is created having books with id 1

# Array Reduce method

The reduce method is the most verstile and the most powerful array method in JS.
We can implement all the methods using the reduce method.

let's say we want to read all the books in an array and we want to know all the pages that we have to read.

The reduce method basically reduces the entire array to one value.
There are 2 arguments first is the function and 2nd is the starter value. In the function on the first argument we also have 2 arguments 1 is the accumuator and second is the array element. The accumulator is the current value of the final value. Basically in all the iterations the value is stored in the accumulator. Basically in accumulator we keep on storing values till the last iterations

```
const books = [
   {
    id: 1,
    title: 'The Lord of the Rings',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
   {
    id: 2,
    title: 'The Lord of the Rings 2',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
   {
    id: 3,
    title: 'The Lord of the Rings 3',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  }
]

const pagesAllBooks = books.reduce((acc, book)=> acc + book.pages, 0);
console.log(pagesAllBooks);
// 3666
```

## Array Sort method

This method is used to sort an array. There are 2 arguments in the sort array first(current value) and second(next value). In the callback function if a negative value is returned then the 2 values will get sorted in ascending way. and if postive then in descending way

```

const x = [3, 7, 1, 2, 9];
const sorted = x.sort((a, b) => a - b);
Output ----> [1,2,3,7,9];

const sortedDescending = x.sort((a, b) => b - a);
Output ----> [9, 7, 3, 2,1]
```

Unlike other array methods sort function does not create a new array. It basically mutated the original array. However, we won't want that to happen. Therefore, in order to avoid original array mutation we can create a copy of the original array and then sort it.

```
const sorted = x.slice().sort((a, b) => a - b);
sorted ---> [1,2,3,7,9];
x ----> [3, 7, 1, 2, 9]
```

## Working with immutable array

In React may operations need to be immutable. It is important to know how to add, delete and modify an array without changing the original array

```
const books = [
   {
    id: 1,
    title: 'The Lord of the Rings',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
   {
    id: 2,
    title: 'The Lord of the Rings 2',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
   {
    id: 3,
    title: 'The Lord of the Rings 3',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  }
]

// Add book object to array

const newBook = {
    id: 4,
    title: 'Harry porter 1',
    publicationDate: '1954-07-29',
    author: 'J. k. Rowling',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  }

  const booksAfterAdd = [...books, newBook];

  Output --->
  [
   {
    id: 1,
    title: 'The Lord of the Rings',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
   {
    id: 2,
    title: 'The Lord of the Rings 2',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
   {
    id: 3,
    title: 'The Lord of the Rings 3',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
  {
    id: 4,
    title: 'Harry porter 1',
    publicationDate: '1954-07-29',
    author: 'J. k. Rowling',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  }
]


//Delete a book

const booksAfterDelete = booksAfterAdd.filter(item => item.id !== 1);
Output ---->
[
   {
    id: 2,
    title: 'The Lord of the Rings 2',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
   {
    id: 3,
    title: 'The Lord of the Rings 3',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
  {
    id: 4,
    title: 'Harry porter 1',
    publicationDate: '1954-07-29',
    author: 'J. k. Rowling',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  }
]


// Update a book

const booksAfterUpdate = booksAfterDelete.map(item => {
  return item.id === 2 ? {...item, pages: 1252} : item
});

Output ---->
[
   {
    id: 2,
    title: 'The Lord of the Rings 2',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1252
  },
   {
    id: 3,
    title: 'The Lord of the Rings 3',
    publicationDate: '1954-07-29',
    author: 'J. R. R. Tolkien',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  },
  {
    id: 4,
    title: 'Harry porter 1',
    publicationDate: '1954-07-29',
    author: 'J. k. Rowling',
    genres: Array(6) [...],
    hasMovieAdaptation: true,
    translations: {...},
    reviews: {...},
    pages: 1222
  }
]


```

## Asynchronous JS Promises

To fetch data from an API we have the fetch API. JS does not wait for the fetch function to complete execution. It will simple start executing the fetch and then simply move to the next line. So how do we wait for the fetch code and do something when data arrives? This is where JS asynchronous operations come into play. Fetch function returns a promise. Promise has multiple states (pending, rejected, fulfilled). This can be handled using then method. `then` method will be called as soon as the promise is fulfilled. Inside the then will be a callback function which will be called after the promise is completed.

The fetch function starts executing and the JS moves to other line (not the `then` method) till the fetch response arrives. As soon as the response is recieved the JS will execute the then operation

```
fetch('https://jsonplaceholder.typicode.com/todos').then((res) => res.json()).then((data) => console.log(data));

```

## Async Await

In the above example we use then. Similar operation can be performed with easier and cleaner way using async await.

Let us create a async function. Here we have created an async function and we have used await before fetch. Here JS will not move to next line inside getTodos function till the fetch response is recieved. It basically performs the same operation as above just in a more cleaner and managable way. The await will work only inside the async function. If we have any call after the function is called
that will get executed first and will not wait for the await.

```
async function getTodos() {
  const res = await fetch('https://jsonplaceholder.typicode.com/todos');
  const data = await res.json();
  console.log(data)
}
```
