# docker-haproxy-nginx-subcomponent-nginx

# Build & Run docker
```sh
$ docker-compose up
# Sample Output:
Attaching to docker-haproxy-nginx_nginx3_1, docker-haproxy-nginx_nginx1_1, docker-haproxy-nginx_nginx2_1, docker-haproxy-nginx_haproxy_1
haproxy_1  | <7>haproxy-systemd-wrapper: executing /usr/local/sbin/haproxy -p /run/haproxy.pid -f /usr/local/etc/haproxy/haproxy.cfg -Ds 
nginx1_1   | 172.18.0.4 - - [17/Mar/2019:07:37:03 +0000] "GET / HTTP/1.1" 200 12 "-" "curl/7.54.0" "-"
nginx2_1   | 172.18.0.4 - - [17/Mar/2019:07:37:04 +0000] "GET / HTTP/1.1" 200 12 "-" "curl/7.54.0" "-"
nginx3_1   | 172.18.0.4 - - [17/Mar/2019:07:37:05 +0000] "GET / HTTP/1.1" 200 12 "-" "curl/7.54.0" "-"
nginx1_1   | 172.18.0.4 - - [17/Mar/2019:07:37:05 +0000] "GET / HTTP/1.1" 200 12 "-" "curl/7.54.0" "-"
nginx2_1   | 172.18.0.4 - - [17/Mar/2019:07:37:06 +0000] "GET / HTTP/1.1" 200 12 "-" "curl/7.54.0" "-"
nginx3_1   | 172.18.0.4 - - [17/Mar/2019:07:37:06 +0000] "GET / HTTP/1.1" 200 12 "-" "curl/7.54.0" "-"
nginx1_1   | 172.18.0.4 - - [17/Mar/2019:07:37:06 +0000] "GET / HTTP/1.1" 200 12 "-" "curl/7.54.0" "-"
nginx2_1   | 172.18.0.4 - - [17/Mar/2019:07:37:07 +0000] "GET / HTTP/1.1" 200 12 "-" "curl/7.54.0" "-"
nginx3_1   | 172.18.0.4 - - [17/Mar/2019:07:37:07 +0000] "GET / HTTP/1.1" 200 12 "-" "curl/7.54.0" "-"
nginx1_1   | 172.18.0.4 - - [17/Mar/2019:07:37:07 +0000] "GET / HTTP/1.1" 200 12 "-" "curl/7.54.0" "-"
```

2. Open a new terminal and run

Sample Input/Output
```sh
$ curl http://localhost:8080
myhost:cel_test sudharch$ curl http://localhost:8080
From nginx1

$ curl http://localhost:8080
myhost:cel_test sudharch$ curl http://localhost:8080
From nginx2
```

In the above example application traffic is routed to one of the backend servers which is called layer 4 (aka TCP) routing.

Often in production environment backend servers serves specific app page request inside your application.
Eg: http://yourapplication.com/blog, here the user request is to provide blog page information. This is called layer 7 (aka HTTP)  routing.

Sample Input/Output
```sh
$ curl http://localhost:8080/blog.html
Blog App
Serving Blog page from nginx3

$ curl http://localhost:8080/blog.html
Blog App
Serving Blog page from nginx4
```

This setting is defined inside haproxy.cfg like below

acl blog_app_url path_beg /blog

For more details check this file: haproxy/haproxy.cfg
