Users
=====

For the full XML representation of users, [check out the data reference](https://github.com/firstmoversadvantage/api.movingleads.com/blob/master/sections/data_reference.md#users).

<!-- 
                           new_user_session GET    /users/sign_in(.:format)          devise/sessions#new
                               user_session POST   /users/sign_in(.:format)          devise/sessions#create
                       destroy_user_session DELETE /users/sign_out(.:format)         devise/sessions#destroy
                              user_password POST   /users/password(.:format)         devise/passwords#create
                          new_user_password GET    /users/password/new(.:format)     devise/passwords#new
                         edit_user_password GET    /users/password/edit(.:format)    devise/passwords#edit
                                            PUT    /users/password(.:format)         devise/passwords#update
                   cancel_user_registration GET    /users/cancel(.:format)           registrations#cancel
                          user_registration POST   /users(.:format)                  registrations#create
                      new_user_registration GET    /users/sign_up(.:format)          registrations#new
                     edit_user_registration GET    /users/edit(.:format)             registrations#edit
                                            PUT    /users(.:format)                  registrations#update
                                            DELETE /users(.:format)                  registrations#destroy
                          user_confirmation POST   /users/confirmation(.:format)     devise/confirmations#create
                      new_user_confirmation GET    /users/confirmation/new(.:format) devise/confirmations#new
                                            GET    /users/confirmation(.:format)     devise/confirmations#show
                                user_unlock POST   /users/unlock(.:format)           devise/unlocks#create
                            new_user_unlock GET    /users/unlock/new(.:format)       devise/unlocks#new
                                            GET    /users/unlock(.:format)           devise/unlocks#show
 -->

Get myself
----------

* `GET /me.xml` returns information about the currently authenticated user.

This endpoint may be requested using a username and password, rather than the API token. This allows applications to obtain the token from those credentials, rather than requiring their users to enter an obscure API token by hand.

**Response:**

``` xml
<user>
  <id type="integer">1</id>
  <name>John Doe</name>
  <email-address>john.doe@example.com</email-address>
  <token>#{api_token}</token>
  <created-at type="datetime">2007-04-23T20:25:29Z</created-at>
  <updated-at type="datetime">2007-04-23T20:25:29Z</updated-at>
</user>
```


