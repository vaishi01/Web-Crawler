# Web Crawler
A standalone C-based web crawler that recursively retrieves and stores web pages starting from a seed URL. The web crawler follows internal links up to a specified depth, saving each page's content locally in a directory with a unique document ID for each page.

## Features
Internal Link Crawling: Only crawls web pages within the same domain as the seed URL.
Customizable Crawl Depth: Allows users to specify a maximum depth for crawling (0–10).
Efficient Storage: Saves the HTML content of each crawled page locally with a unique document ID, while recording the depth and URL for reference.
Politeness Policy: Ensures the crawler pauses for at least one second between fetching pages to avoid overwhelming the server.
Error Handling: Gracefully handles invalid URLs, depth limits, and file creation issues with appropriate error messages.

## Installation
Prerequisites: Install the required libraries:
```bash
sudo apt install libcurl4 libcurl4-gnutls-dev
```
Clone the Repository:
```bash
./crawler <seedURL> <pageDirectory> <maxDepth>
```
Build: Compile the project with the following command:
```bash
gcc -o webcrawler [source_files] -lcurl
```


## Usage:
To run the crawler, use the following syntax:
```bash
./crawler <seedURL> <pageDirectory> <maxDepth>
```

## Files:
crawler.c & crawler.h: Implements the main web crawling functionality.
curl.c & curl.h: Handles HTTP requests and fetching of web pages.
pagedir.c & pagedir.h: Manages storage of the fetched pages in the specified directory.
url.c & url.h: URL parsing and normalization functions.

## Example:
```bash
./crawler http://example.com ./pages 2
```
In this example:

The crawler will start at http://example.com.
It will save the crawled pages in the ./pages directory.
It will crawl internal links up to a depth of 2.

## Output
The crawler saves each crawled page in the specified directory. The file format is as follows:

The file name is the document ID (starting from 1).
The first line of each file contains the full URL of the page.
The second line contains the depth of the page.
The remaining content is the raw HTML of the page.

Example output:
http://example.com
0
<!DOCTYPE html>
<html>
<head>
    <title>Example Domain</title>
</head>
<body>
    <h1>Example Domain</h1>
    <p>This domain is for use in illustrative examples in documents.</p>
    ...
</body>
</html>

## Functional Overview

## Main Functions:
main(): Parses the command-line arguments and starts the crawling process.
crawl(): Implements the core logic of fetching web pages, extracting links, and following them recursively up to maxDepth.
pagefetcher(): Uses libcurl to fetch the contents of a given URL.
pagescanner(): Scans the HTML of a page to extract and normalize all internal links.
pagesaver(): Saves the crawled page, along with the URL and depth information, to the specified directory.

## Helper Modules:
bag of pages: A simple data structure to hold the pages to be crawled.
hashtable of URLs: Keeps track of URLs that have already been seen and prevents duplicate crawling.

## Error Handling
The web crawler will handle and exit gracefully with appropriate error messages in cases such as:
Invalid URL format.
Non-existent or inaccessible page directory.
Invalid maxDepth value (must be between 0 and 10).
Out of memory or file creation errors.
Network errors when fetching web pages.


