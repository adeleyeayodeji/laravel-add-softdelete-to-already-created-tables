# laravel-add-softdelete-to-already-created-tables
Laravel add softdelete to already created tables
```php
php artisan make:migration AddDeletedAtToTables

```

```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class AddDeletedAtToTables extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        // Get all existing tables in the database
        $tables = Schema::getConnection()->getDoctrineSchemaManager()->listTableNames();

        foreach ($tables as $table) {
            // Check if the table doesn't have the `deleted_at` column
            if (!Schema::hasColumn($table, 'deleted_at')) {
                // Add the `deleted_at` column to the table
                Schema::table($table, function (Blueprint $table) {
                    $table->softDeletes();
                });
            }
        }
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::table('tables', function (Blueprint $table) {
            //
        });
    }
}


```

```php
php artisan migrate   

```
