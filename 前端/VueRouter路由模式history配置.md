https://blog.csdn.net/yuyanxinyu/article/details/136254358

```
const router = new VueRouter({
  routes: [

  mode: 'history'   //路由模式，默认hash，history模式需要后端做相关配置

})
```

后端服务器是nginx时，配置
```
location / {
    trry_files $uri $uri/ /index.html;
}
```
后端服务器是tomcat时，配置
```
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```
