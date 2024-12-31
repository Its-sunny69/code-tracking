# Random Quote Component Styling Improvements

This commit refactors the styling of the random quote component to enhance its visual appeal and readability.  The previous version included extra text within the author and date section. This has been removed to create a cleaner display. 

**Previous Code (Relevant Snippet):**

```jsx
<p className=" mt-2 font-medium">
  - by {author} on {dateAdded} very Good 
</p>
```

**Current Code:**

```jsx
import React, { useEffect, useState } from "react";
import Skeleton from "@mui/material/Skeleton";
import { Stack } from "@mui/material";

const RandomQuote = () => {
  const [quote, setQuote] = useState("");
  const [author, setAuthor] = useState("");
  const [dateAdded, setDateAdded] = useState("");
  const [loading, setLoading] = useState(true);

  const fetchQuote = async () => {
    try {
      const response = await fetch(
        "https://api.quotable.io/quotes/random?tags=inspirational|motivational|success|life"
      );
      const data = await response.json();
      setQuote(data[0].content);
      setAuthor(data[0].author);
      setDateAdded(data[0].dateAdded);
      setLoading(false);
    } catch (error) {
      console.error("Error fetching the quote:", error);
    }
  };

  useEffect(() => {
    fetchQuote();
  }, []);

  return (
    <div className="p-4 text-center flex flex-col justify-center items-center min-h-[8rem]">
      {loading ? (
        <div className="w-full flex flex-col justify-center items-center">
          <Stack
            spacing={-1}
            sx={{
              display: "flex",
              width: "100%",
              flexFlow: "column",
              justifyContent: "center",
              alignItems: "center",
            }}
          >
            <Skeleton
              variant="text"
              sx={{ fontSize: "1.5rem", width: "80%", marginY: "0px" }}
            />
            <Skeleton
              variant="text"
              sx={{ fontSize: "1.5rem", width: "60%", marginY: "0px" }}
            />
          </Stack>

          <Skeleton
            variant="text"
            sx={{ fontSize: "1rem", width: "30%", marginTop: "0.5rem" }}
          />
        </div>
      ) : (
        <>
          <p className="text-xl font-semibold italic">\"{quote}\"</p>
          <p className=" mt-2 font-medium">
            - by {author} on {dateAdded}
          </p>
        </>
      )}
    </div>
  );
};

export default RandomQuote;
```