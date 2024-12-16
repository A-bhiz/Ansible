# Ansible

https://www.tecmint.com/install-wordpress-nginx-rhel-linux/


https://www.tecmint.com/install-nginx-mysql-php-on-rhel-8/

[nginx-stable]
name=nginx stable repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=1
enabled=1




sudo dnf install php php-fpm php-mysqlnd php-xml php-gd php-mbstring php-curl -y
gpgkey=https://nginx.org/keys/nginx_signing.key
module_hotfixes=true

#########₹₹₹₹##########


 server {
    listen 80;
    server_name your_server_ip;

    root /var/www/html/wordpress;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include /etc/nginx/fastcgi_params;
        fastcgi_pass unix:/run/php-fpm/www.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location ~ /\.ht {
        deny all;
    }
}
