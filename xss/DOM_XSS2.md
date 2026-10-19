

# [# DOM XSS in `innerHTML` sink using source `location.search`]

**Platform:** [Portswigger]  
**Topic:** [xss]

## 1. Goal
lab contains a DOM-based cross-site scripting vulnerability in the search blog functionality. It uses an `innerHTML` assignment, which changes the HTML contents of a `div` element, using data from `location.search`.

## 2. What I Did
The input parameter was stored in the image tag so I escaped the parameter variable and used the html event handler to perform an alert message

```js
<img src=1 onerror=alert(1)>
```

## 3. What Happened
The lab solved and the alert message popped up. 

## 4. Why It Worked
The input was in the image tag so we have to use the event handler instead of the full script tag. 

## 5. What I Learned
- The xss vulnerability can also be perform with the event handlers also not with the script tag only.

## 6. Key Takeaway
[This lab teaches me to perform xss without using the script tag.]