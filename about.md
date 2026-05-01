---
layout: page
title: About
permalink: /about/
---

just a developer on side quest.

<span id="letterboxd-entry">loading last watched movie...</span>

<script>
(function () {
  fetch('https://servelesscors-zeta.vercel.app/api/cors?url=https://letterboxd.com/itsabiral/rss/')
    .then(function (r) { return r.json(); })
    .then(function (d) {
      document.getElementById('letterboxd-entry').innerHTML =
        'last watched movie from my <a href="https://letterboxd.com/itsabiral/">letterboxd</a> is ' +
        '<a href="' + d.href + '" target="_blank" rel="noopener">' + d.title + '</a>' +
        ' (' + d.year + ') and i rated it ' + d.stars
    })
    .catch(function () {
      document.getElementById('letterboxd-entry').innerHTML = 'last watched movie from my <a href="https://letterboxd.com/itsabiral/">letterboxd</a> is unavailable';
    });
})();
</script>

#### contact

[me@abiral.com](mailto:me@abiral.com) or social links above
