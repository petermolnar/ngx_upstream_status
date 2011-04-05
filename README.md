Nginx upstream status
=====================

This module provides a handler called upstream_status that can be used as follows:

    location /foo {
      upstream_status;
    }

It reports all the upstream blocks configured for this server. For upstreams managed using the round robin (default upstream), it lists all the servers configured in a block and indicates the current status (up/down)


Limitation
==========
nginx maintains the upstream status on a per worker basis. So this module shows the status of the upstream servers as seen by the worker that served the status page. In setups where there is just one worker, this is not a issue.

(Thanks to Maxim Dounin for pointing this out)
