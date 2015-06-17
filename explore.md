# Эксплуатация системы электронной очереди #

Не смотря на то что систему QSystem можно применить в разных вариантах, основные моменты все же одинаковые во всех случаях. Первый момент это установка программного обеспечение. Второй - поддержание её в рабочем состоянии. Если второй момент не имеет каких-то особых свойств, то установка все же требует не большого пояснения.

## Инструкция по установке системы электронной очереди. ##

Шаг1. Приступая к установке.
Перед установкой системы, убедитесь, что у Вас установлена СУБД MySQL версии не ниже 5.1(5.5 рекомендуется) и JRE версии не ниже 1.7. Проверить установку JRE можно следующим способом:
Пуск->Выполнить->cmd-> java –version.
Также рекомендуется установить графические утилиты для работы с СУБД MySQL.

Шаг2. Запуск инсталляции системы.
Microsoft Windows:
Кликните два раза по файлу install.jar.
Linux(универсальный способ для любой ОС):
Запуск инсталляции с командной строки:
Перейдите в папку с файлом install.jar и выполните команду
> java –cp install.jar com.izforge.izpack.installer.Installer

Шаг3.  Инсталляция системы.
В окне приветствия жмем «Далее», в следующем окне представления системы так же жмем «Далее», в следующем окне будет показана версия сборки системы, дата сборки и другая информация о продукте, так же жмем «Далее».
> В следующем окне будет предложено выбрать каталог для установки системы, по умолчанию, каталогом является диск, с установленной ОС в папке Program Files и нажать «Далее». Инсталлятор автоматически создаст каталог, если его не существует.

Далее будет предложен выбор установки компонентов системы:

файлы приложения и библиотеки (по умолчанию, невозможно изменить).
рабочее место оператора (по умолчанию)
сервер
администрирование
пункт регистрации
документация в компонент «Документация» входят: руководство пользователя и руководство администратора, контекстная помощь присутствует всегда.
После выбора необходимых компонентов жмем «Далее».

Шаг4. Настройка системы.
После выбора компонентов, Вам будет предложено ввести адреса и порты для взаимодействия компонентов системы:

  * адрес сервера
  * порт сервера
  * адрес пункта регистрации
  * порт пункта регистрации
  * порт клиентов
  * назначить сервер суперсайтом.
Примечание! В случае заполнения неверных данных в адреса и порты серверов, их можно поправить в **.bat файлах, установленных компонентов системы.
После ввода данных, нажмите «Далее». Вам будет показан список выбранных компонентов, если Вас все устраивает, то жмите «Далее».**

Шаг5. Завершение установки.
Началась установка программных компонентов системы. После ее завершения жмем «Далее». Появится окно, где будет предложено вывести ярлыки на рабочий стол. Создание ярлыков в установленную папку с системой стоит по умолчанию.

Далее после завершения работы инсталяционного пакета необходимо установить некоторые программные продукты и драйвера, если, конечно, они у вас не установлены ранее.

Шаг6. Установка среды JMF выполнения мультимедиа для java.
Если у вас уже установлена среда выполнения JMF, то пропустите этот этап.
Для установки JMF запустите инcталятор jmf-2\_1\_1e-windows-i586.exe в OS Windows или jmf-2\_1\_1e-windows-i586.bin в OS Linux. Инсталятор можно найти в папке JMF в папке куда вы установили саму систему. При установке инсталятор копирует необходимые библиотреки в JRE. Если система безопастности не позволит инсталятору скопировать эти библиотеки автоматически, то нужно сделать это вручную. Файлы из папки C:\Program Files\JMF2.1.1e\lib скопируйте в папку < jre > \lib\ext.

Для установки клиентского модуля этих действий достаточно.

Теперь все необходимые компоненты установлены на ваш компьютер. Необходимо только развернуть БД и настроить ситему для использования этой БД.

Шаг7.Развертывание БД.
В папке DB вы найдете развертывающий скрипт qsystem.sql. Этот скрипт создаст саму базу, необходимые таблицы и заполнит таблицы начальными данными. Если у вас уже имеется БД и вы переходите на новую версию БД, то вам необходимо использовать sql-скрипт для обновления вашей базы до требуемой версии. Для выполнения sql-скриптов можно использовать консоль СУБД MYSQL, но лучше поспользоваться приложением MySQL Query Browser, её вы можете бесплатно скачать из Internet и установить на свой компьютер. Добавте пользователя СУБД и дайте ему доступ до созданной БД.
В настройках СУБД MySQL есть параметр wait\_timeout, это время в секундах, на протяжении которого сервер наблюдает неактивность в неинтерактивном соединения прежде, чем закрыть его. Значение по умолчанию 28800 секунд. Если сервер системы остается работать, к примеру, на ночь или продолжнительные праздники, то при начале работы произойдет ошибка, т.к. СУБД на обработает запрос. Этот параметр можно указать в конфигурационном файле MySQL. Часто в Windows это файл my.ini, точнее посмотреть в настройках сервера в приложении MySQL Administrator. Добавить в этот файл строчку "wait\_timeout=хххх". Сервер имеет функционал для поддержания соединения путем опроса СУБД раз в час. Учтите это если у вас более жесткие настройки.

Шаг 8. Настройка системы для использования БД.
В папке dist запустите admdbcom.bat для OS Windows или admdbcom.sh для OS Linux.   Убедитесь что при этом не запущено других приложений, которые входят в систему. Если во время старта admdbcom будет запущен сервер или программа администрирования, то измененные настройки не смогут быть сохранены. Введите правильные данные касательно соединения с БД и COM-портом(если требуется). Сохраните параметры.

Шаг 9. Заполнение конфигурации и настройка сервера.

Запустите StartAdmin.bat. Первоначально войдите в программу администрирования под пользователем "Администратор" с пустым паролем. Заполните список операторов, составьте дерево услуг, назначте услуги операторам. Позаботьтесь об расписании оказания услуг. Не забудьте сохранить изменения.

Шаг 10. Позиционирования главного и опрераторских табло.

В папке < Qsystem > \config\ есть 2 файлика: clientboard.xml и mainboard.xml (для клиенской машины и для сервера соответственно). В них и указываются координаты позиционирования табло, там-же его можно отключить\включить. Если второй монитор не подключен программа раскрывает всё на одном мониторе. Что-бы табло попадало на второй монитор, нужно указать в clientboard.xml и mainboard.xml координаты, которые находятся на втором мониторе. В настоечных файлах выставить параметры х и у:

<Board visible="1" x="-500" y="10" Наименование="Сохранить конфигурацию табло">
Наименование="Сохранить конфигурацию табло">
По ним будет определено расположение табло и развернуто на весь второй монитор. Когда подключается второй монитор, то нужно на него расширить рабочий стол. Это расширение рабочего стола будет иметь координаты относительно основного рабочего стола. В настройках нужно указать координаты точки попадающей на это расширение. По этой точке будет позиционирование. Т.е. табло будет помещено левым верхним углом в эту точку. Помним что координаты левого верхнего угла основного монитора (0,0). К примеру, подключен доп.монитор и рабочий стол расширен на него как бы слева от основного. Доп. монитор имеет расширение 640х480. Относительно главного рабочего стола левый верхний угол дополнительного рабочего стола имеет координаты (-640, 0). В настройках стоит x="-500" y="10", это значит табло позиционируется на доп.рабочий стол, но не в самый угол доп.монитора, а на 10 пикселов вниз и на 140 пикселов от края доп. монитора. И после этого развернется на весь экран.

После выполнения всех шагов система готова к использованию.

## Поддержание системы в работоспособном состоянии ##

Никаких особенных мероприятий во время эксплуатации QSystem не требуется. Ниже приведены несколько советов которые и так известны любому системному администратору.

  * Имейте запас термобумаги для принтера и регулярно проверяйте наличие бумаги в принтере на пункте регистрации.
  * Регулярно производите резервное копирование базу данных системы.
  * При обновлении системы всегда делайте резервную копию старой путем простого копирования, это позволит быстро вернуться к старой версии если обновление прошло не удачно.
  * Не злоупотребляйте кнопкой "рестарт" в программе администрирования.
  * Следите за логами системы. При обнаружении в них записей об ошибках, сообщайте разработчику по почте info@apertum.ru. Не забывайте прикладывать логи к письму.
  * Если Вам не хватает информации, то так же обращайтесь к разработчику за разъяснением.