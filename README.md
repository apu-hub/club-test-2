
[![HTTP PHP Logo](https://i.ibb.co/mCh07ty/logo-01.png)](http://github.com/apu-hub/http-php/)

It's a simple HTTP request handling library, written in PHP.
build on top of PHP 7.4.12 .

## documentation:

- Routing
  - [Routes](#routes)
  - [Router](#router)
- Request
  - [Body](#body)
  - [Query](#query)
  - [Params](#params)
- Response
  - [Status](#status)
  - [Send](#send)
  - [json](#json)
  - [Render](#render)

## Routes

Depending on the request method currentlly available class functions are:

get, post, put, delete, route.

```php
// $app->get('/path', function());
$app->get('/', function (Request $request, Response $response) {
    $response->send('Hello World!');
});
```

```php
// $app->route('method', '/path', function());
$app->route('GET','/', function (Request $request, Response $response) {
    $response->send('Hello World!');
});
```

## Router

This function is usefull to create nested routes.

```php
// $app->router('/path', function() {
$app->get('/items', function ($uri) {

    $items = new HTTP_PHP();

    $items->get('/', function ($uri) {
        $items->send('Sending all items');
    });
});
```

## Body

```php
// body(); returns the body of the request as a array
// body('key'); returns the value of the key
$app->get('/', function (Request $request, Response $response) {
    $response->json($request->body());
});
```

## Query

```php
// request query string : ?key=value
// result : ["key" => "value"]

// query(); returns the query of the request as a array
// query('key'); returns the value of the key
$app->get('/', function (Request $request, Response $response) {
    $response->json($request->query());
});
```

## Params

```php
// request params : /1234
// result : ["key"=>"1234"]

// params(); returns the params of the request as a array
// params('key'); returns the value of the key
$app->get('/:key', function (Request $request, Response $response) {
    $response->json($request->params());
});
```

## Send

```php
$app->get('/', function (Request $request, Response $response) {
    $response->send('Hello World!');
});
```

## Json

```php
// jsson(); array as input
// json(); returns the body to client as json
$app->get('/', function (Request $request, Response $response) {
    $response->json(['key' => 'value']);
});
```

## Render

This function is usefull to render a view. [sample file](sample_file_location/) for view.

```php
$app->get('/page1', function (Request $request, Response $response) {

    $templates=["views/header.html",
                "views/page1.html",
                "views/footer.html"];

    $data = ["page_title" => "Page 1",
             "page_content" => "Content of page 1"];

    // render([templates_path_array], [data_array])
    $response->render($templates, $data);
});
```

# Contributing

This project is open-source, you can contribute to it by making a pull request or opening an issue.

## People

Author of HTTP PHP is [Chayan Sarkar](https://github.com/apu-hub/)

## License

[MIT](LICENSE)
