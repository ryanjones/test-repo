require 'capistrano-deploy'
use_recipes :git, :bundle, :rails, :unicorn, :rails_assets

server '50.116.2.69', :web, :app, :db, :primary => true
set :user, 'deploy'
set :deploy_to, '/home/deploy/yourapplication/current'
set :repository, 'git@github.com:RyanonRails/test-repo.git'

ssh_options[:forward_agent] = true

after 'deploy:update', 'bundle:install'
after 'deploy:update', 'deploy:assets:precompile'
after 'deploy:restart', 'unicorn:reload'


namespace :deploy do
  desc "Set up the unicorns"
  task :unicorn_power, :roles => :db do
    run "mkdir #{deploy_to}/tmp/pids/"
    run "mkdir #{deploy_to}/tmp/sockets/"
    run "cd #{deploy_to} && bundle exec unicorn -c #{deploy_to}/config/unicorn.rb -E production -D"
  end
end