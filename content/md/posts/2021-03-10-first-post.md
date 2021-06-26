{:title "Better Python String Formatting Using f-strings"
 :layout :post
 :tags  ["python"]}

As an avid Python user, I’ve always been jealous of how JavaScript users can seamlessly put together strings and expressions using template literals:

```javascript
>>> const a = 5;
>>> const b = 10;
>>> console.log(`Fifteen is ${a + b}).`;
==> "Fifteen is 15."
```

That is an extremely elegant solution, as opposed to the de facto standard of using Python string formatting:

You might say, “But, Adrian! The Python version doesn’t seem so bad.” And you’re correct… when we’re talking about using single expressions. But what if we’re using more than one?

Skim through the following code examples in both JavaScript and Python to see how quickly things can get tricky.

Here’s the JavaScript version: