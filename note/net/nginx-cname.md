# nginx 配置cname跳转

```javascript
server {
    listen 80;
    listen 443 ssl;
    server_name note.wangxiaokai.vip;
    ssl_certificate   cert/note.wangxiaokai.vip.pem;
    ssl_certificate_key  cert/note.wangxiaokai.vip.key;
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    return 301 https://hosting.gitbook.com;
}
```