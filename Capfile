require 'capistrano-deploy'
use_recipes :git, :bundle, :rails, :unicorn, :rails_assets

server '50.116.0.17', :web, :app, :db, :primary => true
set :user, 'deploy'
set :deploy_to, '/home/deploy/yourapplication/current'
set :repository, 'git@github.com:RyanonRails/test-repo.git'

ssh_options[:forward_agent] = true

after 'deploy:update', 'bundle:install'
after 'deploy:update', 'deploy:assets:precompile'
after 'deploy:restart', 'unicorn:reload'
