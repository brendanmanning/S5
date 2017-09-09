# S5
Super Simple Server Side Security

## Setup
1. Download **S5.php** and place it somewhere in your application.
2. Edit the header and replace the database login information with your own.

## Usage
``` php
$security = new S5();
```
## Documentation
### User Authentication
``` php
$security->register('username', 'password'); // -> true/false (Success)
$security->login('username', 'password'); // -> true/false (Credentials correct/incorrect)
```
### Managing Users
``` php
$security->set_user_active('username'); // -> true/false (Sucess/Failure)
$security->set_user_inactive('username'); // -> true/false (Success/Failure)
```
### API Requests
Client calls ` https://yourserver.com/api.php?api_key=(API KEY)&api_secret=(API SECRET) `
