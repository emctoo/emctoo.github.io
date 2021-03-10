### Nginx

#### rewrite to remove prefix

```nginx
location /dev/ {
  rewrite ^/dev/(.*)$ /$1 break;
  proxy_pass http://127.0.0.1:4000;
}

location /x/ {
  proxy_pass http://127.0.0.1:2000;
}
```

