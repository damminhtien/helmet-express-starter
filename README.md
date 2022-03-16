# helmet-express-starter
```javascript
const app = express();
app.use(helmet.hidePoweredBy()); // remove the X-Powered-By header.
app.use(helmet.frameguard({action: 'deny'})); // mitigate the Risk of Clickjacking
app.use(helmet.xssFilter()); // mitigate the Risk of Cross Site Scripting (XSS) Attacks
app.use(helmet.noSniff()); // avoid Inferring the Response MIME Type
app.use(helmet.ieNoOpen()); // prevent IE from Opening Untrusted HTML
let ninetyDaysInSeconds = 90*24*60*60;
app.use(helmet.hsts({ maxAge: ninetyDaysInSeconds, force: true })); // ask Browsers to Access Your Site via HTTPS Only
/* To improve performance, most browsers prefetch DNS records for the links in a page. In that way the destination ip is already known when the user clicks on a link. This may lead to over-use of the DNS service (if you own a big website, visited by millions people…), privacy issues (one eavesdropper could infer that you are on a certain page), or page statistics alteration (some links may appear visited even if they are not). If you have high security needs you can disable DNS prefetching, at the cost of a performance penalty. */
app.use(helmet.dnsPrefetchControl()); // disable DNS Prefetching
app.use(helmet.noCache()); // disable Client-Side Caching
/* By setting and configuring a Content Security Policy you can prevent the injection of anything unintended into your page. This will protect your app from XSS vulnerabilities, undesired tracking, malicious frames, and much more. CSP works by defining an allowed list of content sources which are trusted. You can configure them for each kind of resource a web page may need (scripts, stylesheets, fonts, frames, media, and so on…). There are multiple directives available, so a website owner can have a granular control. See HTML 5 Rocks, KeyCDN for more details. Unfortunately CSP is unsupported by older browser. */
app.use(helmet.contentSecurityPolicy({ directives: { defaultSrc: ["'self'"], scriptSrc: ["'self'", "trusted-cdn.com"] }} ));
```
