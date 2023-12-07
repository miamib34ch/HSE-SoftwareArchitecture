# HSE-SoftwareArchitecture
Разработка системы для проведения интерактивных экскурсий по городам.

**Пользователи:** турфирмы/экскурсоводы и туристы. 

**Требования:**
1) Мобильный клиент для экскурсоводов:
   * составление маршрутов для туризма (экскурсовод ставит точки на карте, которые будут пройдены за маршрут),
   * загрузка материалов (текстовые, медиа) по достопримечательностям,
   * расставление материалов в дополненной реальности (необязательно идти на точку для расстановки),
   * формирование ссылок на маршруты для туристов
3) Мобильный клиент для туристов:
   * просмотр маршрутов (туристы открывают ссылку маршрута экскурсовода, и получают доступ к маршруту),
   * использование дополненной реальности для просмотра материалов во время маршрута (когда находишься на точке, которую добавил экскурсовод в маршруте)
4) Сервер:
   * связывает клиентов,
   * хранит и обрабатывает загруженные экскурсоводом материалы

**Дополнительный контекст:**
* Приложение поставляется турфирмам/экскурсоводам и предлагается туристам самими турфирмами/экскурсоводами, как дополнительное средство при прохождении маршрута от турфирмы/экскурсовода ("с приложением маршрут будет интереснее")
* Мобильные клиенты только для iOS, используются нативные API для разработки
