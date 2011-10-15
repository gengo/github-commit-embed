GitHub Commit Embeds with JavaScript
=======================================================================================
**[GitHub Gists](https://gist.github.com/)** are awesome for showcasing pieces of code in small
snippets, ideal for developer documentation and examples. Sadly, there currently exists no official
way to embed a specific commit or file from GitHub; they do, however, offer a stellar API, which we
can use to finagle commits out from within JavaScript in a fairly Gist-like manner.


How This Works
----------------------------------------------------------------------------------------
GitHub's API (V3) will allow you to retrieve a file at a given commit, but it's not exactly
the most clear API to work with. You need to supply a `hash-object` for said file, and the
response you get will (provided the hash is correct) be the Base64 encoded (with line breaks...?) version 
of the file itself.

This library handles all the behind the scenes aspects of forming the correct request, and returns
the decoded file as a string to your callback function. _This library does not give you syntax highlighting
like Gists do; combine it with something like **[SyntaxHighlighter](https://github.com/alexgorbatchev/SyntaxHighlighter)** to
get your desired effects._


How to get a File SHA
----------------------------------------------------------------------------------------
For each commit you want to pull down, you'll need to supply a File SHA that GitHub will
recognize. To do this, simply navigate to your repo in a terminal, and execute the following:

    git hash-object path_to_file

The result can be used for the `fileSHA` argument in the code below.


Example Usage
----------------------------------------------------------------------------------------
``` html
<!-- May want a pre/code tag combo here -->
<div id="code_block"></div>

<script type="text/javascript" src="path/to/githubcommitembed.min.js"></script>
<script type="text/javascript">
    // Create a new commit to fetch; .fetch() actually fires calls (below).
    var commit = new GitHubCommit({
        username: 'mygengo',
        reponame: 'mygengo-python',
        fileSHA: 'cbb0816e1fb873019d8617500e4562299663bf4f',
        node: 'code_block'
    });
	
    // Once we're safe and jazz, pull it down. 
	$(document).ready(function() {
		// Fetch the data and handle it 100% yourself after callback
		commit.fetch(function(content) {
			// Inject/highlight/etc with content (also as this.content)
		});
    });
</script>
```


Why Does This Exist?
----------------------------------------------------------------------------------------
At myGengo, we'd prefer to not have to maintain separate Gist-embeds for each of our API
repositories; we embed all our examples into our API documentation, though, so we wanted to
be able to re-use the same content whereever possible. Thus, this exists.

Credit for the `hash-object` tipoff that this library uses should go to **[Matt Swanson's GitHub API v3 blog post](http://swanson.github.com/blog/2011/07/09/digging-around-the-github-v3-api.html)**, as it was uber useful in figuring out what to even do.

Questions, Comments?
----------------------------------------------------------------------------------------
We're always interested in hearing from developers! You can find us at the following channels;
bugs and such should be filed on the **[GitHub Issue Tracker](https://github.com/myGengo/github-commit-embed)** for this 
repo. Pull Requests are welcome!

**[myGengo Devs on Twitter](http://twitter.com/mygengo_dev)**  
**[myGengo Devs on GitHub](http://github.com/myGengo/)**  
