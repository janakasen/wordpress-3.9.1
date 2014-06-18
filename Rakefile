require 'rubygems'
require 'fileutils'
require 'erb'
require 'tempfile'
require 'json'
require 'securerandom'

task :install do
  dbhost = '127.0.0.1'
  app_config = {}

  # Read app user from METADATA
  metadata = JSON.parse(File.read("/opt/durga/meta.json"))
  dbuser = metadata['dbinfo']['dbuser']
  dbpassword = metadata['dbinfo']['dbpass']
  dbname = metadata['dbinfo']['dbname']
  system_fqdn = metadata['fqdn']
  app_config[:system_fqdn] = system_fqdn

  # Read app user from METADATA
  app_config[:username] = metadata['username']
  app_config[:firstname] = metadata['firstname']
  app_config[:lastname] = metadata['lastname']
  app_config[:title] = metadata['title']
  app_config[:displayname] = metadata['displayname']
  app_config[:title] = metadata['title']
  app_config[:clientname] = metadata['clientname']
  app_config[:streetaddress] = metadata['streetaddress']
  app_config[:state] = metadata['state']
  app_config[:city] = metadata['city']
  app_config[:zip] = metadata['zip']
  app_config[:country] = metadata['country']
  app_config[:phone] = metadata['phone']
  app_config[:fax] = metadata['fax']

  #Create documents directory
  FileUtils.chown_R "www-data", "www-data", "/var/www"

  new_config = ERB.new(File.read("/var/www/wp-config-sample.php")).result(binding)
  File.open("/var/www/wp-config.php", "w") do |f|
    f.write(new_config)
    f.flush
  end

  #TODO: move the rakefile to Top directory
  File.unlink("/var/www/Rakefile")

end
