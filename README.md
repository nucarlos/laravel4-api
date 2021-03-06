## API Response for Laravel 4

API is a useful to create response format and testing request.

### Installation

- [API on Packagist](https://packagist.org/packages/teepluss/api)
- [API on GitHub](https://github.com/teepluss/laravel4-api)

To get the lastest version of Theme simply require it in your `composer.json` file.

~~~
"teepluss/api": "dev-master"
~~~

You'll then need to run `composer install` to download it and have the autoloader updated.

Once Theme is installed you need to register the service provider with the application. Open up `app/config/app.php` and find the `providers` key.

~~~
'providers' => array(

    'Teepluss\Api\ApiServiceProvider'

)
~~~

API also ships with a facade which provides the static syntax for creating collections. You can register the facade in the `aliases` key of your `app/config/app.php` file.

~~~
'aliases' => array(

    'API' => 'Teepluss\Api\Facades\API'

)
~~~

Publish config using artisan CLI.

~~~
php artisan config:publish teepluss/api
~~~

## Usage

Create reponses format for RESTful.

~~~php
// Response entries.
$users = User::all();
API::createResponse($users);

// Response entry.
$user = User::find($id);
return API::createResponse($user);

// Response Laravel error.
$errors = $validation->messages()->all(':message');
return API::createResponse(compact('errors'), 400);

// Response created data.
$user = Url::create($data);
return API::createResponse($user, 201);

// Response 404.
API::createResponse("User [$id] was not found.", 404);

//Response deleted.
API::createResponse(null, 204);
~~~

Internal testing request.

~~~php
// GET Request.
API::get('user/1');

// POST Request.
API::post('user', array('title' => 'Demo'));

// PUT Request.
API::put('user/1', array('title' => 'Changed'));

// DELETE Request.
API::delete('user/1');

// You can make remote request without changing code also.
API::post('http://api.github.com', array('username' => 'teepluss'));
~~~
>> Remote request using [Guzzle](http://guzzlephp.org/) as an adapter.

## Support or Contact

If you have some problem, Contact teepluss@gmail.com

<a href='http://www.pledgie.com/campaigns/22201'><img alt='Click here to lend your support to: Donation and make a donation at www.pledgie.com !' src='http://www.pledgie.com/campaigns/22201.png?skin_name=chrome' border='0' /></a>
