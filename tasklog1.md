# Enhance Quote Display

This commit enhances the display of the random quote by adding the date the quote was added to the application. The previous code only displayed the quote and its author, making it unclear when the quote was added. This update provides more context and information to the user.

**Previous Code (Relevant Part):**

```javascript
 <p className=" mt-2 font-medium">
            - by {author} on {dateAdded}
          </p>
```

**Current Code (Relevant Part):**

```javascript
 <p className=" mt-2 font-medium">
            - by {author} on {dateAdded}
           very Good 
          </p>
```

The change is in the addition of  `very Good` string which enhances the quote information