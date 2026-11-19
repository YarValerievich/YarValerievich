<a href="https://git.io/typing-svg">
  <img src="https://readme-typing-svg.herokuapp.com?font=Fira+Code&size=32&duration=2000&pause=1000&color=1FBFF6&center=true&vCenter=true&width=800&lines=Embedded+Software+Engineer;Python+%7C+C%2FC%2B%2B+%7C+Hardware" alt="Typing SVG" />
</a>

✦ ✦ ✦

## Ambilight WLED (Embedded)

Разработал аппаратно-программный комплекс для динамической подсветки 85" ТВ. Главная инженерная задача заключалась в построении стабильного end-to-end пайплайна: от захвата видео с камеры до управления 340 зонами WS2812B через ESP32 с задержкой менее 50 мс.

В процессе разработки столкнулся с рядом нетривиальных проблем, которые потребовали доработки архитектуры:

* **Блокировки сетевого ввода-вывода.** Изначально при потере связи с ESP32 mDNS-резолвинг (`wled-tv.local`) блокировал основной поток на 5 секунд на каждом кадре. Переписал транспортный слой: перевел UDP-сокеты в неблокирующий режим и добавил принудительное разрешение IP-адреса только при инициализации. Это обеспечило честную drop-policy без фризов конвейера.
* **Аппаратные артефакты на линии данных.** На тестовых стендах наблюдались сбои цветов и "мертвые" первые пиксели из-за несовпадения логики 3.3В (ESP32) и 5В (лента), а также наводок. Решил проблему внедрением согласователя уровней 74AHCT125 и токоограничивающего резистора 330 Ом непосредственно перед входом DI ленты.
* **Конфликты окружения на ARM64.** Столкнулся с бинарной несовместимостью C-расширений OpenCV и свежего NumPy 2.x на Raspberry Pi 5. Оптимизировал процесс деплоя, разделив тяжелые системные зависимости (установка через `apt`) и изолированные Python-библиотеки в `venv`, что полностью исключило ошибки `binary incompatibility`.
* **Деградация плавности при просадках FPS.** Стандартное сглаживание зависело от частоты кадров. Реализовал алгоритм Time-based EMA, где коэффициент сглаживания рассчитывается динамически на основе реального `dt` между кадрами, делая картинку математически инвариантной к лагам камеры.

**Стек:** Python 3.11, OpenCV, FastAPI, MQTT, WLED, Raspberry Pi 5, ESP32, systemd.

**[Исходный код и документация](https://github.com/YarValerievich/ambilight-wled)**

• • •

## Архив проектов (Data Analytics)

| Проект | Цель | Стек | Результат |
| :--- | :--- | :--- | :--- |
| **[Анализ эффективности бизнеса](https://nbviewer.org/github/YarValerievich/Project5_business_performance_analysis/blob/main/business_performance_analysis.ipynb)** | Выявить причины убытков, оптимизировать бюджет. | Python, Pandas, когортный анализ, юнит-экономика | Обосновано перераспределение бюджета: отказ от канала с CAC в 3 раза выше среднего. |
| **[Анализ рекламных источников + SQL](https://nbviewer.org/github/YarValerievich/Project4_advertising_sources_dashboard/blob/main/Project4_advertising_sources_dashboard.ipynb)** | Оценить поведение пользователей по источникам трафика. | Python, Pandas, SciPy, SQL, проверка гипотез | Даны рекомендации по перераспределению ресурсов на самые конверсионные каналы. |
| **[Исследование рынка общепита Москвы](https://nbviewer.org/github/YarValerievich/Project3_analysis_moscow_places/blob/main/Project3_analysis_moscow_places.ipynb)** | Найти локации с наименьшей конкуренцией для инвесторов. | Python, Pandas, Plotly, Folium, SciPy | Определены районы и ниши (булочные) с максимальным потенциалом и минимальной конкуренцией. |
| **[A/A/B-тестирование и воронка](https://nbviewer.org/github/YarValerievich/Project2_AAB-test_sales_funnel/blob/main/Project2_AAB-test_sales_funnel.ipynb)** | Оценить путь пользователя и найти узкие места воронки. | Python, Pandas, Plotly, SciPy, A/B-тесты | Выявлена критическая точка оттока (62%) на этапе перехода к экрану предложений. |
| **[Приоритизация гипотез и A/B тест](https://nbviewer.org/github/YarValerievich/Project1_AB-test_hypothesis/blob/main/Project1_AB-test_hypothesis.ipynb)** | Оценить результаты эксперимента интернет-магазина. | Python, Pandas, NumPy, SciPy, фреймворки ICE/RICE | Тест остановлен досрочно: зафиксирована победа группы B (рост конверсии на 15%). |

---

## Контакты

- **Telegram:** [@yar_valeriich](https://t.me/yar_valeriich)
- **Email:** [9lppa_0228@mail.ru](mailto:9lppa_0228@mail.ru)
- **Телефон:** +7 (932) 712-71-74
