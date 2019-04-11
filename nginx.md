# nginx 

## http handling

<pre>
http
ngx_http_block
ngx_http_optimize_servers
ngx_http_init_listening
ngx_http_add_listening
ls = ngx_create_listening(cf, &addr->opt.sockaddr.sockaddr,
                              addr->opt.socklen);
ngx_http_init_connection
ls->handler = ngx_http_init_connection; -> ngx_http_wait_request_handler

ngx_http_proxy_handler
post_handler set to ngx_http_upstream_init
rc = ngx_http_read_client_request_body(r, ngx_http_upstream_init);


http wait request handler	// ngx_http_wait_request_handler
recv
reusable connection:0
http process request line
http request line: "GET /api HTTP/1.1"
http uri: "/api"
http process request header line
http header
http header done
event timer
rewrite phase:0
test location "/api"
using configuration "/api"
http cl:-1 max:1048576
rewrite phase: 2
post rewrite phase: 3
generic phase: 4
..
generic phase: 10
http init upstream, client timer: 0
http script copy: "Host"
http proxy header
"GET /api HTTP/1.0^M
Host: localhost:8000^M
Connection: close^M
User-Agent: curl/7.54.0^M
Accept: */*^M
http cleanup add
get rr peer
stream socket 
connect to 
http upstream connect: -2
http finalize request: -4, "/api?" a:1, c:2

</pre>
