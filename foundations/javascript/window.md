# window

Window is top object of Javascript, it also represents the current interactive window, all global attributes are mounted on it.

There are some important attributes as well:

* history
    > Which is strongly associated with `Routing System`, mainly because when we get back or forward in history, there is no need to reload whole page. we also have a greate user experence in our web application. In html5, `history` object has introduced `pushState`, we can create any history in current `document` without reload multi-documents at all, and it is perfect for script-heavily web app. There is another way to implement it without refresh whole page using `hash` in the URL. .but it looks a little ugly. Sometimes, not too friendly to search engine.`location.hash` and `window.addEventListener('hashchange',hashChangeHandler);`

* 