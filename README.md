# README

### Development environment config
##### Postgres  
Setup DB username (and password)

> config>database.yml

    default: &default  
        username: postgres

### Development environment variables

##### Devise Secret Keys  
These secret keys are used for verifying the integrity of signed cookies used by Devise.  
Use `rails secret` to generate your own secure secret key.

> config>secrets.yml

    development:
      secret_key_base: <insert_secure_key_here>

    test:
      secret_key_base: <insert_secure_key_here>

    production:
      secret_key_base: <%= ENV["SECRET_KEY_BASE"] %>

##### Twillio
`TWILIO_SID:` Twilio Account SID  
`TWILIO_AUTH_TOKEN:` Twilio Auth Token  
`TWILIO_NUMBER:` Assigned Twilio Number  
Note: All phone numbers need to have country codes!

> config>local_env.yml

    TWILIO_SID: <insert_SID>
    TWILIO_AUTH_TOKEN: <insert_tuth_token>
    TWILIO_NUMBER: <insert_twilio_number>

> config>application.rb

Load local_env.yml into the ENV array.

    class Application < Rails::Application
      config.before_configuration do
        env_file = File.join(Rails.root, 'config', 'local_env.yml')
        YAML.load(File.open(env_file)).each do |key, value|
          ENV[key.to_s] = value
        end if File.exist?(env_file)
      end
    end
