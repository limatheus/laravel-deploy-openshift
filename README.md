# How to deploy a Laravel application on Openshift plataform

### 1. clone this repository in a separated folder

```shell
git clone https://github.com/limatheus/laravel-deploy-openshift.git
```

### 2. Copy the .openshift folder to your existing application folder

```shell
cp -Rap .openshift /path/to/your/existing/application
```

### 3. Modify your `config/database.php` file changing the `connection` parameters to:

```php
// database.php  config file
// file START ommited
    'connections' => [

        'sqlite' => [
            'driver'   => 'sqlite',
            'database' => database_path('database.sqlite'),
            'prefix'   => '',
        ],

        'mysql' => [
            'driver'    => 'mysql',
            'host'      => env('DB_HOST', env('OPENSHIFT_MYSQL_DB_HOST', 'localhost')),
            'port'      => env('DB_PORT', env('OPENSHIFT_MYSQL_DB_PORT', 3306)),
            'database'  => env('DB_DATABASE', env('OPENSHIFT_APP_NAME', 'forge')),
            'username'  => env('DB_USERNAME', env('OPENSHIFT_MYSQL_DB_USERNAME', 'forge')),
            'password'  => env('DB_PASSWORD', env('OPENSHIFT_MYSQL_DB_PASSWORD', '')),
            'charset'   => 'utf8',
            'collation' => 'utf8_unicode_ci',
            'prefix'    => '',
            'strict'    => false,
        ],
        
        'pgsql' => [
            'driver'   => 'pgsql',
            'host'     => env('DB_HOST', env('OPENSHIFT_POSTGRESQL_DB_HOST', 'localhost')),
            'port'     => env('DB_PORT', env('OPENSHIFT_POSTGRESQL_DB_PORT', 5432)),
            'database' => env('DB_DATABASE', env('OPENSHIFT_APP_NAME', 'forge')),
            'username' => env('DB_USERNAME', env('OPENSHIFT_POSTGRESQL_DB_USERNAME', 'forge')),
            'password' => env('DB_PASSWORD', env('OPENSHIFT_POSTGRESQL_DB_PASSWORD', '')),
            'charset'  => 'utf8',
            'prefix'   => '',
            'schema'   => 'public',
        ]
    ],
// file END ommited
```

### 4. Add remote origin to your existing git config
