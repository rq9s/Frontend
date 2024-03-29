## Installation

Once you are in your Ubuntu machine run the following script.

```shell
cd /var/www
rm -r /var/www/BloxSafe
git clone https://github.com/BloxSafe/Frontend.git BloxSafe
cd BloxSafe
npm install
npm run build
killall nginx
nginx
```

Once done, Open `./src/settings.js` and Change `window.$productionURL` to your BloxSafe backend url. open nginx config file on your machine(`/etc/nginx/sites-enabled/default`) and add this configuration to it.

```js
// /src/settings.js
export default {
  $productionURL: "YOUR_BACKEND_SERVER_URL_GOES_HERE",
  $developmentURL: "http://localhost:5000",
};
```

```nginx
server {
    listen 80;
    server_name bs.jubot.site; ## Your Server Name(If you got one)
    root /var/www/BloxSafe/dist;
    index index.html index.htm;

    location / {
        try_files $uri $uri/ /index.html;
    }

    error_log  /var/log/nginx/vue-app-error.log;
    access_log /var/log/nginx/vue-app-access.log;
}
```

and finally

```shell
killall nginx
nginx
```
