-В функции mysearch_permission, название и описание, завернуты в функцию t() для перевода.
-В function mysearch_menu() добавил аргумент для передачи  'page arguments' => array(1),
-В function mysearch_searchpage  аргумент который принимает значение ключа для поиска $searchterm.
-Переделан запрос в перекрестный, в котором поиск значений происходит по телу и заголовку в материалах в вид более правильный. 
$query = db_select('node', 'n');
    $query->innerJoin('field_data_body', 'b', 'b.entity_id = n.nid');
    $query->fields('n', array('nid', 'title'));

    $db_or = db_or();
    $db_or->condition('n.title', '%' . db_like($searchterm) . '%', 'LIKE');
    $db_or->condition('b.body_value', '%' . db_like($searchterm) . '%', 'LIKE');

    $query->condition($db_or);

-Создана форма mysearch_form для ввода значений ключа для поиска.
-Определена функция для опредения заголовка drupal_set_title. 
-Неприемлем вывод разметки в коде.
-Вывод материала с помощью фунции theme в виде списка значений.

