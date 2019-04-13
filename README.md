> lua **go**es web

# doc

    make LUA_PATH="./?.lua;/usr/share/luagoesweb/?.lua"
    ./luagoesweb ./example.lua [...]

## bindings

### http

start serving requests

    local http = require("http")

    -- the 3rd argument is either nil or a path to a directory containing static files
    http.serve("127.0.0.1:5558", {
      { method = "GET", context = "/", callback = func(w, r) w.write("hello world") end }
      { method = "POST", context = "/", callback = func(w, r) w.write("hello post world") end }
    }, nil)

define callback functions for http requests

    function example(w, r)
      -- r is the request
      useragent = r.getHeader("User-Agent")

      -- w is the response writer
      w.addHeader("X-Header-Foo", "example")
      w.setStatus(200)
      w.write("this is the response body")
    end

### json

    local json = require("json")

    foo = json.decode('{"hello":"world"}')
    print(foo.hello)
    foo.bla = 3
    json.encode(foo)