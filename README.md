# tradescape.cash

Prepare website
---------------

Docker was used to host this website. You may use your own preferred method.

1. Install Docker: https://docs.docker.com/engine/install/
2. Follow "Configuration" & "SSL/HTTPS" Apache Docker image instructions here: https://hub.docker.com/_/httpd/

Docker requires preparation of the following files before proceeding further:

`httpd.conf` - Required for SSL setup only (docker only).<br>
`server.crt` - Required public key. Use your own preferred certificate signing method<br>
`server.key` - Required private key. Use your own preferred certificate signing method<br>

Running website - Linux
-----------------------

1. Download source code into a preferred local directory.
2. Place updated `httpd.conf` file in: `/usr/local/apache2/conf/`
3. Place certificate files in: `/usr/local/apache2/conf/`
4. Run website with one command:<br>
`docker run -dit --name tradescape.cash -p 80:80 -p 443:443 -v "$PWD":/usr/local/apache2/htdocs/ -v /usr/local/apache2/conf/httpd.conf:/usr/local/apache2/conf/httpd.conf -v /usr/local/apache2/conf/server.crt:/usr/local/apache2/conf/server.crt -v /usr/local/apache2/conf/server.key:/usr/local/apache2/conf/server.key httpd:2.4`

NOTE: When performing website source code updates and the source is updated on the host `$PWD`, the docker container volume bind mount will cause the container to automatically update the website content, no other action is required.

Docker image can run on any OS. Update your local path to reflect your local directory for source, httpd.conf file and certificate locations.

Example for Windows:
--------------------

`X:\where-your-source-is-located\` instead of `$PWD`<br>
`X:\path-to-httpd.conf-and-certs\conf\` instead of `/usr/local/apache2/conf/`

Other commands:
---------------

Stop website container<br>
`docker stop tradescape.cash`

Start website container again, existing container<br>
`docker start tradescape.cash`

Remove docker container, source code on host is untouched. Must stop before removing.<br>
`docker rm tradescape.cash`
