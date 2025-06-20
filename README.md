{
  "name": "Pedido Especial 💍",
  "short_name": "Pedido",
  "start_url": "pedido_pwa.html",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#ffc0cb",
  "icons": [{
    "src": "icon.png",
    "sizes": "192x192",
    "type": "image/png"
  }]
}

self.addEventListener('install', function(e) {
  e.waitUntil(
    caches.open('pedido-cache').then(function(cache) {
      return cache.addAll([
        'pedido_pwa.html',
        'manifest.json',
        'icon.png'
      ]);
    })
  );
});

self.addEventListener('fetch', function(e) {
  e.respondWith(
    caches.match(e.request).then(function(response) {
      return response || fetch(e.request);
    })
  );
});
