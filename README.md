# Laravel API Template

<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

## Tips

1. Creating new Laravel Project

   ```sh

   composer create-project laravel/laravel <name of project>

   ```

2. Serving app

   ```sh

   php artisan serve

   ```
3. Creating Model

   ```sh

   php artisan make:model <name of model> --migration

   php artisan migrate

   ```
4. Creating Controller

   ```sh

   php artisan make:controller <name of controller> --api

                        OR

    php artisan make:controller <name of controller>

   ```

4. Authentication

   ```sh

   composer require laravel/sanctum

   php artisan vendor:publish --provider="Laravel\Sanctum\SanctumServiceProvider"

   php artisan migrate

   ```
   In app/Http/Kernel.php replace api key with:

   ```sh

   'api' => [
    \Laravel\Sanctum\Http\Middleware\EnsureFrontendRequestsAreStateful::class,
    'throttle:api',
    \Illuminate\Routing\Middleware\SubstituteBindings::class,
    ],

    ```
    In User Model:
    ```sh

    use Laravel\Sanctum\HasApiTokens;

    class User extends Authenticatable
    {
        use HasApiTokens, HasFactory, Notifiable;
    }

    ```

    Protected routes example:
    ```sh
    //Protected routes
    Route::group(['middleware' => ['auth:sanctum']], function () {
        Route::post('/logout', [AuthController::class, 'logout']);
        Route::post('/products', [productsController::class, 'store']);
        Route::put('/products/{id}', [productsController::class, 'update']);
        Route::delete('/products/{id}', [productsController::class, 'destroy']);
    });
    ```