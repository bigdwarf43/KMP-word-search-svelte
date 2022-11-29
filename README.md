# KMP Pattern searching

Pattern searching is an important problem in computer science. When we do search for a string in a notepad/word file or browser or database, pattern-searching algorithms are used to show the search results. The KMP matching algorithm uses degenerating property (pattern having the same sub-patterns appearing more than once in the pattern) of the pattern and improves the worst-case complexity to O(n). 

The basic idea behind KMP’s algorithm is: whenever we detect a mismatch (after some matches), we already know some of the characters in the text of the next window. We take advantage of this information to avoid matching the characters that we know will anyway match.


This is a simple implementation of the algorithm which is used to search for patterns in some text. 

### Check the deployed github pages environment

### for running the this svelte application locally follow this guide: https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/Svelte_getting_started#creating_your_first_svelte_app

## References:
https://towardsdatascience.com/pattern-search-with-the-knuth-morris-pratt-kmp-algorithm-8562407dba5b
https://benwendt.ca/articles/the-knuth-morris-pratt-algorithm-implemented-in-javascript/


![Screenshot 2022-11-29 201133](https://user-images.githubusercontent.com/62785185/204559364-92c8c94c-3dc6-4cac-ac2f-b28beec8e2de.png)
![Screenshot 2022-11-29 201200](https://user-images.githubusercontent.com/62785185/204559373-6b66dd49-9703-4e2d-bff4-29b6618ea6dc.png)
