django项目部署
------------------
### uwsgi
- uwsgi安装
```sh
pip install uwsgi
```
- 启动uwsgi web服务器
```sh
uwsgi --ini uwsgi.ini
```
- 更新配置文件，重启uwsgi
```sh
uwsgi --reload uwsgi.pid
```
- 关闭服务器
```sh
uwsgi --stop uwsgi.pid
```

### Nginx
- nginx安装
```sh
sudo apt-get install nginx
```
- nginx配置
```conf
# admin
upstream mn_project {
        server 127.0.0.1:8001;
}

server {
        listen  80;
        server_name     139.129.229.223;

        location /admin {
                include /etc/nginx/uwsgi_params;
                uwsgi_pass mn_project;
        }

        location /ckditor {
                include /etc/nginx/uwsgi_params;
                uwsgi_pass mn_project;
        }

        location / {
                root /root/mn_project/static_files;
                index index.html index.htm;
        }
}
```
- nginx代理服务器启动
```sh
/usr/sbin/nginx -c /etc/nginx/nginx.conf
```
- nginx代理服务器的重启
```sh
/usr/sbin/nginx -s reload
```
### 创建管理员用户&&数据库迁移
```sh
python manage.py createsuperuser

python manage.py makemigrations
python manage.py migrate
```
### 静态文件的收集
```sh
python manage.py collectstatic
```
