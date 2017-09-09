# S5
Super Simple Server Side Security

## Setup
1. Download **S5.php** and place it somewhere in your application.
2. Edit the header and replace the database login information with your own.
3. Create a file (I called mine createdatabase.php) in the same folder as S5.php
4. Paste the following in the file you created
``` php
<?php
  require 'S5.php';
  $security = new S5();
  $security->prepare_database();
?>
```
## Usage
``` php
$security = new S5();
```
## Documentation
#### User Authentication
``` php
$security->register('username', 'password'); // -> true/false (Success)
$security->login('username', 'password'); // -> true/false (Credentials correct/incorrect)
```
#### Managing Users
``` php
$security->set_user_active('username'); // -> true/false (Sucess/Failure)
$security->set_user_inactive('username'); // -> true/false (Success/Failure)

$security->verify_account_active('username'); // -> true/false (Account active/inactive)
```

#### Creating API Credentials
1. Create a blank php file in the same folder a S5.php and paste in the following
``` php
<?php
  require 'S5.php';
  
  $security = new S5();
  
  $credentials = $security->create_api_credentials();
  
  echo "API Key: " . $credentials['key'];
  echo "<br>";
  echo "API Secret: " . $credentials['secret'];
?>
```
2. View that page in a browser (for example: visit `http://yourserver.com/(file name).php`). It will display your credentials onscreen.
3. **Delete the file** to prevent anyone from creating their own api credentials

#### Validating API Requests
1. Client calls `https://yourserver.com/api.php?api_key=(API KEY)&api_secret=(API SECRET)&user=(Username from S5)&token=(User's token)`
2. at the top of api.php (or whatever you call it) add 
```php
if(!$security->verify_get_api_request()) {
  die("Request invalid");
}

// ... the rest of your code
```
