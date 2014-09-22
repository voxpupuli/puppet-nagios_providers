source ENV['GEM_SOURCE'] || "https://rubygems.org"

def location_for(place, fake_version = nil)
  if place =~ /^(git[:@][^#]*)#(.*)/
    [fake_version, { :git => $1, :branch => $2, :require => false }].compact
  elsif place =~ /^file:\/\/(.*)/
    ['>= 0', { :path => File.expand_path($1), :require => false }]
  else
    [place, { :require => false }]
  end
end

# C Ruby (MRI) or Rubinius, but NOT Windows
platforms :ruby do
  gem 'pry', :group => :development
end

gem "puppet", *location_for(ENV['PUPPET_LOCATION'] || ['> 3.7', '< 5'])
gem "facter", *location_for(ENV['FACTER_LOCATION'] || ['> 1.6', '< 3'])
gem "hiera", *location_for(ENV['HIERA_LOCATION'] || '~> 1.0')
gem "rake", "10.1.1", :require => false

group(:development, :test) do
  gem "rspec", "~> 2.14.0", :require => false

  # Mocha is not compatible across minor version changes; because of this only
  # versions matching ~> 0.10.5 are supported. All other versions are unsupported
  # and can be expected to fail.
  gem "mocha", "~> 0.10.5", :require => false
end

if File.exists? "#{__FILE__}.local"
  eval(File.read("#{__FILE__}.local"), binding)
end

# vim:filetype=ruby
