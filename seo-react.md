# SEO + React

## Generic rules
* URLs should look like static URLs with directories as much as possible
* Some JavaScript-heavy sites or single-page apps have a hashtag in the URL, which Google likely would not crawl (e.g. https://www.alicesbooks.com/#scifi).
* Ensure consequential content is linked by `<a href>` links to ensure search engine discovery. Google may not follow a site's `onclick` events at all
* The initial content that loads before a user interacts should all be done server-side. After that, client-side rendering is OK.
* Google made an announcement in October 2015 mentioning that they would crawl the JS and CSS on websites as long as they allow the crawlers to access them.

## React Tools & Techniques

### URLs
* URLs : use **React Router** to build unique URL routes

### Server-side rendering

In Client-side rendering, your browser downloads a minimal HTML page. It renders the JavaScript and fills the content into it.

Server-side rendering, on the other hand, renders the React components on the server. The output is HTML content.

* Server-side rendering of the HTML can be done by using `ReactDOM.renderToString` instead of `ReactDOM.render`
* **React Helmet** can be useful to render head section elements such as meta tags.
*  **Next JS** is built specifically for server-side rendering and comes with its own internal routing library.

#### Isomorphic Javascript

An Isomorphic Javascript technology based React website automatically detects if the JavaScript is disabled on the client side. If so it serves a minimal HTML containing all key SEO data.

* [react-website tools](https://github.com/catamphetamine/react-website) 

#### Prerendering

Prerender will wait for the page to finish loading and then return the content in full HTML. Search engine crawlers can be targeted specifically to use Prerender (then see full HTML page result) while other browsers can still render the page by themselves (using React).

* **Prerender:**
The Prerender.io middleware that you install on your server will check each request to see if it's a request from a crawler. If it is a request from a crawler, the middleware will send a request to Prerender.io for the static HTML of that page. If not, the request will continue on to your normal server routes. The crawler never knows that you are using Prerender.io since the response always goes through your server.

## Misc

### Sources
* https://www.pmg.com/blog/seo-for-react-js-websites/
* https://it-consultis.com/blog/best-seo-practices-for-react-websites
* https://blog.digitalkwarts.com/server-side-rendering-with-reactjs-react-router-v4-react-helmet-and-css-modules/
* https://medium.freecodecamp.org/server-side-rendering-your-react-app-in-three-simple-steps-7a82b95db82e