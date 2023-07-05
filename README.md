Step 1: Create a new Laravel project
    composer create-project --prefer-dist laravel/laravel your-project-name

Step 2: Install and configure the LaravelLocalization package
Install the package
    composer require mcamara/laravel-localization
Publish the package
    php artisan vendor:publish --provider="Mcamara\LaravelLocalization\LaravelLocalizationServiceProvider"

Step 3: Configure the supported locales
For example, to enable German ('de') and English ('en'), modify the supportedLocales array as follows:
    'supportedLocales' => [
        'de' => ['name' => 'German', 'script' => 'Latn', 'native' => 'Deutsch', 'regional' => 'de_DE'],
        'en' => ['name' => 'English', 'script' => 'Latn', 'native' => 'English', 'regional' => 'en_GB'],
    ],

Step 4: Set up language files and translations
Inside each locale directory, create a messages.php file that contains the translation messages for that locale. For example, create resources/lang/de/messages.php for German translations and resources/lang/en/messages.php for English translations.
for each locale in resources/lang/{locale}/ directory. For instance, you can add "welcome"
    // resources/lang/de/messages.php
    return [
        'welcome' => 'Willkommen',
        'hello' => 'Hallo',
    ];

    // resources/lang/en/messages.php
    return [
        'welcome' => 'Welcome',
        'hello' => 'Hello',
    ];

Step 5: Define routes with language prefix
    Route::group(['prefix' => LaravelLocalization::setLocale()], function () {
        Route::get('/', function () {
            return view('welcome');
        });
    });

Step 6: Use language switcher in your views
    <ul class="navbar-nav ml-auto">
        <li class="nav-item">
            @if(LaravelLocalization::getCurrentLocale() == 'de')
                <a class="nav-link nav-link-icon" href="{{ LaravelLocalization::getLocalizedURL('en') }}" data-toggle="tooltip" title="Translate to English">
                    <img src="{{ asset('argon/img/icons/flags/GB.png') }}" alt="">
                </a>
            @else
                <a class="nav-link nav-link-icon" href="{{ LaravelLocalization::getLocalizedURL('de') }}" data-toggle="tooltip" title="Translate to German">
                    <img src="{{ asset('argon/img/icons/flags/DE.png') }}" alt="">
                </a>
            @endif
        </li>
    </ul>

    or

    <div class="language-switcher">
    @foreach(LaravelLocalization::getSupportedLocales() as $localeCode => $properties)
        <a href="{{ LaravelLocalization::getLocalizedURL($localeCode) }}" class="{{ app()->getLocale() === $localeCode ? 'active' : '' }}">
            {{ $properties['native'] }}
        </a>
    @endforeach
    </div>

Step: 7

    <h1>{{ __('messages.welcome') }}</h1>


Step: 8
    Test

