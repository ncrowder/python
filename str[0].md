We had a list that contained categories and months that was created from a split on a string, such as Sales_Jan which became then [Sales, Jan].  This does appear like a list, but to pull out a specific part of that, like the first position (element = 0) we used .str[0] approach, because we saw that otherwise [0] simply pulls out the first position entirely, so [‘Sales’,’Jan’].  You could use [0][0] and get just the ‘Sales’ part.  But then to apply that for the entire series (column) you’d end up needing something like this:
```
melted['Category2'] = melted['Category_Month'].str.split('_').map(lambda x: x[0])
```
The map would work on each element in the category_month column after the split (each element is a list) and then pull out the first element of each list.  So this would be an alternative approach.  However, clearly this is more succinct: 
```
melted['Category'] = melted['Category_Month'].str.split('_').str[0]
```
The confusing part is why it’s part of the .str methods since as we pointed out it’s a list after the split and not a string.  Quite frankly, I thought about it for a while yesterday and didn’t have a good explanation beyond what I had already said, that it just works that way because it’s working on each element within the column.  It’s essentially a shortened “syntax sugar” version of something like what I wrote above.  However, I found one site that mentioned the following:

.str works on a series of strings OR OBJECTS THAT BEHAVE LIKE STRINGS.  It notes that “behave like strings” includes lists and tuples if you’re applying a function that makes sense for a sequence, which in this case means it’s iterable (we can reference a piece of it using an index position).

In any case, I hope that helps at least somewhat.  It will be true for you, and it was true for me as well (as well as everyone on Earth), but there are a few things you eventually have to take on faith and learn how to use, and understanding will hopefully come later.
