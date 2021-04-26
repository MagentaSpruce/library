# library
Library project for The Odin Project using HTML, CSS, and JS




This project helped me to practice and better understand:

1) HTML tables
2) SVG sprite files
3) CSS grid/flexbox
4) Text-align: -webkit-match-parent property
5) DOM manipulation
6) Creating and implementing functions
7) Testing
8) JS coding
9) Working with objects
10) Using local storage


This project has the following known bugs which need correcting:
The images do not load properly despite the liver-server showing the page correctly and all of the files being uploaded. The anchor tags and sign-in button lack any functionality.

A general walkthrough of the project and it's noteworhy code is as follows:

To begin, the DOM elements and starting parameters must be constructed.
```JavaScript
let library;
let book;
const DEFAULT_DATA = [
    {name: "The Count of Monte Cristo", author: "Dumas", status: "read"},
    {name: "Master and Commander", author: "O'Brian", status: "read"},
    {name: "Romance of the Three Kingdoms", author: "Luozhong", status: "not read"},
]

const name = document.querySelector('#name');
const author = document.querySelector('#author');
const status = document.querySelector('#status');
const tableBody = document.querySelector("#book-table-body");
```

Next create a class for book and attach event listeners to the form and table.
```JavaScript
class Book {
  constructor(name, author, status) {
    this.name = name;
    this.author = author;
    this.status = status;
  }
    }
    
const form = document.querySelector('#form').addEventListener('submit', formSubmit);
const table = document.querySelector("table").addEventListener("click", removeBook)
```

Next create the functions required. 
```JavaScript

const formSubmit = (e) => {
  e.preventDefault();
  addBookToLibrary();
  render();
  clearForm();
};

const removeBook = (e) => {
  const currentTarget = e.target.parentNode.parentNode.childNodes[1];
  if(e.target.innerHTML === 'delete'){
       if(confirm(`Are you sure you want to delete ${currentTarget.innerText}`))
      deleteBook(findBook(library, currentTarget.innerText));}
       updateLocalStorage();
       render();
  };
  
function addBookToLibrary() {
  name.value.length === 0 || author.value.length === 0 ? alert("Please fill in all fields 🤗") : console.log('Test spot');

  const newBook = new Book(name.value, author.value, status.value);
      
  library.push(newBook);
  updateLocalStorage();
  }

function changeStatus(book) {library[book].status === "read" || library[book].status === "reading" ? status : "not read"}
      
    
function deleteBook(currentBook) {
    library.splice(currentBook, currentBook + 1);
    }

      
  
function findBook(libraryArray, name) {
    if (libraryArray.length === 0 || libraryArray === null) {
        return;
    }
    for (book of libraryArray)
      if (book.name === name) {
         return libraryArray.indexOf(book);
    }
      }


function clearForm() {
  name.value = "";
  author.value = "";
      }


function updateLocalStorage() {
    localStorage.setItem("library", JSON.stringify(library)); 
      }

function checkLocalStorage() {
    if (localStorage.getItem("library")) {
      library = JSON.parse(localStorage.getItem("library"));
    } else {
      library = DEFAULT_DATA;
    }
  }
      
function render() {
    checkLocalStorage();
      tableBody.innerHTML = "";
      library.forEach((book) => {
    const htmlBook = `
        <tr>
          <td>${book.name}</td>
          <td>${book.author}</td>
          <td><button class="status-button">${book.status}</button></td>
          <td><button class="delete">delete</button></td>
        </tr>
            `;
      tableBody.insertAdjacentHTML("afterbegin", htmlBook);
        });
      }
      
render();

```

All of these functions are JS code is straight forward and so no further explantation is neccessary.
***End Walkthrough
