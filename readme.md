# Contact form howto

```composer create-project laravel/laravel mailer "5.2.27"```

## register any email account with smtp support
ie I use ngs.ru

pass params to .env

```
MAIL_DRIVER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=465
MAIL_USERNAME=your-gmail-login@gmail.com
MAIL_PASSWORD=your-gmail-password
MAIL_ENCRYPTION=ssl
```

adjust mailer/config/mail.php
```
    'from' => [
        'address' => env('MAIL_USERNAME', null),
        'name' => 'mailer'
    ],
    
    'admins' => [
        'elliotr@gmail.com' // pass recievers email
    ],
```

create contact form(contact.blade.php)

https://github.com/ifubar/mailer/blob/master/resources/views/contact.blade.php

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

https://github.com/ifubar/mailer/blob/master/app/Http/Controllers/MailController.php

make email template (mailer/resources/views/email.blade.php)

https://github.com/ifubar/mailer/blob/master/resources/views/email.blade.php

```php artisan serve```

that is

















