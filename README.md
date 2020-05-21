# Better file copier

Self proclaimed better file copier then the rest.

Better file copier is a node package to allow you to copy a file or folder.
Yeah.... as simple as that...

But why bother making one?

# Why?

 - Because all major folder recursive copy package are unable to handle big file (greater than 0x1fffffe8 characters). Better Copy will copy anything regardless it size!
 - Another file copier will hit your RAM harder the larger the file you copy.
 - More customize event on the process of copying, such as onBeforeCopy, or onAfterCopy, etc
 - Options to switch into the OS' native file copy command
 - Because I'm bored!

# Usage
Bare minimum command :
```javascript
const bCopy = require('better-copy');

//bCopy(from, to, options, callback)
bCopy('/path/to/your/moreThan2TBFiles.ext', '/path/to/destination/file.ext')
.then((result) => {
	console.log(result)
})
```
Resolved result are an object containing pairs of source & destination path :

    {
	    "/source/path/1" : [
		    "/destination/path/1",
		    "/destination/path/2"
		    ...
		    ]
		"/source/path/2" : [...]
    }


A single command to copy both file or folders :
```javascript
const bCopy = require('better-copy');

// copy file to a directory, assuming the same file name
bCopy('/path/to/your/file.txt', '/path/to/destination/folder');

// copy directory recursively
bCopy('/path/to/your/folder', '/path/to/destination/folder');
```

Copy from & into multiple file/directory at once:
```javascript
const bCopy = require('better-copy');

// use an array as parameter for more than one input path
bCopy(['/path/to/your/folder1', '/path/to/some/file.txt'], '/path/to/destination/folder');

// Copy some file into multiple directory
bCopy(['/path/to/your/folder'], 
	[
		'/path/to/destination/folder', 
		'/path/to/other/folder'
	]);
```

# Options

```javascript
// The default value of the options parameter
bCopy('/path/to/your/folder1', '/path/to/destination/folder', 
	{
		filter:function(from, to) {
			// return false to exclude
			// return true to include
			return true;
		},
		onAfterCopy : function(from, to) {},
		onBeforeCopy : function(from, to) {},
		overwrite : false, // will overwrite the target if set true
		useShell : false, // use shell copy if possible (not all OS are supported)
				
	});
```
Filtering example
```javascript
// Copy only the zip file
var path = require('path');
copy('F:/source/', ['F:/destination/'], {
	filter:function(from, to) {
		console.log("handling ", from);
		if (path.extname(from).toLowerCase() == '.zip') {
			console.log("extension is zip, skipping")
			return true;
		}
		return false;
	}
})
.then(function(result) {
	console.log("Copied files :", result)
})
```
# License

MIT License

Copyright (c) 2020 Dreamsaviors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.