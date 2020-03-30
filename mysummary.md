> from (https://www.talater.com/upup/getting-started-with-offline-first.html)
> forked at: (https://github.com/farisubuntu/UpUp.git)
## UpUp: Make your web pages offline:
- This tutorial will show you how to add offline functionality to your site in under 10 minutes. 

### Let's get started

We'll start with a simple site, and add the offline features to it:

```html
<html>
<head>
  <meta charset="UTF-8">
  <title>Lonely Globe Advisor</title>
</head>
<body>
  <h1>Top Hotels in Rome</h1>
  <ol>
    <li>Villa Domus - Via Piacenza 9, Rome, Italy</li>
    <li>Hotel Trivelli - Piazza Barberini 11, Rome, Italy</li>
  </ol>
</body>
</html>
```

Our sample site, Lonely Globe Advisor, offers visitors a list of the top hotels in Rome, with user ratings and an address.

But what happens if our user just landed in Rome and doesn't have a local data plan?

Well, he'll be out of luck.

### Adding Basic Offline Content

We can control the experience our users get when they are offline with 2 simple steps:

1.  Include the UpUp script in our page.
2.  Define the content we'd like the user to see when they are offline.

```html
<html>
<head>
  <meta charset="UTF-8">
  <title>Lonely Globe Advisor</title>
</head>
<body>
  <h1>Top Hotels in Rome</h1>
  <ol>
    <li>Villa Domus - Via Piacenza 9, Rome, Italy</li>
    <li>Hotel Trivelli - Piazza Barberini 11, Rome, Italy</li>
  </ol>
  <script src="/upup.min.js"></script>
  <script>
    UpUp.start({
      'content': '<html><body><h1>Top Hotels in Rome</h1><p>Villa Domus</p><p>Hotel Trivelli</p></body></html>'
    });
  </script>
</body>
</html>
```

In the code above we simply told UpUp to display some simple HTML the next time a user can't access our site.

With just this tiny bit of code, we've added an offline experience for our site, and allowed our users to see the best hotels in Rome… even when they can't access the web.	

#### How Does It Work?

UpUp uses service workers to determine when network requests fail. A service worker is a special script that runs in the browser in the background, and can see the status of network requests.

When the user first visits your site, UpUp registers a service worker with your browser, and gives it a list of files to cache for later.

The next time the user visits your site, the service worker listens for network errors. If a network request fails, and the service worker finds that file in the cache, it will return that file, as if it came from the network.

### Creating a rich offline experience

- We'll begin by moving our offline content to a separate file. This will make it much easier to update and maintain, and we'll no longer have to include the entire content of the offline site on every page:

```html
<html>
<head>
  <meta charset="UTF-8">
  <title>Lonely Globe Advisor</title>
</head>
<body>
  <h1>Top Hotels in Rome</h1>
  <ol>
    <li>Villa Domus - Via Piacenza 9, Rome, Italy</li>
    <li>Hotel Trivelli - Piazza Barberini 11, Rome, Italy</li>
  </ol>
  <script src="/upup.min.js"></script>
  <script>
    UpUp.start({
      'content-url': 'offline.html'
    });
  </script>
</body>
</html>
```

Now the content our users see when they are offline, is the contents of  `offline.html`. This is just a simple HTML file, no different than any other page on our site.

Our  `offline.html`  file contains two css files:  `bootstrap.min.css`  and  `offline.css`. Let's make sure these are cached and available to our users when they are offline:

```html
<html>
<head>
  <meta charset="UTF-8">
  <title>Lonely Globe Advisor</title>
</head>
<body>
  <h1>Top Hotels in Rome</h1>
  <ol>
    <li>Villa Domus - Via Piacenza 9, Rome, Italy</li>
    <li>Hotel Trivelli - Piazza Barberini 11, Rome, Italy</li>
  </ol>
  <script src="/upup.min.js"></script>
  <script>
    UpUp.start({
      'content-url': 'offline.html',
      'assets': ['css/bootstrap.min.css', 'css/offline.css']
    });
  </script>
</body>
</html>
```

#### Where Should I Place My Files?

For security reasons, the browser only lets UpUp's service worker see network requests within its scope.

The scope that the service worker can affect is determined by where you placed  `upup.min.js`  and  `upup.sw.min.js`. For example, if you place it on  `https://yoursite.com/js/upup.sw.min.js`, UpUp will only be able to show your offline content when users try to look at the  `/js/`  directory.

This is why it is important to place both files on the same server as your content, and not in a subdirectory. This should idealy be in the root of your site (e.g. https://yoursite.com/upup.min.js).

### Getting fancy

With just one command and two settings, we can create rich offline experiences for our users. These can be as simple as the examples above, or as robust as a full single page application using frameworks like AngularJS, with content customized for each user, videos and even files the user can access while offline.

```html
<script src="/upup.min.js"></script>
<script>
  UpUp.start({
    'content-url': 'schedule.html?user=joe', // show this when the user is offline
    'assets': [                 // define additional assets needed while offline:
      'img/logo.png',           // such as images,
      'css/offline.css',        // custom stylesheets,
      'schedule.json?user=joe', // dynamic requests with data per user,
      'js/angular.min.js',      // javascript libraries and frameworks,
      'mov/intro.mp4',          // videos,
      'contacts.pdf'            // and more.
    ]
  });
</script>
```

#### HTTPS Only

To preserve the user's security and privacy, service worker can only detect requests over a secure connection.

During development you can use UpUp through localhost (e.g.  `http://localhost/`  or  `http://localhost:1234/`  are ok), but to deploy it to production you'll need to have HTTPS set up on your server.

This is a requirement for many new web technologies, and you can get free SSL certificates these days, so don't let that stop you… progress is coming.

#### Browser Support

UpUp plays nicely with all browsers, progressively enhancing browsers that support Service Workers, while leaving users with older browsers unaffected.

UpUp currently supports Chrome 40+, Opera 27+ and Firefox 41+. If your users are using a different browser, they simply won't notice anything different.

#### Downloading:
https://github.com/TalAter/UpUp/raw/master/dist/upup.zip
