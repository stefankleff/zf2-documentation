.. EN-Revision: none
.. _zend.service.flickr:

Zend\Service\Flickr
===================

.. _zend.service.flickr.introduction:

Введение
--------

*Zend\Service\Flickr* является простым API для использования веб-вервиса
Flickr. Чтобы использовать веб-вервисы Flickr, вы должны иметь ключ к
API. Для того, чтобы получить ключ и больше информации о сервисе
Flickr, обратитесь к `документации по API веб-вервиса Flickr`_.

В следующем примере мы используем метод *tagSearch()* для поиска
фотографий со словом "php" в тегах.

.. rubric:: Простой поиск фотографий в Flickr

.. code-block:: php
   :linenos:

   <?php
   require_once 'Zend/Service/Flickr.php';

   $flickr = new Zend\Service\Flickr('MY_API_KEY');

   $results = $flickr->tagSearch("php");

   foreach ($results as $result) {
       echo $result->title . '<br />';
   }

.. note::

   **Опциональный параметр**

   *tagSearch()* принимает массив опций как второй опциональный
   параметр.

.. _zend.service.flickr.finding-users:

Поиск фотографий и информации о пользователе Flickr
---------------------------------------------------

*Zend\Service\Flickr* предоставляет несколько способов получения
информации о пользователях Flickr:

- *userSearch()*: Принимает строку запроса, состоящую из разделенных
  пробелами тегов, массив опций поиска как опциональный второй
  параметр и возвращает набор фотографий в виде объекта
  *Zend\Service_Flickr\ResultSet*.

- *getIdByUsername()*: Возвращает ID пользователя, связанного с данным
  именем.

- *getIdByEmail()*: Возвращает ID пользователя, связанного с данным e-mail
  адресом.

.. rubric:: Поиск открытых фотографий пользователя по адресу e-mail

В этом примере мы, имея e-mail пользователя Flickr, ищем его открытые
фотографии, используя метод *userSearch()*:

.. code-block:: php
   :linenos:

   <?php
   require_once 'Zend/Service/Flickr.php';

   $flickr = new Zend\Service\Flickr('MY_API_KEY');

   $results = $flickr->userSearch($userEmail);

   foreach ($results as $result) {
       echo $result->title . '<br />';
   }

.. _zend.service.flickr.grouppoolgetphotos:

Поиск фотографий из пула группы
-------------------------------

*Zend\Service\Flickr* позволяет извлекать фотографии из пула группы
(group's pool), используя ID группы. Используйте метод *groupPoolGetPhotos()*:

.. _zend.service.flickr.grouppoolgetphotos.example-1:

.. rubric:: Извлечение фотографий из пула группы через ID группы

.. code-block:: php
   :linenos:

   <?php
       require_once 'Zend/Service/Flickr.php';

       $flickr = new Zend\Service\Flickr('MY_API_KEY');

       $results = $flickr->groupPoolGetPhotos($groupId);

       foreach ($results as $result) {
           echo $result->title . '<br />';
       }

.. note::

   **Опциональный параметр**

   *groupPoolGetPhotos()* принимает массив опций как опциональный второй
   параметр.

.. _zend.service.flickr.getimagedetails:

Извлечение данных по изображению в Flickr
-----------------------------------------

*Zend\Service\Flickr* делает быстрым и легким получение данных по
изображению через его ID. Просто используйте метод *getImageDetails()*,
как показано в следующем примере:

.. rubric:: Получение данных по изображению в Flickr

Имея ID изображения, легко извлечь информацию об этом
изображении:

.. code-block:: php
   :linenos:

   <?php
   require_once 'Zend/Service/Flickr.php';

   $flickr = new Zend\Service\Flickr('MY_API_KEY');

   $image = $flickr->getImageDetails($imageId);

   echo "Image ID $imageId is $image->width x $image->height pixels.<br />\n";
   echo "<a href=\"$image->clickUri\">Click for Image</a>\n";

.. _zend.service.flickr.classes:

Классы результатов Zend\Service\Flickr
--------------------------------------

Объекты следующих классов возвращаются методами *tagSearch()* и
*userSearch()*:

   - :ref:`Zend\Service_Flickr\ResultSet <zend.service.flickr.classes.resultset>`

   - :ref:`Zend\Service_Flickr\Result <zend.service.flickr.classes.result>`

   - :ref:`Zend\Service_Flickr\Image <zend.service.flickr.classes.image>`



.. _zend.service.flickr.classes.resultset:

Zend\Service_Flickr\ResultSet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Представляет набор результатов поиска, возвращенных Flickr

.. note::

   Реализует интерфейс *SeekableIterator* для легкой итерации (например,
   с использованием *foreach*) и прямого доступа с помощью метода
   *seek()*.

.. _zend.service.flickr.classes.resultset.properties:

Свойства класса
^^^^^^^^^^^^^^^

.. table:: Свойства класса Zend\Service_Flickr\ResultSet

   +---------------------+---+------------------------------------------------------+
   |Имя                  |Тип|Описание                                              |
   +=====================+===+======================================================+
   |totalResultsAvailable|int|Общее количество доступных результатов                |
   +---------------------+---+------------------------------------------------------+
   |totalResultsReturned |int|Общее количество возвращенных результатов             |
   +---------------------+---+------------------------------------------------------+
   |firstResultPosition  |int|Смещение для данного набора в общем наборе результатов|
   +---------------------+---+------------------------------------------------------+

.. _zend.service.flickr.classes.resultset.totalResults:

Zend\Service_Flickr\ResultSet::totalResults()
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

int:``totalResults()``


Возвращает общее количество результатов в наборе.

:ref:`Назад к списку классов <zend.service.flickr.classes>`

.. _zend.service.flickr.classes.result:

Zend\Service_Flickr\Result
^^^^^^^^^^^^^^^^^^^^^^^^^^

Отдельный результат запроса к Flickr.

.. _zend.service.flickr.classes.result.properties:

Свойства класса
^^^^^^^^^^^^^^^

.. table:: Свойства класса Zend\Service_Flickr\Result

   +----------+-------------------------+--------------------------------------------------------------------+
   |Имя       |Тип                      |Описание                                                            |
   +==========+=========================+====================================================================+
   |id        |string                   |ID изображения                                                      |
   +----------+-------------------------+--------------------------------------------------------------------+
   |owner     |string                   |NSID владельца фотографии                                           |
   +----------+-------------------------+--------------------------------------------------------------------+
   |secret    |string                   |Ключ, используемый при построении URL                               |
   +----------+-------------------------+--------------------------------------------------------------------+
   |server    |string                   |Имя сервера, используемое при построении URL                        |
   +----------+-------------------------+--------------------------------------------------------------------+
   |title     |string                   |Подпись к фотографии                                                |
   +----------+-------------------------+--------------------------------------------------------------------+
   |ispublic  |string                   |Является ли фотография общедоступной                                |
   +----------+-------------------------+--------------------------------------------------------------------+
   |isfriend  |string                   |Фотография доступна потому, что вы являетесь другом владельца.      |
   +----------+-------------------------+--------------------------------------------------------------------+
   |isfamily  |string                   |Фотография доступна потому, что вы являетесь членом семьи владельца.|
   +----------+-------------------------+--------------------------------------------------------------------+
   |license   |string                   |Лицензия, по которой доступна фотография                            |
   +----------+-------------------------+--------------------------------------------------------------------+
   |dateupload|string                   |Дата загрузки фотографии                                            |
   +----------+-------------------------+--------------------------------------------------------------------+
   |datetaken |string                   |Дата получения фотографии                                           |
   +----------+-------------------------+--------------------------------------------------------------------+
   |ownername |string                   |Ник пользователя                                                    |
   +----------+-------------------------+--------------------------------------------------------------------+
   |iconserver|string                   |Сервер, используемый в URL иконок                                   |
   +----------+-------------------------+--------------------------------------------------------------------+
   |Square    |Zend\Service_Flickr\Image|Уменьшенная копия изображения 75x75                                 |
   +----------+-------------------------+--------------------------------------------------------------------+
   |Thumbnail |Zend\Service_Flickr\Image|Уменьшенная копия изображения 100x100                               |
   +----------+-------------------------+--------------------------------------------------------------------+
   |Small     |Zend\Service_Flickr\Image|Уменьшенная копия изображения 240x240                               |
   +----------+-------------------------+--------------------------------------------------------------------+
   |Medium    |Zend\Service_Flickr\Image|Уменьшенная копия изображения 500x500                               |
   +----------+-------------------------+--------------------------------------------------------------------+
   |Large     |Zend\Service_Flickr\Image|Уменьшенная копия изображения 640x640                               |
   +----------+-------------------------+--------------------------------------------------------------------+
   |Original  |Zend\Service_Flickr\Image|Оригинал изображения                                                |
   +----------+-------------------------+--------------------------------------------------------------------+

:ref:`Назад к списку классов <zend.service.flickr.classes>`

.. _zend.service.flickr.classes.image:

Zend\Service_Flickr\Image
^^^^^^^^^^^^^^^^^^^^^^^^^

Представляет изображение, возвращенное в результате поиска.

.. _zend.service.flickr.classes.image.properties:

Свойства класса
^^^^^^^^^^^^^^^

.. table:: Свойства класса Zend\Service_Flickr\Image

   +--------+------+----------------------------------------+
   |Имя     |Тип   |Описание                                |
   +========+======+========================================+
   |uri     |string|URI для оригинального изображения       |
   +--------+------+----------------------------------------+
   |clickUri|string|Ссылка для изображения (страница Flickr)|
   +--------+------+----------------------------------------+
   |width   |int   |Ширина изображения                      |
   +--------+------+----------------------------------------+
   |height  |int   |Высота изображения                      |
   +--------+------+----------------------------------------+

:ref:`Назад к списку классов <zend.service.flickr.classes>`



.. _`документации по API веб-вервиса Flickr`: http://www.flickr.com/services/api/
