
# [# DOM XSS in jQuery anchor `href` attribute sink using `location.search` source]

**Platform:** [Portswigger]  
**Topic:** [xss]

## 1. Goal
This lab contains a DOM-based cross-site scripting vulnerability in the submit feedback page. It uses the jQuery library's `$` selector function to find an anchor element, and changes its `href` attribute using data from `location.search`.

## 2. What I Did
In the add comment section there was the path called return path so we can input our javascript query 

```js
javascript:alert(document.cookie)
```

## 3. What Happened
The code injected in the link worked and we got the document.cookie

## 4. Why It Worked
There was no authentication with the help of we can input any javascript query to the server.
## 5. What I Learned
- Links can be tricked with the javascript code also.
