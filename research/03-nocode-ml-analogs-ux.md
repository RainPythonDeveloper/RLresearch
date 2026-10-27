# 03. Аналоги no-code ML/AI платформ, уроки успехов и провалов, UX

> Автор: агент «Аналитик no-code продуктов и UX» · Дата: 2026-10-27 · Прочитанные файлы research/: README.md (других файлов в папке на момент записи не было — кросс-ссылки на 01, 02, 04–08 даны «вперёд» по плану README и не проверены по содержимому)

**Оговорка об объёме поиска.** Лимит веб-поиска сессии исчерпался после ~29 запросов. Не покрыты (или покрыты только общими знаниями без ссылок, и помечены как таковые): Vertex AI AutoML, H2O, Clarifai, Vention MachineMotion, Universal Robots PolyScope/URCaps, судьба Lobe после 2020, текущий статус Akkio, детальный пост-мортем Project Bonsai. Многие цифры по стартапам взяты из агрегаторов (Sacra, valueaddvc, clay и т.п.) — это вторичные источники, уверенность везде «средняя» или «низкая», если не сказано иное.

---

## 1. Краткое резюме

1. **Узкий no-code ML-инструмент как самостоятельный бизнес выживает редко.** Успехи (Roboflow, Edge Impulse) — это платформы с активным open-source/dev-сообществом и привязкой к конкретной вертикали (CV, edge); из no-code RL-прецедентов массово не выжил ни один: Bonsai закрыт Microsoft (2023), Pathmind, по данным агрегаторов, остановлен (2021), AWS DeepRacer свёрнут как консольный сервис (декабрь 2025), RoboMaker закрыт (сентябрь 2025). Composabl — единственный живой, но малый (seed $4.25M).
2. **Парадигма «no-code» в 2026 году сместилась с drag-and-drop на «чат с агентом, который пишет код»** (Lovable, Replit, Bolt, Cursor): десятки и сотни миллионов ARR за считанные месяцы. Это самое сильное рыночное свидетельство того, каким должен быть интерфейс — но у этих продуктов плохая маржа и неизвестный churn.
3. **Для RL ключевая UX-проблема — не сам запуск обучения, а постановка цели (reward) и диагностика, почему не учится.** Эксперты тоже плохо делают reward вручную; LLM-генерация reward (Eureka) — перспективный путь, подходящий для чат-интерфейса.
4. **Обучение демонстрацией у не-экспертов работает хуже, чем кажется** (HCI-исследования: люди дают плохие демонстрации), поэтому нужны подсказки, оценка качества демонстраций и гибрид «демо + визуальные правки».
5. **Рекомендация (вывод):** чат-агент как основной интерфейс + шаблоны задач + прозрачные визуальные артефакты (видео роллаутов, кривые, сравнение политик) + «escape hatch» в код. Time-to-first-wow — ≤10 минут, на готовом шаблоне в браузерной симуляции.

---

## 2. Часть A. Кейсы no-code / low-code ML платформ

### 2.1 Сводная таблица

| Продукт | Сегмент | Ключевые факты (с датами) | Судьба / статус | Уверенность |
|---|---|---|---|---|
| **Roboflow** | CV, no-code/low-code | Series B $40M (ноябрь 2024; PitchBook — $37.5M); суммарно привлечено $62–100M в зависимости от источника; заявлено >16 000 организаций [1] | Растёт, новых раундов после ноября 2024 не найдено | средняя |
| **Edge Impulse** | Edge ML | Основан в 2019 (Jongboom, Shelby); ~170 000 разработчиков; Qualcomm объявил о покупке в марте 2025, цена не раскрыта [2] | Поглощён производителем чипов; бренд сохраняется, оптимизация под Dragonwing | средняя (закрытие сделки в найденных источниках не подтверждено) |
| **Google Teachable Machine** | Обучение/демо классификации | CHI 2020: >182 000 пользователей, >125 000 моделей; позднее заявка на Cannes Lions — >1.3M пользователей, >1.5M моделей (дата не указана) [3] | Живёт как образовательный/демо-инструмент, не бизнес | средняя |
| **Lobe (Microsoft)** | Desktop no-code CV | Куплен Microsoft в 2018, публичный preview в 2020, только классификация изображений [4] | Статус в поиске подтвердить не удалось; по моим знаниям (без ссылки) приложение не получило развития | низкая |
| **Landing AI / LandingLens** | Промышленный CV | Series A $57M (2021), клиенты Stanley Black & Decker, Foxconn; сейчас смещение к «Agentic Document Intelligence» [5] | Живёт, но сменил фокус (вывод: показатель того, что узкий CV-no-code ищет новую нишу) | средняя |
| **DataRobot** | Enterprise AutoML | Оценка $6.3B (2021); в 2022 уволил 26% штата, смена CEO; оценка выручки Sacra ~$225M за 2023 [6] | Выжил, пересобрался в «gen/agentic AI platform» | средняя |
| **Obviously AI** | No-code predictive | Seed $4.7M (2021); по одному агрегатору — переименование в Zams и свёртывание в августе 2026 [7] | Предположительно закрыт; один источник | низкая |
| **Akkio** | No-code AutoML для бизнеса | Series A $15M, всего $18M (данные 2021–2022) [7] | Актуальный статус не установлен | низкая |
| **SageMaker Canvas (AWS)** | No-code ML у гиперскейлера | Pay-as-you-go: ~$1.9/ч за workspace + обучение/инференс отдельно [8] | Живой продукт внутри AWS; число пользователей не раскрыто | высокая (цены) |
| **Microsoft Project Bonsai** | **No-code RL / machine teaching** | Закрыт в начале 2023 вместе с командой Industrial Metaverse (~100 увольнений) [9] | Закрыт | высокая (факт), низкая (причина) |
| **Pathmind** | **No-code RL для симуляций AnyLogic** | Бывший Skymind; привлечено ~$14.7M (Dealroom); по агрегатору остановлен в ноябре 2021 [10] | Закрыт (одиночный источник по дате) | низкая–средняя |
| **Composabl** | **No-code UI для «autonomous agents»** | Seed $4.25M (май 2024, лид Momenta); общий объём по разным источникам $5.7–8.2M [11] | Работает, малый масштаб | средняя |
| **AWS DeepRacer** | **RL для обучения** | Консольный сервис доступен до 15 декабря 2025; исходники опубликованы как AWS Solution для самостоятельного развёртывания [12] | Свёрнут как managed-сервис, остался open-source «solution» | средняя–высокая |
| **AWS RoboMaker** | Облачная симуляция роботов | Поддержка прекращена 10 сентября 2025; рекомендованная замена — AWS Batch [13] | Закрыт | высокая |
| **Unity ML-Agents** | RL для игр/симуляций | Пакет жив: релизы 4.x (4.0.0 — сентябрь 2025; 4.1.0 — июль 2026 по единственному источнику); на форуме в ноябре 2025 обсуждали метку «deprecated» без официального ответа [14] | Поддерживается, но не как продукт-платформа; требует кода на C#/Python | средняя |

### 2.2 No-code RL: что общего у закрытых прецедентов

Факты:
- Bonsai позиционировался как инструмент «machine teaching», позволяющий экспертам предметной области строить автономные системы без глубоких знаний ИИ [9][15]. Закрыт в рамках сворачивания Industrial Metaverse; публично Microsoft про Bonsai причин не объясняла, СМИ связывали с переориентацией на OpenAI [9].
- DeepRacer: консоль сервиса закрыта в декабре 2025, замена — self-deploy решение в аккаунте клиента [12].
- RoboMaker закрыт в сентябре 2025 [13].
- Pathmind был надстройкой над AnyLogic — зависимость от одной платформы-хозяина [10].

Оценка и выводы (вывод):
- Причины закрытий Bonsai/RoboMaker/DeepRacer, судя по публичным данным, — **стратегические приоритеты гиперскейлеров, а не доказанный провал технологии**. Для стартапа это двоякий вывод: нишу не «доказали» невозможной, но и **не доказали, что она даёт коммерческий результат на масштабе гиперскейлера**. Явного положительного кейса «no-code RL → большая выручка» в найденном нет (отсутствие в моих поисках не равно отсутствию в мире).
- DeepRacer — пример сильного **образовательного/комьюнити-хука** (соревнования, физическая машинка) без устойчивой монетизации у AWS; факт закрытия консоли есть, причины в найденном не раскрыты (вывод: вероятно, не масштабировался в выручку — это предположение).
- Pathmind: зависимость от стороннего симулятора + нишевость (промышленная оптимизация) (оценка).
- Типичные барьеры RL, которые no-code не снимает: нужна симуляция/цифровой двойник, sim-gap, дорогие вычисления [15]. См. 02-rl-tech-state-of-art.md, разделы про sim2real.

### 2.3 Новая парадигма: no-code = чат + агент, пишущий код

| Продукт | Данные (2026) | Уверенность |
|---|---|---|
| **Lovable** | >$500M ARR в июне 2026, по одному источнику ~$600M в сентябре; Series C $400M в августе 2026 при оценке $13.3B (удвоение от $6.6B в декабре 2025) [16] | средняя (агрегаторы со ссылкой на TechCrunch/Bloomberg) |
| **Replit** | Series D $400M при $9B (март 2026); ARR оценивается Sacra в ~$525M (апрель 2026), $150M в сентябре 2025; цель $1B к концу 2026; рост приписывают Agent и выходу к не-разработчикам. Данные по марже противоречат: ~23% против ~85% [17] | средняя/низкая |
| **Bolt.new** | $20M ARR за 2 месяца, $40M ARR к марту 2025 по агрегаторам; у StackBlitz до пивота было <$1M ARR за 7 лет [18] | средняя; данных по churn не найдено |
| **Cursor (Anysphere)** | Series D $2.3B при $29.3B (ноябрь 2025); ARR ~$2B в феврале 2026 и ~$4B позже; источники противоречат по поводу сделки со SpaceX на $60B [19] | низкая (агрегаторы расходятся) |

Что это значит (вывод):
- Скорость роста подтверждает: **массовый спрос на «опиши словами — получи результат»**. Для 2026 года основной интерфейс no-code — диалог с агентом, который сам пишет и запускает код, а пользователь правит результат, глядя на живой превью.
- Но: ни в одном из источников нет надёжных цифр удержания; по Replit противоречивые оценки маржи (23% vs 85%) [17] — **вычислительная стоимость агента может съедать маржу**. Для RL, где вычисления ещё дороже, это критично (см. 05-compute-hardware-costs.md и 06-business-models-pricing.md).
- Параллель для RL: «vibe coding» ≈ «vibe training» — пользователь описывает поведение словами, агент пишет reward/среду, запускает обучение, показывает видео и предлагает правки. Eureka показывает, что LLM способна писать reward-функции лучше экспертов на 83% тестовых задач (по сообщениям, 29 сред, 10 морфологий) [20].

---

## 3. Часть B. No-code в робототехнике

| Игрок | Подход | Факты | Ограничения (оценка/вывод) |
|---|---|---|---|
| **Wandelbots** | Обучение демонстрацией (TracePen), далее Nova — «robot-agnostic OS» | Series B $30M (2020), Series C $84M (январь 2022, Insight Partners), всего $123M; заявлено ускорение программирования «до 70 раз» (маркетинг компании) [21] | Раундов после 2022 не найдено; демонстрация→траектория, не обучение политик |
| **Micropsi Industries (MIRAI)** | Обучение «по примеру» движению с камерой, гибкая реакция на отклонения | Series B $30M (февраль 2022); клиенты Siemens Energy, ZF, BSH; партнёры ABB, NVIDIA, UR [22] | Узкие задачи (вставка, сборка); данные о выручке не найдены |
| **Standard Bots** | Cobot, обучаемый демонстрацией и no-code UI | Series B $63M (2024 или 2025 — источники расходятся); Series C $200M при $1B (по Sacra — июнь 2026, один источник) [23] | Компания продаёт и железо — «no-code» часть продукта, не отдельный бизнес |
| **Augmentus** | No-code по CAD/облаку точек для сварки и покрытия | Series A $5M (ноябрь 2023), A+ ~$11M (июль 2025); заявлено снижение времени программирования с 4 недель до 15 минут (маркетинг) [24] | Узкая вертикаль (surface finishing/welding), без обучения политик |
| **Intrinsic Flowstate** | Веб-платформа для разработки роботизированных приложений | СП с Foxconn (конец 2025), в феврале 2026 Intrinsic вошёл в Google [25] | Крупнокорпоративная модель, цель — разработчики без глубокой робототехники |
| **Viam** | Dev-платформа (open source, любой язык, облако/флот) | Series C $30M (март 2025, лид USV), всего $117M [26] | Платформа для разработчиков, не для не-программистов |
| **Formant** | Платформа телеметрии/флота | Seed $6M (2018), Series A $18M (2022), поглотил Formation (2019) [27] | Не обучение, а эксплуатация |
| **Vention, UR PolyScope/URCaps** | Не исследовано (лимит поиска) | — | Известный из общих знаний паттерн: блочное/«дерево программы» + экосистема плагинов; ссылок нет |
| **Gemini Robotics-ER 1.5** | LLM как планировщик с вызовом Robot API/VLA | Доступен через Gemini API с 25 сентября 2025; в документации июня 2026 упомянут 1.6-preview; Boston Dynamics строит поверх Spot SDK [28] | Reasoning-слой, не обучение политик |

Вывод (вывод): в робототехнике «no-code» сегодня означает почти исключительно **детерминированное программирование траекторий/процессов** (демо, CAD, блоки), а не **обучение политик с подкреплением**. Это одновременно (а) незанятая позиция для нас и (б) сигнал, что рынок платит за надёжность и сроки внедрения, а не за «ML внутри». Подробнее о рынке и конкурентах — 01-market-competitors.md; о технологиях VLA/имитации — 02-rl-tech-state-of-art.md.

---

## 4. Часть C. UX-паттерны и что доказано исследованиями

### 4.1 Таблица паттернов

| Паттерн | Что доказано (источник) | Оценка применимости к RL-платформе |
|---|---|---|
| **Визуальное программирование (блоки)** | Онлайн-исследование KTH, N=279: не-эксперты после минимального обучения создавали простые программы в готовом визуальном интерфейсе [29] | Подходит для логики «до/после» обучения (триггеры, safety-условия), не для самого обучения |
| **Task-oriented vs robot-oriented интерфейс** | 22 не-эксперта: сопоставимое время обучения и программирования при двух подходах [29] | Не стоит ожидать чуда от смены метафоры; важнее шаблоны и обратная связь |
| **Обучение демонстрацией** | Люди часто дают неэффективные демонстрации; гибрид кинестетика + визуальное программирование распространён [29]; небольшая работа показывает, что не-робототехники плохо дают иерархические демонстрации без тренировки [29] | Нужна встроенная оценка качества демонстраций и подсказки |
| **Mixed reality** | Меньше когнитивная нагрузка и быстрее выполнение, чем в 2D-интерфейсе (Brown) [29] | Нишево, требует оборудования; не для MVP |
| **Цели (goals) vs reward** | RLC 2025: не-эксперты одинаково способны задавать и интерпретировать reward и цели, но **сильно предпочитали цели**; работа предварительная [30] | Основной ввод — цель на естественном языке; reward как «продвинутый режим» |
| **Reward — сложно даже экспертам** | AAAI 2023: ручной подбор reward ведёт к переобучению под алгоритм и неверным спецификациям [30] | LLM-генерация reward + автоматическая проверка поведения; показ «что агент реально делает» |
| **Метрики выравнивания reward** | Preprint 2026: предоставление Trajectory Alignment Coefficient улучшало reward у практиков в Lunar Lander и снижало нагрузку [30] | Идея: показывать пользователю «насколько reward согласуется с вашими предпочтениями» |
| **Обратная связь оценками** | Rating-based RL (оценки сегментов траекторий) заявлен как подходящий для не-экспертов — по вторичному описанию, не по первоисточнику [30] | Human-in-the-loop через простые оценки «лучше/хуже» (A/B роллаутов) |
| **Reward shaping как «естественный» метод** | Исследование 51 участника: классический reward shaping показался наиболее естественным методом и экспертам, и не-экспертам (2018) [30] | Позволяет интерактивное «подправь в процессе» |

### 4.2 Паттерны без достаточных ссылок (выводы/гипотезы, не факты)

- **Шаблоны задач** (pick&place, ходьба, навигация, balance) — снижают пустой экран; в нашем поиске прямых RL-HCI-исследований не найдено. Аналогия: на Teachable Machine рост пользовательской базы связан с мгновенным результатом в браузере (3: 182k пользователей / 125k моделей к 2020 г.) (оценка).
- **Видео роллаутов и кривые**: для не-экспертов видео понятнее кривых (гипотеза; проверить A/B на своих пользователях).
- **One-click deploy** — ценность подтверждена косвенно успехом AWS DeepRacer на физической машинке (есть в [12], но причина популярности в найденном не раскрыта) и подходом Edge Impulse «данные→модель→устройство» [2].
- **Escape hatch в код**: Viam и Unity ML-Agents — code-first платформы; Roboflow/Edge Impulse открывают код/SDK (общие знания; пруфов в найденном нет).

---

## 5. Часть D. Главные причины провалов no-code ML и как избежать

| Причина | Свидетельства | Как избежать (вывод) |
|---|---|---|
| **Потолок возможностей** — упираешься в ограничения, нужен код | Lobe поддерживал лишь классификацию изображений [4]; Pathmind был завязан на AnyLogic [10] | Слой «full-code снизу»: экспорт проекта в Python/Isaac/Mujoco-код, свои reward/сенсоры |
| **Утечка продвинутых пользователей** | Явных цифр не найдено; наблюдение по Unity ML-Agents / Viam (code-first) | Делать продвинутым выгодным оставаться: совместная работа, версии, вычисления, маркетплейс шаблонов |
| **Слишком узкий рынок** | Obviously AI — предположительное закрытие в 2026 [7]; Landing AI сменил фокус [5]; Pathmind — одна ниша [10] | Не привязываться к одному симулятору/отрасли; широкая «агентная» ось (роботы + игры + операции) — см. 04-beyond-robotics-use-cases.md |
| **Стоимость вычислений** | Спор о марже Replit (23% vs 85%) [17]; RL требует тысяч симуляций | Квоты + лимиты, предоплаченные кредиты, превью-обучение на малом бюджете; см. 05-compute-hardware-costs.md, 06-business-models-pricing.md |
| **Нет ценности для бизнеса / приоритеты вендора** | Bonsai закрыт при реорганизации [9]; RoboMaker [13]; DeepRacer [12] | Начинать с задач с измеримым ROI, не быть «фичей» гиперскейлера; избегать зависимости от одного облака |
| **Sim-gap** | Отмечается как общая проблема RL [15] | Домен-рандомизация по умолчанию; режим «проверка на реальном роботе» с безопасными лимитами; см. 07-risks-safety-regulation.md |
| **Фундаментальная сложность постановки задач** | Reward misdesign [30] | Чат-помощник + автогенерация и аудит reward (Eureka-подход [20]) |

Честная оговорка: **доказательной базы о том, что именно привело к закрытию Bonsai/DeepRacer, нет** — это наша интерпретация (вывод).

---

## 6. Часть E. Рекомендации по UX платформы

### 6.1 Персоны

| Персона | Цель | Входной сценарий | Критичное |
|---|---|---|---|
| **Хоббист** (дрон, робот-пылесос, Arduino/Raspberry) | Увидеть, как «оно учится» | Шаблон + симуляция в браузере | Бесплатный старт, понятные видео |
| **Студент** | Курсовая/диплом | Шаблон + эксперименты + экспорт кода | Образовательные кредиты, воспроизводимость |
| **Инженер завода** | Заменить ручную настройку | Загрузка CAD/сцены или демонстрации | Безопасность, отчёты, деплой на оборудование |
| **Разработчик игр** | NPC и баланс | Плагин для Unity/Unreal | Интеграция в движок (Unity ML-Agents — отправная точка [14]) |
| **ML-инженер** | Быстрее прототипировать | API/SDK/CLI | Escape hatch, открытый формат |

Это персоны-гипотезы (вывод); приоритезация сегментов — в 08-ecosystem-community-gtm.md.

### 6.2 Путь (user journey) до первого обученного агента

1. Регистрация одним кликом (без карты), сразу чат: «Что вы хотите, чтобы агент делал?».
2. Агент предлагает 3 шаблона + возможность описать словами; создаёт среду в симуляторе.
3. Автогенерация reward + показ «как я понял цель» (текст + короткий ролик нулевой политики).
4. Запуск обучения с живыми видео-роллаутами каждые N шагов, кривая прогресса «в человеческих терминах» (успех в %).
5. Human-in-the-loop: кнопки «лучше/хуже» для пар роллаутов, правка цели в чате.
6. Сравнение версий (A/B), выбор лучшей.
7. One-click: расшаренная ссылка, экспорт, деплой на реального робота/в движок.
8. «Открыть как код» — полный проект.

**Целевой time-to-first-wow: ≤10 минут** (это целевая оценка, а не измеренный факт). В пользу цели: Teachable Machine построен на мгновенном результате в браузере [3].

### 6.3 Принципы

- **«No-code сверху, full-code снизу».** Чат — основная поверхность; под ним всегда видны сгенерированные reward, конфиг, скрипты (аналог Lovable/Replit, где пользователь может заглянуть в код) (вывод по [16][17]).
- **Цель словами, а не reward** — по результатам RLC 2025, где участники сильнее предпочитали цели [30].
- **Агент как наставник по диагностике**: «обучение застряло — вот 3 возможные причины».
- **Безопасность по умолчанию** для реальных роботов (лимиты скоростей/усилий, dry-run) — см. 07-risks-safety-regulation.md.
- **Не обещать универсальность**: честная матрица «что получится / что нет».

### 6.4 Метрики для проверки UX (предлагаемые)

- TTFW (медиана до первого видео с успешным поведением), доля завершивших первую задачу, доля, перешедшая на «открыть как код», стоимость вычислений на активного пользователя, удержание D7/D30.

---

## Выводы для платформы

1. **Прецеденты no-code RL (Bonsai, Pathmind, DeepRacer-консоль, RoboMaker) закрыты** — это предупреждение: спрос на «RL без кода» не доказан в масштабе, причины закрытий публично не раскрыты; закладывать гипотезу «найдём устойчивый платящий сегмент» как главный риск [9][10][12][13].
2. **Основной интерфейс — чат с агентом**, как у Lovable/Replit/Cursor, чей рост в 2026 годовых выручках исчисляется сотнями миллионов — миллиардами [16][17][19]. Но это не подтверждает рентабельность: у Replit данные по марже противоречивы [17].
3. **Ввод цели — естественный язык**, reward генерируется и проверяется агентом (Eureka-подход); ручной reward — режим для продвинутых [20][30].
4. **Обучение демонстрацией включать как опцию с обратной связью о качестве демо**: не-эксперты демонстрируют плохо [29].
5. **Вертикаль и кроссплатформенность**: не привязываться к одному симулятору (урок Pathmind) и не к одному облаку (урок AWS/Microsoft) [10][12][13].
6. **Escape hatch обязателен**: всегда экспорт кода/политик; держать продвинутых пользователей внутри через вычисления, коллаборацию и маркетплейс шаблонов (гипотеза).
7. **Вычислительная экономика с первого дня**: кредиты, квоты, «превью-обучение» дешёвое; следить за маржой (см. 05, 06).
8. **Робототехнический no-code сегодня — это детерминированные программы**; позиция «обучение политик для не-экспертов» свободна, но рынок платит за надёжность (Standard Bots, Augmentus, Wandelbots) [21][23][24]. Начинать с задач, где результат измерим (cycle time, % успеха).
9. **Образовательный хук** (аналог Teachable Machine: >182k пользователей к 2020, DeepRacer) полезен для воронки, но не заменяет монетизацию [3][12].
10. **Неизвестное, что нужно проверить интервью/прототипами**: реальный TTFW, удержание, готовность платить в каждой персоне; в нашем поиске нет прямых RL-HCI-исследований о видео-роллаутах и шаблонах.

---

## Источники

[1] Roboflow funding / Series B ($40M, Nov 2024; PitchBook $37.5M; CB Insights $62.75M total; >16 000 организаций) — агрегаторы и страницы компании: https://roboflow.com/contact ; https://pitchbook.com/profiles/company/439526-44 ; https://www.cbinsights.com/company/roboflow ; https://www.clay.com/dossier/roboflow-funding — (дата обращения 2026-10-27)
[2] Qualcomm acquires Edge Impulse — Hackster.io / EdgeIR / AI Business — https://hackster.io/news/qualcomm-to-acquire-edge-impulse-as-it-seeks-to-gain-ground-in-the-artificial-intelligence-of-things-2db3bb6f0d63 ; https://www.edgeir.com/qualcomm-acquires-edge-impulse-accelerating-ai-and-iot-expansion-at-the-edge-20250317 — (2026-10-27)
[3] Teachable Machine: Approachable Web-Based Tool… — Google Research (CHI 2020) — https://research.google/pubs/teachable-machine-approachable-web-based-tool-for-exploring-machine-learning-classification ; Cannes Lions entry — https://www.lovethework.com/work-awards/campaigns/teachable-machine-724027 — (2026-10-27)
[4] Microsoft adds Lobe to AI lineup — Redmond Magazine (2018) — https://redmondmag.com/articles/2018/09/13/microsoft-adds-lobe-to-ai-lineup.aspx ; public preview — https://aibusiness.com/ml/microsoft-makes-machine-learning-more-accessible-with-public-preview-of-lobe — (2026-10-27)
[5] Landing AI Series A $57M — BetaKit / HPCwire — https://betakit.com/mcrock-capital-leads-57-million-usd-round-for-californias-landing-ai-created-by-former-google-brain-lead/ ; https://startupintros.com/orgs/landingai — (2026-10-27)
[6] DataRobot layoffs/valuation — TechTarget; Boston Globe; Sacra — https://techtarget.com/searchenterpriseai/news/252524275/Troubled-AI-vendor-DataRobot-hit-by-more-layoffs ; https://www.bostonglobe.com/2022/08/25/business/boston-tech-startup-datarobot-slashes-26-percent-staff ; https://sacra.com/c/datarobot/valuation/ — (2026-10-27)
[7] Obviously AI / Akkio — yespress.io; VentureBeat — https://yespress.io/obviously-ai ; https://venturebeat.com/ai/akkio-raises-15m-to-advance-no-code-ai-platform-for-enterprises — (2026-10-27)
[8] Amazon SageMaker Canvas pricing — AWS — https://aws.amazon.com/sagemaker/canvas/pricing/ — (2026-10-27)
[9] Microsoft cuts industrial metaverse team (Project Bonsai) — Redmond Magazine — https://redmondmag.com/articles/2023/02/10/microsoft-reportedly-cuts-industrial-metaverse-team.aspx ; https://www.computing.co.uk/news/4139346/microsoft-halts-flagship-metaverse-ventures-layoffs-loom — (2026-10-27)
[10] Pathmind — Dealroom, APIs.io, Craft — https://dealroom.co/companies/pathmind/ ; https://apis.io/providers/skymind/ ; https://craft.co/pathmind — (2026-10-27)
[11] Composabl launches no-code UI platform and raises $4.25M — Arc / press release — https://www.arcweb.com/node/149576 ; https://www.vcbacked.co/company/composabl — (2026-10-27)
[12] AWS DeepRacer final league / DeepRacer on AWS — AWS — https://aws.amazon.com/blogs/machine-learning/celebrating-the-final-aws-deepracer-league-championship-and-road-ahead ; https://docs.aws.amazon.com/solutions/latest/deepracer-on-aws/solution-overview.md ; https://builder.aws.com/content/2otsNvwo08hywC4Ovpr7mi1ySyI/deepracer-is-back-first-impressions-of-deepracer-on-aws — (2026-10-27; страницы получены только через сниппеты поиска, прямое открытие не удалось)
[13] AWS RoboMaker end-of-support notice — AWS Docs — https://docs.aws.amazon.com/robomaker/latest/dg/using-service-linked-roles.html — (2026-10-27)
[14] Unity ML-Agents — Unity Discussions; mirror коммитов — https://discussions.unity.com/t/is-ml-agents-being-deprecated/1643681 ; https://www.issoh.co.jp/md/tech/4905 ; https://code.morphllm.com/Unity-Technologies/ml-agents/commits/branch/develop — (2026-10-27)
[15] Machine teaching: How people's expertise makes AI even more powerful — Microsoft Blogs — https://blogs.microsoft.com/latinx/2019/05/01/machine-teaching-how-peoples-expertise-makes-ai-even-more-powerful/ — (2026-10-27)
[16] Lovable — valuation/ARR — Wikipedia и агрегаторы — https://en.wikipedia.org/wiki/Lovable_(company) ; https://valueaddvc.com/pulse/company/lovable ; https://devgraphiq.com/lovable-stats/ — (2026-10-27)
[17] Replit — valuation/ARR — агрегаторы — https://valueaddvc.com/pulse/company/replit ; https://www.northmetric.io/estimate/replit ; https://www.techbuzz.ai/articles/replit-hits-9b-valuation-eyes-1b-arr-in-monster-round — (2026-10-27)
[18] Bolt.new statistics / Lenny's Newsletter — https://www.getpanto.ai/blog/bolt-new-statistics ; https://www.lennysnewsletter.com/p/inside-bolt-eric-simons — (2026-10-27)
[19] Cursor / Anysphere — Wikipedia, агрегаторы — https://en.wikipedia.org/wiki/Anysphere ; https://valueaddvc.com/company/cursor ; https://getlatka.com/companies/cursor.com — (2026-10-27)
[20] Eureka: Human-Level Reward Design via Coding LLMs — NVIDIA Research (ICLR 2024); пересказ — https://www.robotics247.com/article/eureka_nvidia_research_uses_large_language_models_train_robots/nvidia ; https://venturebeat.com/ai/new-nvidia-ai-agent-powered-by-gpt-4-can-train-robots/ — (2026-10-27; первоисточник arXiv не открывали)
[21] Wandelbots Series C $84M / Series B $30M — The Robot Report; Tech.eu — https://www.therobotreport.com/wandelbots-raises-84m-for-no-code-robotics-programming/ ; https://tech.eu/brief/wandelbots-series-b/ — (2026-10-27)
[22] Micropsi Industries Series B $30M — Micropsi blog; Robotics 24/7 — https://micropsi-industries.com/blog/micropsi-industries-secures-30m-in-series-b ; https://www.robotics247.com/article/micropsi_raises_30m_series_b_funding_to_scale_industrial_automation_with_human_motion_trained_robots — (2026-10-27)
[23] Standard Bots — Series B $63M / Series C $200M — https://standardbots.com/blog/standard-bots-raises-63m-to-accelerate-ai-in-robotics ; https://sacra.com/c/standard-bots ; https://aiweekly.co/alerts/standard-bots-hits-1b-valuation-with-200m-round — (2026-10-27)
[24] Augmentus raises $11M — Evertiq; Pulse 2.0 — https://evertiq.com/news/2025-07-30-augmentus-raises-11m-to-advance-robotic-surface-finishing-welding ; https://pulse2.com/augmentus-5-million-funding/ — (2026-10-27)
[25] Intrinsic joins Google; Foxconn JV — TechCrunch; SiliconANGLE; The Robot Report — https://techcrunch.com/2026/02/25/alphabet-owned-robotics-software-company-intrinsic-joins-google ; https://siliconangle.com/2025/11/20/alphabets-intrinsic-foxconn-plan-accelerate-factory-automation-smarter-robots ; https://www.therobotreport.com/foxconn-intrinsic-building-flexible-robots-for-us-factories/ — (2026-10-27)
[26] Viam announces $30M Series C — Viam; Fortune — https://www.viam.com/press-releases/viam-announces-30-million-series-c ; https://fortune.com/2025/03/03/mongodb-viam-union-square-ventures-albert-wenger-ai-robotics/ — (2026-10-27)
[27] Formant — Robotics 24/7; The Robot Report — https://www.robotics247.com/article/formant_raises_series_a_funding_for_cloud_based_robot_fleet_management_platform ; https://www.therobotreport.com/formant-buys-formation-teleoperation-robotics-fleet-management/ — (2026-10-27)
[28] Gemini Robotics-ER 1.5 — Google AI for Developers; Boston Dynamics — https://ai.google.dev/gemini-api/docs/models/gemini-robotics-er-1.5-preview ; https://bostondynamics.com/blog/tools-for-your-to-do-list-with-spot-and-gemini-robotics/ — (2026-10-27)
[29] End-user robot programming (HCI) — arXiv 2406.00841; JHU Huang et al. 2020; Brown H2R (Gadre 2019); Frontiers in Robotics and AI 2021; IEEE Access 2019 — https://arxiv.org/html/2406.00841v1 ; https://www.cs.jhu.edu/~cmhuang/documents/publications/huang2020contextual.pdf ; https://h2r.cs.brown.edu/wp-content/uploads/gadre19.pdf ; https://www.frontiersin.org/journals/robotics-and-ai/articles/10.3389/frobt.2021.646002/full ; https://doaj.org/article/ea0c23500cb64658981beacfe6bf4703 — (2026-10-27; выводы взяты из сниппетов поиска, полные тексты не читались; соотнесение отдельных тезисов с конкретными работами неточное — проверить перед цитированием)
[30] Reward / goal specification studies — Rani, Booth, Sreedharan, RLJ/RLC 2025; Booth et al. AAAI 2023; arXiv 2601.16906; KER 2018 — https://rlj.cs.umass.edu/2025/papers/Paper308.html ; https://ojs.aaai.org/index.php/AAAI/article/view/25733 ; https://arxiv.org/abs/2601.16906v1 ; https://maxapress.com/data/article/ker/preview/pdf/S0269888918000206.pdf — (2026-10-27; сниппеты поиска)
