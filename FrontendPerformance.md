### Frontend Performance  tips:

- Modern approaches such as lazy loading, image optimization, and JavaScript optimization are essential for mobile-first experiences.
- Reducing HTTP requests is one of the most effective ways to improve loading speeds.
- Control caching with HTTP headers sent by your server:
    - Cache-Control: This is the boss. It tells the browser how to cache (e.g., "Keep this for 30 days").
    - Expires: An older way of setting a "best before" date on a file.
    - ETag: A "fingerprint" for a file. If the file hasn't changed since the last visit, the server tells the browser, "Your version is still good, don't download it again."
- 1. Node.js (using Express): In Node.js, if you are using the Express framework, you can set headers manually using res.set() or automatically for static files.

**Manual implementation:**
JavaScript
---
``` app.get('/api/data', (req, res) => {
  // Sets Cache-Control to 1 hour (3600 seconds)
  res.set('Cache-Control', 'public, max-age=3600');
  
  // Express calculates ETags automatically, but you can set custom ones:
  res.set('ETag', 'v1.2.3');

  res.json({ message: "This is cached data" });
});
````

For Static Files (Best Practice):
**JavaScript**
---
```

// Automatically handles ETags and Cache-Control for a whole folder
app.use(express.static('public', {
  maxAge: '1d', // Sets Cache-Control for 1 day
  etag: true    // Enables ETag generation
}));
```

2. PHP In PHP, you use the header() function. These commands must be called before any HTML or text is printed to the screen.
```
<?php
// Set Cache-Control: Public means it can be cached by anyone, 
// max-age is in seconds (3600 = 1 hour)
header("Cache-Control: public, max-age=3600");

// Set Expires (using PHP's gmdate to format it correctly)
$expireTime = gmdate("D, d M Y H:i:s", time() + 3600) . " GMT";
header("Expires: $expireTime");

// Manually setting an ETag (usually a hash of the content)
$etag = md5("content_of_your_page");
header("ETag: \"$etag\"");

// Logic to check if the browser already has the file
if (isset($_SERVER['HTTP_IF_NONE_MATCH']) && trim($_SERVER['HTTP_IF_NONE_MATCH']) == "\"$etag\"") {
    header("HTTP/1.1 304 Not Modified");
    exit;
}

echo "This content is now cached.";
?>
```

3. **Java (Spring Boot)** : In modern Java development with Spring Boot, you have elegant ways to handle this using the ResponseEntity builder or Filters.
Using ResponseEntity (Specific Route):

```
@GetMapping("/logo")
public ResponseEntity<byte[]> getLogo() {
    byte[] image = imageService.getLogo();

    return ResponseEntity.ok()
            .cacheControl(CacheControl.maxAge(30, TimeUnit.DAYS)) // Cache-Control
            .eTag("v1.0") // ETag
            .body(image);
}
Global ETag Configuration: Instead of doing it for every route, you can add a "Filter" that creates a "fingerprint" (ETag) for every response automatically:


**Java**
@Bean
public ShallowEtagHeaderFilter shallowEtagHeaderFilter() {
    return new ShallowEtagHeaderFilter();
}  
```

- Use compress images -> !) lossless compression to retain perfect quality and 2) lossy compression for slightyl reduce quality for smaller size file
- Implement Lazy Loading to Prioritize Visible Content First
- -Native lazy loading: Supported by modern browsers using the loading="lazy" attribute:
```
<img src="image.jpg" loading="lazy" alt="Description">
<video loading="lazy" controls>
  <source src="video.mp4" type="video/mp4">
</video>
```
- Using the Intersection Observer API for more control and broader support
- Minimize JavaScript and CSS Files to Optimize Performance
- Use Asynchronous Loading for JavaScript to Boost Rendering using **async and differ**
- Implement Critical CSS to Improve Initial Rendering
- Use Content Delivery Networks to Improve Website Speed
- Use SVGs for Lightweight and Scalable Graphics for Faster Media
- Implement Server-Side Rendering to Boost Content Delivery
-  Optimize JavaScript Execution to Shape a Better User Experience
-  Use HTTP/2 to Improve Resource Delivery Speed
-  Use GZIP or Brotli Compression to Speed Up Data Transfer
-  Defer Non-Essential CSS to Enhance Rendering
```
<link rel="stylesheet" href="critical.css">
<link rel="stylesheet" href="desktop.css" media="screen and (min-width: 1024px)">
<link rel="stylesheet" href="print.css" media="print">
```
- Use Cache-Control Headers to Get Optimal Resource Caching
- Reduce CSS Complexity to Improve Front-End Efficiency




