jsonrpC
=======

jsonrpC is an implementation of [JSON RPC 2.0](http://www.jsonrpc.org/specification) protocol in C.
* Simple API
* Portable
 * The implementation is ANSI C.
 * JSON library can be easily ported. (e.g. [yajl](http://lloyd.github.com/yajl), [jansson](http://www.digip.org/jansson/))
 * Transport independent. You can use this library with UDS, WebSocket, ...
* Tiny

jsonrpC is licensed under the [MIT License](http://www.opensource.org/licenses/mit-license.php)

##Example
####Register Method
```C
jsonrpc_server_t * init_jsonrpc(void)
{
  jsonrpc_server_t *server;
	jsonrpc_error_t   error;
	
	server = jsonrpc_server_open(jsonrpc_plugin_yajl());
	
	error  = jsonrpc_server_register_method(server, JSONRPC_TRUE, subtract, "subtract", "minuend:i, subtrahend:i");
	error  = jsonrpc_server_register_method(server, JSONRPC_TRUE, sum, "sum", "iii");
  // add more method here
  return server;
}
```
####Execute request
```C
void execute_jsonrpc(jsonrpc_server_t *server)
{
  const char       *req, *res;
	
	req = "{\"jsonrpc\": \"2.0\", \"method\": \"subtract\", \"params\": {\"subtrahend\": 23, \"minuend\": 42}, \"id\": 3}";
	res = jsonrpc_server_execute(server, req);
	// use 'res'
}
```
####Example code (screenshot)
run server
```shell
$make
$./jsonrpc
```
open test_websocket.html (with WebSocket supported browser)
![screenshot](http://farm9.staticflickr.com/8454/8062570242_1aea4d2602.jpg)