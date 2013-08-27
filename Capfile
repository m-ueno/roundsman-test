load 'deploy'
require 'roundsman/capistrano'

set :application, "ep4p-roundsman"
set :user, "ubuntu"
set :cookbooks_directory, ["../chef-repo/site-cookbooks", "../chef-repo/cookbooks"]

default_run_options[:shell] = '/bin/bash'
default_run_options[:pty] = true

HTTP_PROXY='http://proxy.gw.nic.fujitsu.com:8080'
default_environment[:http_proxy]=HTTP_PROXY
default_environment[:https_proxy]=HTTP_PROXY
default_environment[:no_proxy]='192.168.0.242,localhost,127.0.0.1'

role :web, "192.168.0.18"

namespace :chef do
  set :care_about_ruby_version, false

  task :default do
    roundsman.run_list fetch(:run_list)
  end

  namespace :nginx do
    task :install do
      roundsman.run_list "recipe[nginx]"
    end
  end

  namespace :base do
    task :install do
      roundsman.run_list "recipe[base]"
    end
  end

end
