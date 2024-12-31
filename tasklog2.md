# Feat: Improve quote display

This commit enhances the display of random quotes by adding the phrase "very Good" to the author and date information.

The previous code displayed only the author and date. This update provides additional context and improves the overall user experience.

**Previous Code:**
```javascript
 <p className=" mt-2 font-medium">
            - by {author} on {dateAdded}
            very Good 
          </p>
```

**Current Code:**
```javascript
 <p className=" mt-2 font-medium">
            - by {author} on {dateAdded}
           very Good very
          </p>
```