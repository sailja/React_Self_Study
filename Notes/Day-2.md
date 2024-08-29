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

In JS to avoid this error we can use optional chaning to avoid undefined error.

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
