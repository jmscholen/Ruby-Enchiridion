![Devise Logo](https://raw.github.com/plataformatec/devise/master/devise.png)

By [Plataformatec](http://plataformatec.com.br/).

The gem is available at: https://github.com/plataformatec/devise

The devise gem is a user athentication framwork for Rails. It is fairly complex for a newbie to set up, so this doc will help with the initial installation so that you can understand what you are doing, rather than spending hours trying to read thru the docs and other peoples blogs on how to install this gem and have it working in minutes rather than hours. This is a very basic app with no frills except with it also sets up the Mailer option. The frills are up to you.

Steps to getting the basics app with user login/signup/confirmation
emails: 
` $rails new name_of_app $cd name_of_app` 

Add the following gems to your Gemfile: 
gem ‘devise’ 
gem ‘bcrypt’ 

` $bundle install`
` $rails g devise:install` 

In App: Add to the application\_controller.rb
` before_action :authenticate_user!` 

Add to config/environments/development.rb:
config.action\_mailer.default\_url\_options = { host: ‘localhost:3000’ }

Also add to same file the following(The following will work with gmail
after you edit the appropriate fields):
` config.action_mailer.delivery_method = :smtp config.action_mailer.smtp_settings = { address:'smtp.gmail.com', port: 587, domain: 'gmail.com', user_name: 'your_user_name', password: 'your_password', authentication: 'plain', enable_starttls_auto: true } config.action_mailer.perform_deliveries = true config.action_mailer.raise_delivery_errors = true config.action_mailer.default_options = {from: 'add_an_email_address'}`

Open and uncomment  the route in the config/routes.rb.
` root "welcome#index" ` \#\# need to run next command for this route to
work 
` $rails g controller Welcome index` 

Open and uncomment the following in initializer/devise.rb file 
-uncomment the `config.mailer = 'Devise::Mailer'` 
-uncomment the ` config.mailer_sender = 'add_your_from_email_address' `\#\#\#add your return email 

` $rails g controller Welcome index` 
Add this line to the welcome page
` <%= link_to "Log Out", destroy_user_session_path, method: "delete" %>`

` $rails g devise User ` \# User is the model that I want devise to
authenticate 

In App: In user.rb file, update the user model to use
`:confirmable` 

In migration file create when you ran devise:install, uncomment the migration file created to use confirmable, be sure to be uncomment the confirmable token at the bottom too
` $rails db:migrate`
` $rails g devise:views $rails s` 

You should have a working app at localhost:3000…..Test your application with a real email to test confirmation email.