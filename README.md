# DICAS DE CMD

## criar um projeto
`laravel new nomedoprojeto`

`composer create-project --prefer-dist laravel/laravel blog "5.6.*"`

## rodar servidor direto
`php artisan serve`

## ver lista de rotas
`php artisan route:list`

## criar um controller (usar plural no nome da classe)
`php artisan make:controller PostsController`

## criar um controller com os métodos padrão
`php artisan make:controller --resource PostsController`

## migrations
`php artisan migrate`
`php artisan migrate:fresh`

## auth
`php artisan make:auth`

## criando seeder
`php artisan make:seeder ItemsTableSeeder`

`não esquecer de linkar o seeder filho com o databaseseeder`

## criando model
`php artisan make:model name`

`php artisan make:model name -c`

`php artisan make:model name -m`

## usando tinker
`php artisan tinker`

## assinalando todos os métodos para um resource controller
`Route::resource('posts','PostsController');`

    | GET|HEAD  | posts             | posts.index   | App\Http\Controllers\PostsController@index   | web |

    | POST      | posts             | posts.store   | App\Http\Controllers\PostsController@store   | web |

    | GET|HEAD  | posts/create      | posts.create  | App\Http\Controllers\PostsController@create  | web |

    | GET|HEAD  | posts/{post}      | posts.show    | App\Http\Controllers\PostsController@show    | web |

    | PUT|PATCH | posts/{post}      | posts.update  | App\Http\Controllers\PostsController@update  | web |

    | DELETE    | posts/{post}      | posts.destroy | App\Http\Controllers\PostsController@destroy | web |

    | GET|HEAD  | posts/{post}/edit | posts.edit    | App\Http\Controllers\PostsController@edit    | web |

# DICA DE ROUTES

## USE para CODE COMPLETION na ROUTE
`use Illuminate\Support\Facades\Route;`

## passando dados via get url amigavel
`Route::get('/post/{id}', 'PostsController@index');`

`public function index($id) {}`

## criando route para resource
`Route::resource('categories','CategoriesController');`

## Usando middleware group de auth
    Route::middleware(['admin'])->group(function (){
        Route::resource('admin/users', 'AdminUsersController',['as'=>'admin']);
        Route::resource('admin/posts', 'AdminPostsController',['as'=>'admin']);
        Route::resource('admin/categories','AdminCategoriesController',['as'=>'admin']);
        Route::resource('admin/comments','PostCommentsController',['as'=>'admin']);
        Route::resource('admin/comments/replies','CommentRepliesController',['as'=>'admin']);
    });

## adicionando prefixo no route name - usando AS
`Route::resource('admin/users', 'AdminUsersController',['as'=>'admin']);`

# DICAS DE PROBLEMAS

## como resolver o specifyed key too long
`no arquivo: app\Providers\AppServiceProvider.php`
`use Illuminate\Support\Facades\Schema;`
`Schema::defaultStringLength(191);`

# VIEWS HEAD
`@guest`
`@endguest`
`@auth`
`@endauth`

## importando css local da pasta public, usar no href:
`{{ asset('css/style.css') }}`

# VIEWS FORMS

## como chamar uma action
`{{ route('users.store') }}`

`{{route('users.update',[$user->id])}}`

## form data
`enctype="multipart/form-data"`

## form method
`@method('PUT')`

## form csrf
`@csrf`

# DICAS DE CONTROLLERS

## redirecionamentos
`$request->session()->flash('comment_message', 'Comment submited. Waiting moderation approval.');`

`// return redirect()->back();`

`return redirect()->to(url()->previous() . '#comment_message');`