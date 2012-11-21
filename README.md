## hiera_http : a HTTP back end for Hiera


### Description

This is a back end plugin for Hiera that allows lookup to be sourced from HTTP queries.  The intent is to make this backend adaptable to allow you to query any data stored in systems with a RESTful API such as CouchDB or even a custom store with a web front-end

### Configuration

The following is an example hiera.yaml configuration for use with hiera-http

    :backends:
      - http
     
    :http:
      :host: 127.0.0.1
      :port: 5984
      :output: json
      :failure: graceful
      :paths:
        - /configuration/%{fqdn}
        - /configuration/%{env}
        - /configuration/common


The following are optional configuration parameters

`:output: ` : Specify what handler to use for the output of the request.  Currently supported outputs are plain, which will just return the whole document, or YAML and JSON which parse the data and try to look up the key

`:http_connect_timeout: ` : Timeout in seconds for the HTTP connect (default 10)

`:http_read_timeout: ` : Timeout in seconds for waiting for a HTTP response (default 10)

`:failure: ` : When set to `graceful` will stop hiera-http from throwing an exception in the event of a connection error, timeout or invalid HTTP response and move on.  Without this option set hiera-http will throw an exception in such circumstances

The `:paths:` parameter can also parse the lookup key, eg:
    :paths:
      /configuraiton.php?lookup=%{key}

### TODO

Theres a few things still on my list that I'm going to be adding, including

* Add SSL support
* Add HTTP basic auth support
* Add proxy support
* Add further handlers (eg: XML)


### Author

* Craig Dunn <craig@craigdunn.org>
* @crayfishX
* IRC (freenode) crayfishx
* http://www.craigdunn.org



