# Notepad-PWA

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Description

A Progressive Web Application that functions as a Notepad to store text for later. The notepad supports JavaScript syntax as well.

## Table of Contents

- [Installation](#Installation)
- [Usage](#Usage)
- [License](#License)
- [Questions](#Questions)

## Installation

To host the program locally on your device: Download the files. Then, in your terminal run "npm i" in both the "client" and "server" folders to install the dependancies. Then, from the root folder run "npm start" to build and run the server.

## Usage

Enter text into the notepad to save it to refer to later. Text persists upon refresh so it won't be removed.

## License

[MIT License](https://opensource.org/licenses/MIT)

## Questions

Any questions regarding the application can be directed via GitHub or Email:
- [GitHub Profile](https://www.github.com/jacksonr-k)
- jrkbirdy@hotmail.com

## Credits

File: database.js

Source: Omar - Assistant Instructor
```
Code: 

// Add text to indexedDB
export const putDb = async (content) => {
  const jateDB = await openDB("jate", 1);
  const tx = jateDB.transaction("jate", "readwrite");
  const store = tx.objectStore("jate");
  const request = store.put({ id: 1, value: content });
  const result = await request;
  console.log(result);
};

// Retrieve text from indexedDB
export const getDb = async (e) => {
  const jateDb = await openDB("jate", 1);
  const tx = jateDb.transaction("jate", "readonly");
  const store = tx.objectStore("jate");
  const request = store.get(1);
  const result = await request;
  return result?.value;
};
```

File: src-sw

Source: Omar - Assistant Instructor
```
Code :

// Asset caching
registerRoute(
	// Here we define the callback function that will filter the requests we want to cache (in this case, JS and CSS files)
	({ request }) => ['style', 'script', 'worker'].includes(request.destination),
	new StaleWhileRevalidate({
	  // Name of the cache storage.
	  cacheName: 'asset-cache',
	  plugins: [
		// This plugin will cache responses with these headers to a maximum-age of 30 days
		new CacheableResponsePlugin({
		  statuses: [0, 200],
		}),
	  ],
	})
  );
```