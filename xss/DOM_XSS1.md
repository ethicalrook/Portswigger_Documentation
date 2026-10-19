
# [## DOM XSS in `'document.write` sink using source `location.search`]

**Platform:** [Portswigger]  
**Topic:** [XSS]

## 1. Goal
lab contains a DOM-based cross-site scripting vulnerability in the search query tracking functionality. It uses the JavaScript `document.write` function, which writes data out to the page.

## 2. What I Did
I escaped the img src tag and with the help of double quotes and then I wrote the alert message in the script tag
```js
"><script>alert("you are hacked")</script>
```

## 3. What Happened
It escaped and the error message pop up.

## 4. Why It Worked
The first double quotes with the angular bracket escapes the string and then we can write out malicious script for ex alert in the script tag

## 5. What I Learned
- Escaping the string tag
- DOM XSS Concepts

## 6. Key Takeaway
It is easy to escape the tag in the input section. and then we can put up our script there.