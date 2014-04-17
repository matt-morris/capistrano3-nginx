# Capistrano::Nginx [![Gem Version](https://badge.fury.io/rb/capistrano3-nginx.png)](http://badge.fury.io/rb/capistrano3-nginx)

Nginx support for Capistrano 3.x

## Installation

Add this line to your application's Gemfile:

    gem 'capistrano3-nginx', '~> 2.0'
    gem 'capistrano'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install capistrano3-nginx

## Usage

Require in `Capfile` to use the default task:

```ruby
require 'capistrano/nginx'
```

You will get the following tasks

```ruby
cap nginx:start                    # Start nginx service
cap nginx:stop                     # Stop nginx service
cap nginx:reload                   # Reload nginx service
cap nginx:restart                  # Restart nginx service
cap nginx:site:add                 # Creates the site configuration and upload it to the available folder
cap nginx:site:disable             # Disables the site removing the symbolic link located in the enabled folder
cap nginx:site:enable              # Enables the site creating a symbolic link into the enabled folder
cap nginx:site:remove              # Removes the site removing the configuration file from the available folder
cap nginx:gzip_static              # Compress all js and css files in :nginx_static_dir with gzip
```

Configurable options (copy into deploy.rb), shown here with examples:

```ruby
# Server name for nginx
# No default vaue
set :nginx_domains, "foo.bar.com"

# nginx service script
# Defaults to using the 'service' convinience script.
# You might prefer using the init.d instead depending on sudo privilages.
# default value: "service nginx"
set :nginx_service_path, "/etc/init.d/nginx"

# Roles the deploy nginx site on,
# default value: :web
set :nginx_roles, :web

# Path, where nginx log file will be stored
# default value:  "#{shared_path}/log"
# set :nginx_log_path, "#{shared_path}/log"

# Path where nginx is installed
# default value: "/etc/nginx"
set :nginx_root_path, "/etc/nginx"

# Path where to look for static files
# default value: "public"
set :nginx_static_dir, "my_static_folder"

# Path where nginx available site are stored
# default value: "sites-available"
set :nginx_sites_available, "sites-available"

# Path where nginx available site are stored
# default value: "sites-enabled"
set :nginx_sites_enabled, "sites-enabled"

# Path to look for custom config template
# `:default` will use the bundled nginx template
# default value: :default
set :nginx_template, "#{stage_config_path}/#{fetch :stage}/nginx.conf.erb"

# Use SSL on port 443 to serve on https. Every request to por 80
# will be rewritten to 443
# default value: false
set :nginx_use_ssl, false

# Name of SSL certificate file
# default value: "#{application}.crt"
set :nginx_ssl_certificate, 'my-domain.crt'

# SSL certificate file path
# default value: "/etc/ssl/certs"
set :nginx_ssl_certificate_path, "#{shared_path}/ssl/certs"

# Name of SSL certificate private key
# default value: "#{application}.key"
set :nginx_ssl_certificate_key, 'my-domain.key'

# SSL certificate private key path
# default value: "/etc/ssl/private"
set :nginx_ssl_certificate_key_path, "#{shared_path}/ssl/private"

# Whether you want to server an application through a proxy pass
# default value: true
set :app_server, true

# Socket file that nginx will use as upstream to serve the application
# Note: Socket upstream has priority over host:port upstreams
# no default value
set :app_server_socket, "#{shared_path}/sockets/unicorn-#{fetch :application}.sock"

# The host that nginx will use as upstream to server the application
# default value: 127.0.0.1
set :app_server_host, "127.0.0.1"

# The port the application server is running on
# no default value
set :app_server_port, 8080
```

## Thanks
Thansk for the inspiration on several nginx recipes out there

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
