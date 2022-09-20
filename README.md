# nextjs-dynamic-routing-custom-server

A custom server is unable to render dynamic routes on Next.js when the following conditions are met:

- Next.js `12.1.0` or above is used. Latest version known to work is `12.0.10`
- A custom server is used
- The production server as opposed to the dev server is used (e.g no `npx next dev`)
- `useFileSystemPublicRoutes` is disabled by Next.js configuration

## Scenario Next.js `12.0.10`

Prework:

```bash
npm install --no-save next@12.0.10
npx next build
NODE_ENV=production node server.js
```

Resolving dynamic route:

```bash
curl -v http://127.0.0.1:3000/sub/hello

*   Trying 127.0.0.1:3000...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 3000 (#0)
> GET /sub/hello HTTP/1.1
> Host: 127.0.0.1:3000
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< X-Powered-By: Next.js
< ETag: "4f3-0KDGwO715cAonxq/KE9KmXzeb/E"
< Content-Type: text/html; charset=utf-8
< Content-Length: 1267
< Vary: Accept-Encoding
< Date: Tue, 20 Sep 2022 21:11:06 GMT
< Connection: keep-alive
< Keep-Alive: timeout=5
```

## Scenario Next.js 12.1.0 or above (`12.3.1`)

Prework:

```bash
npm install --no-save next@12.3.1
npx next build
NODE_ENV=production node server.js
```

Resolving dynamic route:

```bash
curl -v http://127.0.0.1:3000/sub/hello

*   Trying 127.0.0.1:3000...
* TCP_NODELAY set
* Connected to 127.0.0.1 (127.0.0.1) port 3000 (#0)
> GET /sub/hello HTTP/1.1
> Host: 127.0.0.1:3000
> User-Agent: curl/7.68.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 404 Not Found
< X-Powered-By: Next.js
< ETag: "pea9ek4noo1tc"
< Content-Type: text/html; charset=utf-8
< Content-Length: 2352
< Vary: Accept-Encoding
< Date: Tue, 20 Sep 2022 21:12:11 GMT
< Connection: keep-alive
< Keep-Alive: timeout=5
```