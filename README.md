Nginx upstream status
=====================

This module provides a handler called `upstream_status` that can be used as
follows:

    location /upstream_status {
      upstream_status;
    }

It reports all the upstream blocks configured for this server in JSON. For
upstreams managed using round robin (default upstream), it lists all the servers
configured in an upstream, and indicates the current status (up/down).


    {"application_pool":[{"server":"117.53.170.16:80","status":"up"},{"server":"117.53.170.17:80","status":"up"}],"another_pool":[]}


Installation
------------

You will need to re-compile Nginx from source to include this module.

    ./configure --add-module=/path/to/ngx_upstream_status
    make
    make install

Usage
-----

Add a new location block to your Nginx config

    location /status/upstreams {
      upstream_status;
      allow 127.0.0.1;
      deny *;
    }

Limitations
-----------
Nginx maintains the upstream status on a per worker basis. This module shows the
status of the upstream servers as seen by the worker that served the status page.
In setups where there is just one worker, this is not a issue.

(Thanks to Maxim Dounin for pointing this out)
