# smsIntegration
A laravel app with SMS Integration 



Create Laravel Project

If you haven’t installed the Laravel application yet, then head over to console screen, use the composer command with a create-project flag to create the brand new laravel app:

composer create-project --prefer-dist laravel/laravel cyber

Bash

Right after the installation process is over, get inside the project’s root:
Setting Up Vonage (Nexmo) SMS Package

Vonage (formerly known as Nexmo) is the notable communication service provider, Laravel works smoothly with Vonage and makes the SMS sending to phone process smooth. Thereupon, we need to register a new account with Vonage and get the proper API access.

Creating a Voyage account is relatively simple, you need to fill in your name and email; once you complete the account creating process right after that, you can access the SMS API dashboard.

Initially, It will credit some balance in your account that you can use to send SMS to your phone, you also have to choose the programming language on which you are developing the sms sending app.

Also, install the nexmo client using the composer command:

composer require nexmo/client

SQL

To establish the consensus between the laravel app and Vonyage client, you need to have the Nexmo key and secret. Hence, click on the Getting started link from the left sidebar. And, copy both key and secret from the Vonyage API dashboard.

Laravel 8 Send SMS Notification to Mobile
Generate and Configure Controller

Now, generate a new controller using the compoer command:

php artisan make:controller NotificationController

Bash

Execution of the previous command generated a controller, hence open and add the provided code in app/Http/Controllers/NotificationController.php file:

<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class NotificationController extends Controller
{
    public function sendSmsNotificaition()
    {
        $basic  = new \Nexmo\Client\Credentials\Basic('Nexmo key', 'Nexmo secret');
        $client = new \Nexmo\Client($basic);
 
        $message = $client->message()->send([
            'to' => '9197171****',
            'from' => 'John Doe',
            'text' => 'A simple hello message sent from Vonage SMS API'
        ]);
 
        dd('SMS message has been delivered.');
    }
}

PHP

The $basic property holds the nexmo app key and secret so add both the credentials here to send the sms to mobile phone.
Set up Route

To make the GET request for sending an SMS message to mobile, make a new route. Import controller and create a route with route get method in resources/web.php file:

<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\NotificationController;

Route::get('send-sms-notification', [NotificationController::class, 'sendSmsNotificaition']);

PHP
Run Laravel App

You need to start the laravel application. So, invoke the PHP artisan serve command from the console, it lets you evoke the PHP development server, and you can test the feature you have just created:

php artisan serve

Bash

The app can be started similarly tested on:

http://127.0.0.1:8000/send-sms-notification

