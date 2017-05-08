---
title: "Nodejs notes"
author: lixiang
date: 2017-04-19 09:55
tag: nodejs
---

# Books

[Ebook: An Introduction to libuv](https://nikhilm.github.io/uvbook/index.html)


# StackOverflow Questions

[When is the thread pool used?](http://stackoverflow.com/questions/22644328/when-is-the-thread-pool-used)

> Node runs in **a single event loop**. It's single threaded, and you only ever get that one thread. All of the javascript you write executes in this loop, and if a blocking operation happens in that code, then it will block the entire loop and nothing else will happen until it finishes. This is the typically single threaded nature of node that you hear so much about. But, it's not the whole picture.
>
> Certain functions and modules, usually written in C/C++, support asynchronous I/O. When you call these functions and methods, they internally manage passing the call on to **a worker thread**. ... the strategy used by libuv to achieve asynchronous I/O is not always a thread pool, specifically in the case of the http module a different strategy appears to be used at this time.
>
> * Any external module that you include in your project that makes use of native C++ and libuv is likely to use the thread pool (think: database access)
> * libuv has a default thread pool size of 4, and uses a queue to manage access to the thread pool
> * You can mitigate this by increasing the size of the thread pool through the `UV_THREADPOOL_SIZE` environment variable, so long as you do it before the thread pool is required and created: `process.env.UV_THREADPOOL_SIZE = 10;`

[Confusion about node.js internal asynchronous I/O mechanism](http://stackoverflow.com/questions/15526546/confusion-about-node-js-internal-asynchronous-i-o-mechanism)

> * `libuv` perfroms async file I/O with a thread pool like `libeio`.
> * `libuv` does async network I/O based on the async I/O interfaces in different platforms, such as `epoll` `kqueue` `IOCP`, **without a thread pool**. There is a event loop which runs on the main thread of `uv` which polls the I/O events and processes them.
> * the thread pool inside `libuv` is **a fixed size thread pool**.

[Node.js Event loop](http://stackoverflow.com/questions/25568613/node-js-event-loop)
