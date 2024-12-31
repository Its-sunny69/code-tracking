# Random Quote Component Styling

This commit refactors the styling of the `RandomQuote` component to improve its visual presentation.  The previous version lacked specific styling, resulting in a less visually appealing component. This update enhances the display of quotes and their associated information by applying the following changes:

- **Improved Layout:** The layout of the component is refined for better alignment and spacing using Tailwind CSS classes.  Specifically, the `p-4`, `text-center`, `flex flex-col justify-center items-center`, and `min-h-[8rem]` classes provide proper padding, text alignment, and minimum height.
- **Typography Enhancements:** The typography is improved to enhance readability. The quote itself is displayed using `text-xl font-semibold italic` classes, while the author and date are displayed with `mt-2 font-medium`.
- **Skeleton Screen Improvements:** While the skeleton screen remains unchanged, its integration with the updated styling ensures visual consistency during loading.

The updated `RandomQuote` component now renders more visually appealing and user-friendly display of random quotes. 

```javascript
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