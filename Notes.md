How is Chef different than puppet?
. Puppet CFEngine
. Chef is influenced by Puppet's design but is a rewrite from the grounf up.
. Chef scripts are written Ruby and not a DSL (.rb vs .pp) 

E.g. 
Install the 'tar pacgage

Puppet version:
`package { 'tar':
   ensure => '1.22-2ubuntu1'
}`

Chef version
package "tar" do
  version "1.2-2"
  action :install
end`

`ruby -c tar.rb
Syntax OK``

Similarly, Chef user ERb to modify configuration files: Here is an excerpt from my.cnf.erb:

`user            = mysql
pid-file        = <%= node['mysql']['pid_file'] %>
socket          = <%= node['mysql']['socket'] %>
port            = 3306
basedir         = /usr
datadir         = <%= node['mysql']['data_dir'] %>
tmpdir          = /tmp
`

= che's serialization format is JSON:
We can use chef-solo to add a recipe to a node by passing it a .json file

/etc/chef/dna.json :

`{
  "run_list": ["recipe[apache2]"]
}`

% sudo chef-solo -j /etc/chef/dna.json

Resources can have default attributes and/or default actions.