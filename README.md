# Pagination

Pagination is class that splits the data to segments and browse between these segments. Before usage SQL pagination, need to setup DB connection (AlexKratky\db::connect()).

### Installation

`composer require alexkratky/paginationx`

### The basic usage:

```php
require 'vendor/autoload.php';
use AlexKratky\Pagination;

//example data
$data = array(0,1,2,3,4,5,6,7,8,9);
//enter data and how many elements are on page (3). By default 10.
$pagination = new Pagination($data, 3);
$d = $pagination->getData(); // [0,1,2]
$pagination->currentPage(); // 1
$pagination->totalPages(); // 4 (floor(10/3)+1)
$pagination->previousPage(); // false; because the first page is the lowest one
$pagination->nextPage(); // 2
```
The current page is set by AlexKratky\Route::getValue("{PAGE}"); so just use in your routes {PAGE} parameter. Or it could be done by get parameter ?page= ($_GET["page"]).

## InfinityScrolling
The InfinityScrolling is script, that will automatically load next page using AJAX when the user hits the bottom of page. Everything you need to do is calling this static method Pagination::infinityScroll() inside the DOM element, where the data will be loaded. Also, for this you need route CURRENT_URI_WHERE_IS_INFINITY_SCROLL_USED/load/{PAGE} which will serve the data.