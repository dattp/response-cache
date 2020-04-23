<p align="center">
    <h2 align="center">Response cache</h2>
    <h4 align="center">Simple response caching middleware for ExpressJS using Redis</h4>
</p>

---



### Installation

```bash
npm install response-cache
```

#### Example
```js
// create redisClient
const redis = require('redis')
const ResponseCache = require('response-cache')
const redisClient = redis.createClient()
const responseCache = ResponseCache(redisClient)

const options = {
	duration: 60 // seconds,
}

app.get('/api/example', responseCache.cache(option), (req, res) => {
	  res.send('GET request to the homepage')
  })
  
// Cache all routes
app.use(responseCache.cache(option))
```
#### Clear cache
```js
// create redisClient
const redis = require('redis')
const ResponseCache = require('response-cache')
const redisClient = redis.createClient()
const responseCache = ResponseCache(redisClient)

// manually
app.get('/api/clear', (req, res) => {
	responseCache.clear('key') // clear cache for key in redis
	res.send('clears cache')
  })  
```


#### `options` object properties

| Property                   | Default   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| duration                       | 12 hours| ttl in redis                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| key                       | req.originalUrl      | key in redis                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| prefix_key                       |      | string: key in redis has a same prefix to facilitate remove multiple keys                                                                                                                                                                                                                                                                                                                                                                                                           |
