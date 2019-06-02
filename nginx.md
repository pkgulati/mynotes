# nginx http handling
* http block of configuration
* HTTP Connection 
* HTTP proxy 
* Wait for request
* Process Request
* Events
* Handlers
* SSL
* Busy 
* Upstream

## http block of configuration
* ngx_http_block
* ngx_http_optimize_servers
    * For each 
        * create ngx_listening for listening address using ngx_create_listening
        * set ngx_http_init_connection handler on ngx_listening ; 
        * ngx_http_init_listening
        * ngx_http_add_listening
        * ngx_create_listening
* location handler is set as ngx_http_proxy_handler for http proxy

## HTTP Connection 
* ngx_http_add_listening calls ngx_http_init_connection
* ngx_http_init_connection handler 
* set read handler = ngx_http_wait_request_handler
* ngx_http_connection_t is set as data in connection object and once we start receiving request is set as data

## HTTP proxy 
* ngx_http_proxy_handler 
* post_handler set to ngx_http_upstream_init
* ngx_http_read_client_request_body(r, ngx_http_upstream_init);

## Wait for request 
* This is the 1st handler called upon receiving data on socket (after SSL handshake)
* ngx_http_wait_request_handler waits for incoming requests
* calls ngx_http_create_request to create a new request
* invokes ngx_http_process_request_line
* ngx_http_wait_request_handler is set as handler in ngx_http_init_connection
* ngx_reusable_connection
* set read event handler as ngx_http_process_request_line

## Process Request
* ngx_http_process_request_line is the read event handler invoked by wait request handler
* sets handlers
   * connection -> read event handler = ngx_http_request_handler;
   * connection -> write event handler = ngx_http_request_handler;
   * request -> read event handler = ngx_http_block_reading;
* will parse request line ngx_http_parse_request_line, ngx_http_process_request_headers, ngx_http_read_request_header, 
* finally if NGX_HTTP_PARSE_HEADER_DONE,
* post_handler in proxy handler is set to ngx_http_upstream_init (passing ngx_http_request_t)
* ngx_http_upstream_init will invoke ngx_http_upstream_connect and ngx_http_upstream_send_request
* invokes ngx_http_handler
* invokes ngx_http_run_posted_requests

## Response From Upstream
* ngx_http_upstream_process_header reading response header from upstream
* It will do process_header
* It will call ngx_http_upstream_process_downstream
* upstream_done will be true if completed, then it will invoke ngx_http_upstream_finalize_request


## upstream handling request
* ngx_http_upstream_init
* ngx_http_upstream_connect
* ngx_handle_write_event
* ngx_http_upstream_send_request_body
* location resolver
* ngx_http_upstream_resolve_handler
* ngx_http_upstream_create_round_robin_peer


## ctx
ngx_http_set_ctx
ngx_http_get_module_ctx

## ngx_event_get_peer

## ngx_http_set_ctx

### ngx_post_event

### elts, nelts
elements and number of elements

## ngx_event_get_peer


addr = port->addrs.elts;
last = port->addrs.nelts;

### ngx_http_optimize_servers

### creating object using pool
r = ngx_pcalloc(pool, sizeof(ngx_http_request_t));

ngx_http_writer
ngx_http_finalize_request
ngx_http_finalize_connection 
ngx_http_set_keepalive
ngx_http_set_keepalive 
ngx_http_process_request_line
    ngx_http_parse_request_line
ngx_http_process_request_line
ngx_http_process_request_headers
ngx_http_process_request
ngx_http_handler(r);
ngx_http_run_posted_requests(c);

### phases
void ngx_http_core_run_phases(ngx_http_request_t *r);
ngx_int_t ngx_http_core_generic_phase(ngx_http_request_t *r,
    ngx_http_phase_handler_t *ph);
ngx_int_t ngx_http_core_rewrite_phase(ngx_http_request_t *r,
    ngx_http_phase_handler_t *ph);
ngx_int_t ngx_http_core_find_config_phase(ngx_http_request_t *r,
    ngx_http_phase_handler_t *ph);
ngx_int_t ngx_http_core_post_rewrite_phase(ngx_http_request_t *r,
    ngx_http_phase_handler_t *ph);
ngx_int_t ngx_http_core_access_phase(ngx_http_request_t *r,
    ngx_http_phase_handler_t *ph);
ngx_int_t ngx_http_core_post_access_phase(ngx_http_request_t *r,
    ngx_http_phase_handler_t *ph);
ngx_int_t ngx_http_core_content_phase(ngx_http_request_t *r,
    ngx_http_phase_handler_t *ph);


### content handler
ngx_http_update_location_config

### ngx_http_core_content_phase

### ngx_http_proxy_merge_loc_conf
will set core location conf handler = ngx_http_proxy_handler

ngx_http_core_loc_conf_t
if (clcf->lmt_excpt && clcf->handler == NULL
        && (conf->upstream.upstream || conf->proxy_lengths))
    {
        clcf->handler = ngx_http_proxy_handler;
    }

### ngx_http_proxy_handler
post_handler set to ngx_http_upstream_init
rc = ngx_http_read_client_request_body(r, ngx_http_upstream_init);


### ngx_http_request_handler

### ngx_http_block_reading

### ngx_http_handler
client_header_buffer_size
ngx_http_core_run_phases

### ngx_http_handler
client_header_buffer_size
ngx_http_core_run_phases
extern ngx_queue_t  ngx_posted_accept_events;
extern ngx_queue_t  ngx_posted_events;
ngx_http_upstream_connect
ngx_http_upstream_handler
ngx_http_set_write_handler


### ngx_http_run_posted_requests
* ngx_http_request_handler(ngx_event_t *ev)
* For every request
    * read_event_handler
    * write_event_handler
* pahses are run ngx_http_core_run_phases
* ngx_http_init_phases
* ngx_http_init_headers_in_hash
* ngx_http_init_phase_handlers
* ngx_http_optimize_servers
    * For each 
        * ngx_http_init_listening
        * ngx_create_listening
        * set handler ngx_http_init_connection

### ngx_http_mirror_init as handler flow
* ngx_http_mirror_init is handler which on init pushes itself to main conf
* main conf is obtained using ngx_http_conf_get_module_main_conf
* initiates ngx_http_subrequest

### connect
* ngx_http_upstream_connect called by
* ngx_http_upstream_init_request
* ngx_http_upstream_resolve_handler
* ngx_http_upstream_next

### ngx_http_upstream_process_header
ngx_http_upstream_send_response

### create http request from tcp module
ngx_http_create_request input is ngx_connection_t *c
But it expects c->data as ngx_http_connection_t
One possibility is to call ngx_http_init_connection first


## Log 
<pre>
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

```
typedef enum {
    NGX_HTTP_INITING_REQUEST_STATE = 0,
    NGX_HTTP_READING_REQUEST_STATE,
    NGX_HTTP_PROCESS_REQUEST_STATE,

    NGX_HTTP_CONNECT_UPSTREAM_STATE,
    NGX_HTTP_WRITING_UPSTREAM_STATE,
    NGX_HTTP_READING_UPSTREAM_STATE,

    NGX_HTTP_WRITING_REQUEST_STATE,
    NGX_HTTP_LINGERING_CLOSE_STATE,
    NGX_HTTP_KEEPALIVE_STATE
} ngx_http_state_e;

```
