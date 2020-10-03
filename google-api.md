## Preparation
```
create console app(https://console.developers.google.com/).
get client id and client secret

rails g model GoogleToken access_token:string refresh_token:string expires_at:datetime uid:string

rails db:migrate
```
## gem file add this gem
```
gem 'google-api-client'
gem 'omniauth-google-oauth2'
```
## config/initalizers/omniauth.rb
```
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :google_oauth2, ENV['GOOGLE_CLIENT_ID'], ENV['GOOGLE_CLIENT_SECRET'], {
  scope: ["gmail.readonly", "userinfo.email"],
    access_type: 'offline'}
  # permission application require
end
```
## app/models/google_token.rb
```
require 'net/http'
require 'json'
require 'google/apis/gmail_v1'

class GoogleToken < ApplicationRecord
  def to_params
    {'refresh_token' => refresh_token,
    'client_id' => ENV['GOOGLE_CLIENT_ID'],
    'client_secret' => ENV['GOOGLE_CLIENT_SECRET'],
    'grant_type' => 'refresh_token'}
  end

  def request_token_from_google
    url = URI("https://accounts.google.com/o/oauth2/token")
    Net::HTTP.post_form(url, self.to_params)
  end

  def refresh
    response = request_token_from_google
    data = JSON.parse(response.body)
    update_attributes(
    access_token: data['access_token'],
    expires_at: Time.now + (data['expires_in'].to_i).seconds)
  end

  def expired?
    expires_at < Time.now
  end

  def fresh_token
    refresh if expired?
    access_token
  end
end
```
## routes.rb
```
Rails.application.routes.draw do
  resource :google_account, only: :show
  match "/auth/:provider/callback", to: "google_accounts#create", via: :get
end
```

## app/controllers/google_accounts_controller.rb
```
class GoogleAccountsController < ApplicationController
  def create
    auth = request.env['omniauth.auth']
    @google_token = Token.find_or_create_by(uid: auth['uid']) do |token|
      token.access_token = auth['credentials']['token']
      token.refresh_token = auth['credentials']['refresh_token']
      token.expires_at = Time.at(auth['credentials']['expires_at']).to_datetime
    end
  end
end
```
## app/views/google_accounts/show.html.erb
```
<%= link_to "Authenticate with Google!", '/auth/google_oauth2' %>
```
## app/views/google_accounts/create.html.erb
```
<%= @google_token.access_token %>
```

## work flow of google oauth2
```
  step 1: send authorization request(sessions/index.html.erb)
    - client init a request to Google's OAuth 2.0 endpoint is at https://accounts.google.com/o/oauth2/v2/auth
    with parameters(google_client_id, google_client_scret, scope, ..)
  step 2: User confirm grant permission in prompt
  step 3: Handle the OAuth 2.0 server response
    - After receive response, google response callback url(http://localhost:3000/auth/google_oauth2/callback) include an authorization code 
    - web server call the https://oauth2.googleapis.com/token endpoint and set authorization code parameter
    - google server return access_token.
    - application use this access_token to make calls to a Google API to get data(gmail in this example).
  ```
## add to app/models/google_token.rb
  ```
  def get_messages
    service = Google::Apis::GmailV1::GmailService.new
    self.refresh if expired?
    
    service.authorization = self.access_token
    emails = service.list_user_messages(self.uid)
    return if emails.messages.blank?
    
    emails.messages
  end
  ```