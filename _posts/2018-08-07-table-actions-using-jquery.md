---
layout: post
title: "Table actions using jQuery"
date:   2018-08-07 15:13:00 +0800
categories: jquery
author: "John Aldrin Plata"
meta: "Springfield"
---

-- DRAFT --

```javascript
$.ajax({
  url: '/users',
  method: 'GET',
  success: function(users) {
    users.forEach(function(user) {
      $('tbody').append(`
        <tr>
          <td>${user.id}</td>
          <td>${user.name}</td>
          <td>${user.email}</td>
          <td>
            <a href="#">[Modify]</a>
            <a href="#">[Delete]</a>
          </td>
        </tr>
        `)
      });
    }
})
```

This will render a table like so:

| ID | Name     | Email          | Action            |
|----|----------|----------------|-------------------|
| 1  | John Doe | jdoe@emai.com  | [Modify] [Delete] |
| 2  | Foo Bar  | fbar@email.com | [Modify] [Delete] |

### Linking the element and javascript together

JavaScript `onclick` attribute accepts a function but it can only have native types as an argument. 

```javascript
<a onclick="someFunction('hello world', 2, 2 + 3)">Click me</a>
. . .
function someFunction(someString, someDigit, blah) {
    console.log('the string is ', someString);
    console.log('the digit is ', someDigit);
    console.log('the result is  ', blah);
}
```

But this is not possible
```javascript
<a onclick="someFunction({ firstName: 'John', lastName: 'Doe' })">Click me</a>
```

```javascript
$('tbody').append(`
  <tr>
    <td>${user.id}</td>
    <td>${user.name}</td>
    <td>${user.email}</td>
    <td>
    <a href="#" onclick="modifyUser()">[Modify]</a>
    <a href="#" onclick="deleteUser()">[Delete]</a>
    </td>
  </tr>
`)
```