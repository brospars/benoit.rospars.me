---
layout: post
title: 'Nginx valid ssl configuration'
date: "2022-12-05 18:00:00 +0200"
author: benoit
version: 1.0.0
categories: snippets
comments: true
post_description: To create a valid SSL Nginx configuration with an intermediate certificate, you will need to obtain an SSL certificate and intermediate certificate from a CA, install the certificates on your server, and update your Nginx configuration to use them.
---

To create a valid SSL Nginx configuration, you will need to follow these steps:

1. Obtain an SSL certificate. You can either purchase one from a trusted certificate authority or generate a self-signed certificate. If you are generating a self-signed certificate, you can use the `openssl` tool to do so.

2. Once you have your SSL certificate, Install the SSL certificate and intermediate certificate on your server. The exact steps for doing this will vary depending on your server's operating system and web server software, but generally you will need to place the certificate files in a specific location and update your web server's configuration to use the certificates.

3. Once the certificates are installed on your server, you will need to update your Nginx configuration to use them. The default location for the Nginx configuration file is /etc/nginx/nginx.conf, but the exact location may vary depending on your setup.

4. Within the Nginx configuration file, you will need to add a `server` block that listens for HTTPS connections on port 443. The `server` block should look something like this:


```
server {
listen 443 ssl;
server_name example.com;

    ssl_certificate /path/to/your/certificate.crt;
    ssl_certificate_key /path/to/your/private.key;
}
```

5. The `ssl_certificate`, `ssl_certificate_key`, and `ssl_trusted_certificate` directives specify the paths to your SSL certificate, private key, and intermediate certificate, respectively. Be sure to update these paths with the correct paths to your own certificate and key files.

6. Once you have added the `server` block to your Nginx configuration file, save the file and restart Nginx to apply the changes. You can do this by running the following command:


```
sudo systemctl restart nginx
```

7. At this point, Nginx should be configured to use SSL for HTTPS connections. You can verify this by accessing your website using `https://` in the URL, and checking that the connection is secure (usually indicated by a lock icon in the browser address bar).

Note: This is a basic SSL configuration for Nginx. You may want to further secure your website by enabling additional SSL options, such as strong cipher suites and HTTPS redirects. Consult the Nginx documentation for more information on these options.