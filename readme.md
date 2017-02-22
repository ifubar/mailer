# Contact form howto

```composer create-project laravel/laravel mailer "5.2.27"```

## register any email account with smtp support
ie I use ngs.ru

pass params to .env

```
MAIL_DRIVER=smtp
MAIL_HOST=smtp.ngs.ru
MAIL_PORT=465
MAIL_USERNAME=oppamailertest@ngs.ru
MAIL_PASSWORD=uahahahaha
MAIL_ENCRYPTION=ssl
```

adjust mailer/config/mail.php
```
    'from' => [
        'address' => env('MAIL_USERNAME', null),
        'name' => 'mailer'
    ],
    
    'admins' => [
        'contactstestadmin@mailforspam.com'
    ],
```

create contact form(contact.blade.php)
mailer/resources/views/contact.blade.php
I commented include views like layouts.headerSecondary, coz you have not provided it.

mailer/app/Http/Kernel.php
remove/comment VerifyCsrfToken middleware, coz your contact form doesnt use csrf tokens
http://prntscr.com/ebupfw

add routes
mailer/app/Http/routes.php
```
Route::get('/', function () {
    return view('contact');
});
Route::post('/contact', ['uses' => 'MailController@send']);
```

```php artisan make:controller MailController```

MailController: add method send
make email template (mailer/resources/views/email.blade.php)

```php artisan serve```

that is

















