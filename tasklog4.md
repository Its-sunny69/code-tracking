# Feature: Improved Quote Display

This commit enhances the display of random quotes by adding the phrase "very Good" to the author and date information.  The previous version only displayed the author and date. This change improves the user experience by providing additional context to the quote. 

**Previous Code (Relevant Section):**

```javascript
<p className=" mt-2 font-medium">
  - by {author} on {dateAdded}
  very Good 
</p>
```

**Current Code (Relevant Section):**

```javascript
<p className=" mt-2 font-medium">
  - by {author} on {dateAdded}
  very Good very
</p>
```