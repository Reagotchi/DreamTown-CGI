nginx configuration:


```
location ~ ^/friends/cgi-bin/auth/5555$ {
        rewrite /friends/cgi-bin/auth/5555 /friends/cgi-bin/auth/5555/index.cgi last;
}

location ~ (cgi-bin|cgi)/ {
        include snippets/pythoncgi.conf;
        gzip off;
        root <path to tamagotchi town site files>;

        fastcgi_pass unix:/var/run/fcgiwrap.socket;
        fastcgi_param DOCUMENT_ROOT <same as document root>;
        fastcgi_param DT_DATABASE_USER "<MARIADB USERNAME HERE>";
        fastcgi_param DT_DATABASE_PASSWORD "<MARIADB PASSWORD HERE>";
        fastcgi_param DT_DATABASE_HOST "<MARIADB HOST HERE>";
        fastcgi_param DT_DATABASE_PORT "<MARIADB PORT HERE>";
        fastcgi_param DT_DATABASE_NAME "<MARIADB DATABASE NAME HERE>";
        fastcgi_param PYTHONPATH <path to friends/cgi-bin>;
        fastcgi_index index.cgi;
        include /etc/nginx/fastcgi_params;
}
```