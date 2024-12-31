# Random Quote Component Update

This commit updates the `RandomQuote` component to include the word "very" after the date in the quote display.  The previous version only displayed the author and date.

**Previous Code (Relevant Snippet):**
```javascript
<p className=" mt-2 font-medium">
  - by {author} on {dateAdded}
</p>
```

**Current Code (Relevant Snippet):**
```javascript
<p className=" mt-2 font-medium">
  - by {author} on {dateAdded} very
</p>
```

This seemingly small change adds a bit of stylistic flair to the quote presentation. The rest of the component's functionality (fetching quotes, handling loading states, skeleton loading) remains unchanged.