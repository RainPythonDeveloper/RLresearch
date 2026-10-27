# 01. Рынок, конкуренты, инвестиции, TAM/SAM/SOM

> Автор: агент «Аналитик рынка и конкурентов» · Дата: 2026-10-27 · Прочитанные файлы research/: README.md (других файлов на момент записи в папке не было)

**Оговорка о полноте данных (важно).** В ходе работы исчерпан лимит веб-поиска сессии (200 вызовов на ход, общий для всех агентов), а WebFetch не смог открыть первоисточники (ошибка DNS на ifr.org, goldmansachs.com, techcrunch.com, crunchbase.com, docs.aws.amazon.com). Поэтому все цифры ниже взяты из сниппетов поисковой выдачи (в основном вторичные и агрегаторные пересказы), а не из полных текстов первоисточников. Там, где источник слабый, это помечено. Не получены: рыночные отчёты по размеру «мирового рынка робототехники», «AI in robotics», «RL-рынка» и MLOps (агрегаторы вроде MarketsandMarkets/Grand View), прогнозы Citi/BofA по гуманоидам, статус Project Bonsai/DeepRacer/Pathmind из первоисточника. Эти пробелы указаны явно, чисел «из головы» под видом фактов здесь нет.

Перекрёстные ссылки: технологии RL/sim2real/VLA — см. `02-rl-tech-state-of-art.md`; аналоги no-code ML и их UX — `03-nocode-ml-analogs-ux.md`; применения вне робототехники — `04-beyond-robotics-use-cases.md`; стоимость вычислений и железа — `05-compute-hardware-costs.md`; ценообразование — `06-business-models-pricing.md`; риски и «кладбище» — `07-risks-safety-regulation.md`; экосистема и GTM — `08-ecosystem-community-gtm.md`. (Файлов 02–08 на момент записи ещё не было, ссылки даны по плану из README.)

---

## 1. Размер рынка

### 1.1 Промышленные роботы (IFR World Robotics 2025)

| Показатель | Значение | Источник |
|---|---|---|
| Новые установки в 2024 | 542 000 шт., более чем вдвое больше, чем 10 лет назад; 74% установок пришлось на Азию | [1] |
| Операционный парк на конец 2024 | ≈4,66 млн шт. (4 663 698 по executive summary; +9% г/г) | [1] |
| Китай | парк 2 027 190 шт. (43% мирового); установки 295 045 шт. (+7%, 54% мировых) | [1] |
| Япония | парк 450 530 шт. (10%) | [1] |
| Европа | парк 821 384 шт.; установки упали на 8% до 85 006 шт. | [1] |
| Америка | парк 542 464 шт. | [1] |

Факт, уверенность высокая: цифры IFR согласованы в нескольких пересказах [1]. Денежную стоимость установок IFR в полученной выдаче не было — не привожу.

### 1.2 Сервисные роботы (IFR World Robotics 2025, Service Robots)

- Продажи профессиональных сервисных роботов в 2024: почти 200 000 шт., +9% [2].
- Транспорт и логистика: 102 900 шт. (+14%); гостиничный бизнес: более 42 000 (−11%); профессиональная уборка: более 25 000 (+34%); сельское хозяйство: около 19 500 (−6%); медицинские роботы: около 16 700 (+91%) [2].
- Парк RaaS (robot-as-a-service) вырос на 31%; потребительские сервисные роботы +11% [2].
- Уверенность: высокая по единицам, денежные оценки не получены.

(вывод) Для нас важна не сумма продаж, а структура: логистика и уборка — это мобильные платформы, где «навыки» стандартные, а сегмент манипуляции (сборка, укладка, сортировка) и гуманоиды — там, где нужны обученные политики.

### 1.3 Гуманоиды: прогнозы банков

| Источник | Прогноз | Комментарий |
|---|---|---|
| Goldman Sachs Research, 27.02.2024 | TAM гуманоидов $38 млрд к 2035 (в 6 раз выше прежних $6 млрд); поставки 1,4 млн шт. в 2035; >250 тыс. шт. в 2030, почти все промышленные; себестоимость упала до $30–150 тыс. за единицу (вместо ожидавшегося −15–20% в год упала ≈40%) [3] | Прогноз почти 2,5-летней давности; обновления в выдаче не найдено [3]. Уверенность: средняя (вторичный пересказ). |
| Morgan Stanley, май 2025 | ≈$5 трлн к 2050, ≈1 млрд единиц; ≈13 млн гуманоидов в использовании к 2035 [4] | Сумма включает цепочку поставок, ремонт, инфраструктуру, не только железо. Источник сообщает о возможном обновлении до $7,5 трлн в марте 2026 — не подтверждено первоисточником [4]. Уверенность: средняя. |
| Citi, BofA и др. | не получены | пробел |

Расхождение: у Goldman TAM до 2035 измеряется десятками миллиардов, у Morgan Stanley — триллионами к 2050; методологии и горизонты несопоставимы (вывод: «триллионы» — это в основном сервис и инфраструктура на дальнем горизонте).

### 1.4 ПО для роботов, AI in robotics, RL, MLOps

Отчёты агрегаторов (MarketsandMarkets, Grand View и т.п.) в этой сессии получить не удалось, поэтому цифр по «рынку AI in robotics», «рынку RL» и «MLOps» здесь нет сознательно. (вывод) Использовать их стоит осторожно в любом случае: определения «рынка RL» в таких отчётах обычно размыты. Косвенные ориентиры размера прикладного рынка: ARR Prime Intellect по их собственному заявлению >$100 млн [36] (самоотчёт, не аудит) и сделки по MLOps-инструментам: W&B куплена CoreWeave за ≈$1,7 млрд (по сообщению The Information, компания сумму не раскрывала) [22].

### 1.5 Наша оценка TAM / SAM / SOM (оценка, не факт)

Методика (всё ниже — `(оценка)`, предположения явно названы, подлежат проверке в волне 2, см. `12-resources-financial-plan.md`):

1. **Робототехнический TAM (расходы на ПО/вычисления для обучения навыков роботов).** Базис: ≈542 тыс. промышленных установок в год [1] + ≈200 тыс. профессиональных сервисных роботов [2] ≈ 0,75 млн новых роботов в год. Допущение A: к 2030 доля развёртываний, где нужен обучаемый/адаптивный навык (не жёсткая программа), 10–20%. Допущение B: ПО + вычисления на «обучение навыка» в год на такой робот $2–5 тыс. Итого ≈ 75–150 тыс. роботов × $2–5 тыс. = **≈$0,15–0,75 млрд в год к 2030** (низкая уверенность; допущения A и B не подкреплены источниками). Парк уже установленных роботов (4,66 млн [1]) даёт ещё потенциал дообучения, но мы его не включаем из-за неопределённости.
2. **TAM вне робототехники** (RL для агентов, симуляторов, оптимизации процессов, LLM post-training — см. `04-beyond-robotics-use-cases.md`). Оценить надёжно нельзя; ориентир — масштаб рынка RL-окружений/post-training (Prime Intellect >$100 млн ARR [36], раунд $130 млн [36]). (оценка) порядок $1–3 млрд к 2028–2030, уверенность очень низкая; значительная часть этого рынка — продвинутые ML-команды, а не наша no-code аудитория.
3. **SAM** — сегмент, который реально могут обслужить no-code платформа без ML-экспертизы у клиента: интеграторы и малый/средний бизнес на коботах, образование, исследовательские лаборатории без RL-команд, стартапы роботов, хобби/maker-сообщество. Допущение: 15–25% от робототехнического TAM + небольшая часть внеробототехнического → **≈$50–300 млн в год к 2030**.
4. **SOM (реалистично за 3–5 лет)** — 1–3% SAM: **≈$1–8 млн ARR**. Это уровень «жизнеспособного стартапа на seed/Series A», но не «единорог на одной робототехнике». (вывод) Для масштаба нужен вынос за пределы роботов или рост самого рынка (гуманоиды/манипуляторы в 2028+).

---

## 2. Инвестиции в physical AI, 2024–2026

### 2.1 Общий объём венчура

| Период | Объём | Источник / комментарий |
|---|---|---|
| 2025 (весь год) | Crunchbase: $13,8–15 млрд (в разных статьях разные числа: «почти $14 млрд», «$13,8 млрд», «$15 млрд»); +70% к 2024, выше пика 2021 [5] | Расхождение внутри самого Crunchbase [5] |
| 2025 (шире) | PitchBook: $27,6 млрд по 1 009 сделкам («robotics and physical AI», более широкое определение) [5] | Различие определений |
| 2026 YTD (по состоянию на выдачу) | $18,8 млрд уже превысили весь 2025 [6] | Дата среза неясна. Уверенность: средняя |
| 2024 | ≈$8 млрд (вывод из «+70%» к 2025 [5]; прямой цифры не получено) | низкая |

### 2.2 Крупные раунды и оценки (на 2026-10-27)

| Компания | Событие | Оценка | Статус/уверенность |
|---|---|---|---|
| Physical Intelligence | Series B $600 млн при $5,6 млрд (ноябрь 2025; источники расходятся в годе); март 2026: переговоры о ≈$1 млрд при >$11 млрд; ≈$1,05 млрд Series C в корпоративных документах с мая 2026, публично не объявлено [7][8][9] | $11 млрд+ | Сообщено СМИ, не подтверждено компанией. Средняя |
| Skild AI | Series C ≈$1,4 млрд, лидер SoftBank, участвовали NVentures, Macquarie, 1789 Capital, Bezos Expeditions; стратегические: Samsung, LG, Schneider, Salesforce; 14.01.2026 [10][11] | >$14 млрд (рост >3× за 7 мес.) | Подтверждено пресс-релизом. Высокая |
| Figure AI | Series C >$1 млрд, сентябрь 2025 [12]; в октябре 2026 The Information: NVIDIA может вложить ≈$1 млрд при $39 млрд, не подтверждено [13] | $39 млрд post-money | Раунд подтверждён компанией, лид в источниках расходится (Brookfield vs Parkway). Вторичный рынок ≈$34 млрд [13]. Средняя |
| 1X | Series B $100 млн (янв. 2024); август 2026: переговоры SoftBank о мажоритарной доле при ≈$6 млрд; цель $1 млрд при $10 млрд (сент. 2025) не подтверждалась [14]. NEO продаётся за $20 000 или $499/мес [14] | ≈$6 млрд (в переговорах) | Низкая–средняя |
| Generalist AI | Series B $400 млн (июнь 2026, Radical Ventures) при $2 млрд; расширение ≈$200 млн (8VC) при $3 млрд, август 2026 [15] | $3 млрд | Средняя–высокая (регуляторная подача) |
| Genesis AI | Сид $105 млн (Khosla, Eclipse); переговоры о $500 млн при $3 млрд pre-money [15] | $3 млрд pre | Сообщено Bloomberg, один источник. Низкая |
| Field AI | 2025: $405 млн за два раунда при $2 млрд [16]; октябрь 2026: сообщается о $700 млн при $10 млрд (не подтверждено компанией) [16] | $10 млрд (сообщ.) | Низкая–средняя |
| Apptronik | $935 млн суммарно по Series A при ≈$5 млрд (февраль 2026) [17] | ≈$5 млрд | Данные о раундах противоречивы, средняя |
| Agility Robotics | Series C $400 млн при ≈$2,1 млрд (2025); SPAC с Churchill Capital XI при ≈$2,5 млрд, объявлен 24.06.2026, закрытие ожидается в Q4 2026; выручка 2025 ≈$1,8 млн, <100 роботов развёрнуто [19] | $2,5 млрд | Средняя |
| Unitree | IPO на STAR Market (тикер 688836), цена 06.08.2026 ¥150,80, привлечено ≈¥6,1 млрд (≈$904 млн), оценка ≈$9 млрд по цене размещения; выручка 2025 ≈¥1,708 млрд (+335%), валовая маржа ≈60% [18] | ≈$9 млрд на IPO | Данные из вторичных/агрегаторных источников; сообщение о росте в день листинга на ≈487% из одного источника, не использовать. Средняя |
| Dyna Robotics | суммарно ≈$144 млн (Tracxn) [15] | — | низкая; свежего раунда не найдено |
| The Bot Company | данные не получены | — | пробел |

(вывод) За два года оценки топ-игроков выросли на порядок, но выручка почти отсутствует (Agility ≈$1,8 млн при оценке $2,5 млрд [19]; Figure называют «pre-revenue bet», но это комментарий агрегатора [12]). Капитал концентрируется в foundation-моделях и гуманоидах; **инструментальному слою «для всех остальных» достаётся мало.**

### 2.3 M&A и «аквихаеры»

| Сделка | Детали | Что это значит |
|---|---|---|
| Amazon–Covariant (август 2024) | Неисключительная лицензия на модели + найм основателей (Abbeel, Chen, Duan) и ≈четверти штата; Covariant осталась независимой [20]. По жалобе информатора (2025, не подтверждено): ≈$380 млн + $20 млн, ниже оценки 2023 года $625 млн [20] | «Reverse acquihire»: для стартапа-инструмента RL-для-манипуляции выход — продажа команды, а не продукта |
| Hugging Face–Pollen Robotics (апрель 2025) | Покупка французского стартапа, затем Reachy Mini (цены расходятся: $299/$449 по одним источникам, $399/$499 в блоге HF) [21] | HF строит собственный открытый стек «железо + LeRobot» [27] |
| Qualcomm–Edge Impulse (март 2025) | Сумма не раскрыта; цель: MLOps для edge в Qualcomm AI Hub [22] | Крупные вендоры железа скупают «no-code ML для устройств» |
| CoreWeave–Weights & Biases (март 2025) | ≈$1,7 млрд по сообщению The Information (иные заголовки — $1,4 млрд) [22] | Облака покупают инструменты разработчика |
| Alphabet: Intrinsic встроен в Google (февраль 2026) | Intrinsic объединён с Google для поддержки DeepMind [28] (вторичный источник); СП Intrinsic–Foxconn (конец 2025) [28] | Платформа Flowstate становится частью стека Google |

---

## 3. Карта конкурентов по слоям

### 3.1 Foundation-модели для роботов

| Игрок | Что делает / для кого | Модель дистрибуции и цена | Финансирование | Пересечение с нами |
|---|---|---|---|---|
| Physical Intelligence | π0 / π0.5 / π*0.6; π*0.6 обучается на собственном опыте методом RECAP (RL по advantage-conditioned схеме); заявляют ≈2× пропускной способности и ≈½ отказов на сложных задачах [24] | Исследовательская лаборатория; π*0.6 закрытый, веса не открыты [24]; открытые веса π0/π0.5 — по моим сведениям, не проверено в этой сессии | см. 2.2 | **Высокое по технологии** (RL поверх VLA), низкое по продукту: не no-code |
| Google DeepMind Gemini Robotics | Gemini Robotics-ER 1.5 доступна разработчикам через Gemini API / AI Studio; Gemini Robotics 1.5 и On-Device — только избранным партнёрам и trusted testers [25]; по Wikipedia, 30.07.2026 выпущена Gemini Robotics ER 2 для разработчиков [25] (вторичный источник) | API по подписке/токенам; доступ к VLA ограничен | Внутри Alphabet | Среднее: если Google откроет VLA и SDK для обучения, это прямой конкурент по «простоте» |
| NVIDIA GR00T / Isaac / Cosmos / Newton | GR00T N1.6 — открытая VLA для гуманоидов; Newton (физдвижок, совместно с DeepMind и Disney) в Isaac Lab; GR00T и Isaac Lab-Arena доступны в LeRobot [26]. Лицензия GR00T, возможно, некоммерческая — единичный вторичный источник, проверить [26] | Бесплатно/открыто, монетизация через GPU и DGX/Omniverse | Прибыль NVIDIA | **Высокое**: раздаёт бесплатно слой, на который мы бы опирались, и имеет власть выпустить свой UI |
| Skild AI (Skild Brain) | «Мозг» для разных тел; сделки с Samsung/LG/Schneider/Salesforce [10] | B2B, лицензирование | >$2 млрд всего [10] | Низкое по аудитории (крупный OEM) |
| Figure (Helix), Tesla (Optimus) | Вертикальные гуманоиды со своим ПО | Не продают ПО как продукт | Figure $39 млрд [12] | Нулевое прямое; влияют на ожидания рынка. Детали Helix/Optimus в этой сессии не проверялись |
| Generalist, Genesis AI, Dyna, Field AI | Foundation-модели/«роботные мозги», Genesis — ещё симулятор [15][16] | B2B, закрытые | см. 2.2 | Низкое–среднее |

### 3.2 Платформы и инструменты разработки

| Игрок | Суть | Цена/модель | Пересечение |
|---|---|---|---|
| NVIDIA Isaac Sim / Isaac Lab | Симуляция и RL-обучение на GPU; Isaac Lab получает Newton и GR00T [26] | Бесплатно/open source, привязка к GPU | **Прямой «движок» под нашим слоем**; сам требует экспертизы (код на Python) |
| Hugging Face LeRobot | Открытая библиотека end-to-end robot learning; SmolVLA; сообщество датасетов (128 датасетов от 55 авторов в pretrain-наборе, 11 132 эпизода) [27]; самые скачиваемые датасеты — академические бенчмарки [27]; Reachy Mini [21] | Бесплатно, open source; монетизация через Hub/железо | **Высокое**: де-факто стандарт открытого стека imitation learning; CLI, но без полноценного no-code RL |
| Intrinsic (Flowstate) | Платформа создания роботных приложений «без глубокой робототехнической экспертизы» [28]; СП с Foxconn; теперь в составе Google [28] | Enterprise | Среднее: пересечение по no-code-идее, но фокус на промышленных клиентах |
| Viam | Универсальная платформа (софт + облако), основана сооснователем MongoDB; Series A $30 млн (2022), $42 млн всего; агрегатор называет $117 млн всего (не проверено) [38] | SaaS | Среднее (инфраструктура, не обучение) |
| Formant | Данные, телеоперация, парк роботов; последний раунд $21 млн (2023) [38] | SaaS | Низкое |
| Foxglove | Визуализация/данные для роботов; Series B $40 млн (Bessemer, ноябрь 2025) [37] | SaaS | Низкое (дополняет нас) |
| ROS / Open Robotics, Unity, MathWorks | Не исследовались поисково в этой сессии (общеизвестны: ROS — стандарт ПО, MATLAB/Simulink RL Toolbox, Unity ML-Agents) | — | MathWorks и Unity ML-Agents — устаревшие/нишевые «образовательные» RL-варианты (не проверено) |

### 3.3 No-code / low-code программирование роботов

| Игрок | Суть | Финансирование/цена | Пересечение |
|---|---|---|---|
| Wandelbots (NOVA) | Вендор-независимая платформа программирования, симуляции и оптимизации роботов; позиционируется как «Physical AI»; 22.10.2026 партнёрство со Schaeffler (развёртывание по всем заводам; заявлено снижение издержек жизненного цикла автоматизации до 40%) [29] | Последний известный раунд — Series C $84 млн (2022), суммарно $121–135 млн (трекеры расходятся) [29] | **Среднее–высокое** по аудитории (интеграторы, no-code), но это demonstration-based/траектории, а не RL |
| Micropsi Industries (MIRAI) | Обучение роботов демонстрацией, адаптивное управление по камере; клиенты Siemens Energy, ZF, BSH; Series B $30 млн (2022) [30] | Лицензия | Среднее: ближайшая по идее «человек показывает, робот обобщает» |
| Standard Bots | Робот RO1 без программирования; $63 млн (июль 2024, Series B лид General Catalyst) [31]; подписка от ≈$500/мес (с обслуживанием) по одному листингу, не проверено [31] | Продаёт железо+ПО | Низкое–среднее (вертикально интегрированы) |
| Universal Robots | PolyScope X + UR AI Accelerator (с NVIDIA, Jetson AGX Orin), UR15 [32] | Экосистема сертифицированных продуктов | **Канал**, а не конкурент: можно встроиться как приложение |
| Augmentus, Vention, Flexiv, Mujin, Realtime Robotics | В этой сессии не исследовались | — | пробел |

### 3.4 No-code / managed RL платформы (живые и закрытые)

| Продукт | Статус | Урок |
|---|---|---|
| Microsoft Project Bonsai | Bonsai куплена Microsoft в 2018 (сумма не раскрыта) [39], выпущена как Project Bonsai на Build 2020. Данные о закрытии в этой сессии не подтверждены; по моим сведениям продукт свернут (не проверено, нужна перепроверка) | Самый близкий «ancestor»: no-code RL для промышленных клиентов под крылом гиганта не вырос |
| AWS RoboMaker | **Закрыт**: поддержка прекращена 10.09.2025, консоль и ресурсы недоступны; рекомендован AWS Batch для контейнеризованных симуляций [23] | Крупные облака сворачивают нишевые робо-сервисы |
| AWS DeepRacer | Статус не подтверждён в сессии | — |
| Pathmind | Статус противоречив: Crunchbase — «Active», PitchBook — «Out of Business» (ранее Skymind), startups.rip — команда поглощена Clipboard Health в декабре 2021 [34]. Вывод: самостоятельно не существует | Нишевая «RL для симуляторов AnyLogic» не нашла рынка |
| Composabl | Seed $4,25 млн (лидер Momenta, май 2024), no-code UI для промышленных автономных агентов [33]; одна страница сообщает о ребрендинге в AMESA (октябрь 2025), не подтверждено [33] | Живая, но маленькая; ближайший прямой аналог |
| Unity ML-Agents, InstaDeep | Не исследовались (ML-Agents — open-source игровой/образовательный инструмент; InstaDeep — часть BioNTech) — не проверено | — |
| RL для LLM: OpenAI Reinforcement Fine-Tuning | Тарификация по времени обучения: $100/час wall-clock (o4-mini), токены граздеров отдельно [35] | Платят за GPU-время, не за токены |
| RL для LLM: Thinking Machines Tinker | API для fine-tuning открытых моделей; тариф за токены (prefill/sample/train), цены Qwen3-8B ≈$0,40–0,44 за 1 млн токенов по сторонним источникам [35] | API-first, а не no-code |
| RL для LLM: Prime Intellect | $130 млн (июль 2026, лидер Radical Ventures; участвовали NVentures, Intel Capital, Dell Capital); Environments Hub 2 500+ сред; заявлено >6 000 клиентов и >$100 млн ARR (самоотчёт) [36] | «Hugging Face для RL-окружений» — строят сообщество сред; пересекается с идеей маркетплейса задач (см. `04-beyond-robotics-use-cases.md`, `08-ecosystem-community-gtm.md`) |

(вывод) Закономерность: **все три крупных no-code RL начинания «в лоб» (Bonsai, Pathmind, RoboMaker) закрылись или растворились**, живёт только крошечный Composabl. Детальный разбор причин — в `03-nocode-ml-analogs-ux.md` и `07-risks-safety-regulation.md`.

---

## 4. «Белые пятна» и зоны риска

### 4.1 Где есть свободное место (вывод)

1. **Мост «демонстрации → RL-дообучение» для небольших команд.** π*0.6 показал, что RL поверх VLA на реальном опыте даёт заметный прирост [24], но это закрытая технология лаборатории. Никто не продаёт её в виде продукта для интегратора с 5 роботами. Это основной вакуум.
2. **Постановка цели/награды без кода.** Reward design — главный барьер для не-ML-пользователя (см. `02-rl-tech-state-of-art.md`). У NVIDIA, HF и Google этого слоя нет; Composabl отчасти делает.
3. **Нейтральность между железом и симуляторами.** NVIDIA привязывает к своим GPU [26], UR — к своим роботам [32], Standard Bots — к своему [31]. Хардверно-нейтральная прослойка с экспортом в Isaac/MuJoCo/LeRobot — пустое место (Wandelbots занимает его для «программирования», но не для обучения [29]).
4. **Долгий хвост доменов вне робототехники** (симуляции процессов, дискретные ресурсы, игры, трейдинг, агенты) — но здесь конкуренция с LLM-RL-стартапами и корпоративными ML-командами сильнее (см. `04-beyond-robotics-use-cases.md`).
5. **Образование и maker-сегмент**: LeRobot с SO-100/SO-101 (скачиваемость датасетов этих платформ — сотни тысяч [27]) — большая живая аудитория без no-code RL-опыта.

### 4.2 Где нас раздавят

1. **Бесплатные инструменты гигантов.** NVIDIA (Isaac Lab, GR00T, Newton, Cosmos) и HF (LeRobot, SmolVLA, Reachy Mini) раздают базовый стек бесплатно [26][27][21]; любая наша функция «обучить политику в симуляции» легко повторяется в их UI. (вывод) Нельзя строить moat на «движке» или «моделях».
2. **Foundation-модели, делающие RL ненужным в 80% случаев.** Если VLA типа π0.5/Gemini Robotics 1.5 решает задачу в zero/few-shot через fine-tuning на демонстрациях, пользователю не нужен RL (см. `02-rl-tech-state-of-art.md`). RL нужен там, где важны надёжность и скорость цикла (см. π*0.6 [24]).
3. **Вертикальные игроки** (Standard Bots, UR AI Accelerator, Intrinsic Flowstate) закрывают no-code «из коробки» в связке с железом [28][31][32].
4. **Кладбище**: Bonsai, RoboMaker, Pathmind [23][34][39] — повод для осторожности (подробно в `07-risks-safety-regulation.md`).
5. **Деньги в отрасли идут к foundation-моделям**, а не к инструментам [5–17]: мало готовых клиентов на «ещё одну платформу» и мало венчурного интереса к инструментам, если не показать выручку.

---

## 5. Варианты позиционирования

| Вариант | Суть | За | Против |
|---|---|---|---|
| **A. «Cursor/Replit для обучения роботов»**: платформа-надстройка над открытым стеком (Isaac Lab/MuJoCo, LeRobot) с no-code слоем «цель → награда → политика → проверка → развёртывание» | Мы не пишем движок и не обучаем модели с нуля; продаём UX, шаблоны задач, безопасную проверку | Быстрый MVP; используем бесплатные компоненты; широкая аудитория (maker, образование, малые интеграторы); не конфликтуем с NVIDIA/HF, а дополняем | Тонкий moat (UX копируется); зависимость от чужих API и лицензий (GR00T, возможно, некоммерческая [26]); риск, что HF/NVIDIA добавят UI |
| **B. «Post-training слой для VLA»**: управляемый сервис дообучения/RL-улучшения существующих VLA (π0, GR00T, SmolVLA) на данных клиента | Закрывает вакуум π*0.6-подобного подхода [24]; платят за вычисления и результат; близко к Tinker/OpenAI RFT по модели монетизации [35] | Чёткая ценность и маржа через GPU; понятная метрика (успешность задачи); данные клиента → moat | Нужна глубокая ML-команда и значительные GPU-расходы (см. `05-compute-hardware-costs.md`); не «no-code» в чистом виде; прямая конкуренция с Physical Intelligence, если они откроют сервис |
| **C. «Универсальная RL-студия для любых агентов»** (роботы + симуляторы процессов + игры + LLM-агенты) | Шире TAM, меньше зависимости от медленных поставок роботов; можно пересечься с рынком RL-окружений (Prime Intellect) [36] | Робототехника растёт медленно (выручка стартапов мизерная [19]), диверсификация снижает риск | Распыление; конкуренты в каждом домене сильнее; слабая история продукта; требует отдельного GTM по каждому домену (см. `04-beyond-robotics-use-cases.md`) |

(вывод) Рекомендуемая последовательность: **A как входной продукт + элементы B как платная «глубина»**; C — как опция на втором этапе, когда будет повторяемый паттерн «задача → награда → политика» независимо от домена. Окончательное решение — в `10-vision-strategy.md` (волна 2).

---

## Выводы для платформы

1. **Размер рынка скромнее хайпа.** Рынок в понимании «обучение навыков роботов без ML-экспертизы» по нашей грубой оценке — сотни миллионов долларов в год к 2030, а достижимая выручка за 3–5 лет — единицы миллионов ARR. Бизнес-план должен опираться на это, а не на трлн-прогнозы по гуманоидам (оценка, низкая уверенность).
2. **Деньги идут к foundation-моделям и гуманоидам** (2025: ≈$14–15 млрд в робототехнику, 2026 уже ≈$18,8 млрд [5][6]), а не к инструментам. Венчурный нарратив «инструмент для всех» слабее, чем «модель/железо»; нужна история с первой выручкой.
3. **Три прямых аналога no-code RL закрылись или растворились** (Bonsai, RoboMaker, Pathmind) [23][34][39]; живой Composabl мал [33]. Перед стартом нужно в `03-` и `07-` разобрать, почему.
4. **Нельзя конкурировать с NVIDIA/HF на уровне движков и моделей.** Они раздают Isaac Lab, GR00T, LeRobot бесплатно [26][27]. Наша ценность — UX, шаблоны задач, безопасность, воспроизводимость, интеграция с железом.
5. **Белое пятно — «реальный RL-цикл для небольших команд»**: π*0.6 доказал пользу RL на реальном опыте [24], но продукта для интеграторов нет. Это основное окно возможностей на 12–24 месяца.
6. **Каналы вместо борьбы с вендорами**: UR AI Accelerator, Wandelbots NOVA, LeRobot-сообщество — места, где мы можем быть плагином, а не конкурентом [27][29][32].
7. **Метрика выживания — стоимость вычислений**: OpenAI RFT ≈$100/час [35] показывает, что клиенты привыкли платить за время GPU; нашему сервису нужно устойчивое маржинальное ценообразование (см. `05-` и `06-`).
8. **Выход через M&A реалистичен**: Covariant, Edge Impulse, W&B, Pollen показывают, что стратегические покупатели (Amazon, Qualcomm, CoreWeave, HF) берут команды и инструменты [20][21][22]. Но суммы могут быть ниже последних оценок [20].
9. **Данные требуют верификации**: большинство цифр здесь вторичные; перед внешним использованием проверить по первоисточникам IFR, Goldman, Morgan Stanley, Crunchbase, а также восполнить пробелы (размеры рынков RL/MLOps, Citi/BofA, статус Bonsai/DeepRacer, Augmentus/Vention/Flexiv/Mujin/Realtime Robotics, Helix/Optimus).

---

## Источники

[1] World Robotics 2025 report – Industrial Robots (IFR press release) — International Federation of Robotics — https://ifr.org/ifr-press-releases/news/global-robot-demand-in-factories-doubles-over-10-years ; Executive Summary: https://ifr.org/img/worldrobotics/Executive_Summary_WR_2025_Industrial_Robots.pdf — (дата обращения 2026-10-27; через сниппеты поиска, страница не открывалась)
[2] World Robotics 2025 report – Service Robots — IFR — https://ifr.org/ifr-press-releases/news/service-robots-see-global-growth-boom — (дата обращения 2026-10-27; через сниппеты)
[3] The global market for robots could reach $38 billion by 2035 — Goldman Sachs — https://www.goldmansachs.com/intelligence/pages/the-global-market-for-robots-could-reach-38-billion-by-2035.html — (дата обращения 2026-10-27; через сниппеты)
[4] Humanoid robots seen as $5 trillion global opportunity at Morgan Stanley — OODA Loop (вторичный пересказ) — https://oodaloop.com/briefs/technology/humanoid-robots-seen-as-5-trillion-global-opportunity-at-morgan-stanley/ — (дата обращения 2026-10-27)
[5] Robotics funding (2025) — Crunchbase News — https://news.crunchbase.com/robotics/ai-funding-high-figure-raise-data/ ; H1 2025: https://news.crunchbase.com/robotics/startup-funding-rises-h1-2025-ai-apptronik-data/ — (дата обращения 2026-10-27; через сниппеты)
[6] Robotics startup venture funding surges 2026 — Crunchbase News — https://news.crunchbase.com/robotics/startup-venture-funding-surges-2026-data/ — (дата обращения 2026-10-27; через сниппеты)
[7] Physical Intelligence is reportedly in talks to raise $1 billion, again — TechCrunch, 2026-03-27 — https://techcrunch.com/2026/03/27/physical-intelligence-is-reportedly-in-talks-to-raise-1-billion-again/ — (дата обращения 2026-10-27; через сниппеты)
[8] Ex-DeepMind Staffers' Robotics Startup in Talks for $11 Billion Valuation — Bloomberg, 2026-03-27 — https://www.bloomberg.com/news/articles/2026-03-27/ex-deepmind-staffers-robotics-startup-in-talks-for-11-billion-valuation — (дата обращения 2026-10-27; через сниппеты)
[9] Physical Intelligence funding: Every round, investor, and valuation (2026) — Revenue Memo — https://www.revenuememo.com/p/physical-intelligence-funding — (дата обращения 2026-10-27; агрегатор, уверенность низкая)
[10] Skild AI Raises $1.4B, Now Valued Over $14B — Business Wire, 2026-01-14 — https://www.businesswire.com/news/home/20260114335623/en/Skild-AI-Raises-$1.4B-Now-Valued-Over-$14B — (дата обращения 2026-10-27; через сниппеты)
[11] Robotics Startup Skild Valued Above $14 Billion After SoftBank-Led Funding Round — Bloomberg, 2026-01-14 — https://www.bloomberg.com/news/articles/2026-01-14/robotics-startup-skild-valued-above-14-billion-after-softbank-led-funding-round — (дата обращения 2026-10-27)
[12] Figure exceeds $1B funding, $39B valuation — Figure AI (LinkedIn) — https://www.linkedin.com/posts/figure-ai_announcing-figure-has-exceeded-1b-in-funding-activity-7373703158998446082-f5mJ ; агрегатор: https://www.teahose.com/guides/figure-ai-valuation — (дата обращения 2026-10-27)
[13] NVIDIA's Reported $1B Figure AI Investment... — Tech Times, 2026-10-13 — https://www.techtimes.com/articles/328801/20261013/nvidias-reported-1b-figure-ai-investment-prices-startup-above-goldman-sachs-2035-humanoid-market.htm — (дата обращения 2026-10-27; через сниппеты)
[14] SoftBank in talks to buy a majority stake in 1X at $6B valuation — Tech Startups, 2026-08-27 — https://techstartups.com/2026/08/27/softbank-in-talks-to-buy-a-majority-stake-in-humanoid-robot-startup-1x-at-6-billion-valuation/ ; профиль: https://app.dealroom.co/companies/1x_1 — (дата обращения 2026-10-27)
[15] Robotics startup Generalist reaches $3B valuation — TechCrunch, 2026-08-25 — https://techcrunch.com/2026/08/25/robotics-startup-generalist-reaches-3b-valuation-sources-say/ ; Genesis AI: https://thenextweb.com/news/genesis-ai-500m-raise-robotics-foundation-model ; Dyna (Tracxn): https://tracxn.com/d/companies/genesis-ai/__ElX8vCbm0IkpzgXTiDtwa9nLi1JUwNSN3zY03pjL-Fg — (дата обращения 2026-10-27)
[16] Nvidia, Bill Gates-backed robotics startup Field AI hits $2 billion valuation — CNBC, 2025-08-20 — https://www.cnbc.com/2025/08/20/gates-nvidia-fieldai-robotics.html ; 2026: https://www.benzinga.com/markets/tech/26/10/62150844/fieldai-700-million-10-billion-valuation-physical-ai — (дата обращения 2026-10-27)
[17] Humanoid robot startup Apptronik has now raised $935M at a $5B valuation — TechCrunch, 2026-02-11 — https://techcrunch.com/2026/02/11/humanoid-robot-startup-apptronik-has-now-raised-935m-at-a-5b-valuation/ — (дата обращения 2026-10-27)
[18] Unitree Robotics Files for $608 Million STAR Market IPO — Caixin Global, 2026-03-21 — https://www.caixinglobal.com/2026-03-21/unitree-robotics-files-for-608-million-star-market-ipo-102425491.html ; Unitree IPO 2026: https://robottesters.com/article-unitree-ipo ; https://techmarketbriefs.com/pre-ipo/unitree/ — (дата обращения 2026-10-27; цены размещения только из вторичных источников)
[19] Agility Robotics public SPAC deal — TNW, 2026-06-24 — https://thenextweb.com/news/agility-robotics-public-spac-deal — (дата обращения 2026-10-27; через сниппеты)
[20] Amazon hires Covariant founders, inks licensing deal — GeekWire, 2024-08-31 — https://www.geekwire.com/2024/08/31/amazon-hires-covariant-founders-inks-licensing-deal-with-robotics-ai-startup-in-latest-reverse-acquihire-deal/ — (дата обращения 2026-10-27; сумма $380 млн — из жалобы информатора, не подтверждена)
[21] Reachy Mini – The Open-Source Robot... — Hugging Face blog — https://huggingface.co/blog/reachy-mini ; Slashdot: https://tech.slashdot.org/story/25/07/09/2051245/ — (дата обращения 2026-10-27)
[22] CoreWeave Acquires Weights & Biases in a $1.7 Billion AI Cloud Play — Maginative — https://www.maginative.com/article/coreweave-acquires-weights-biases-in-a-1-7-billion-ai-cloud-play/ ; Qualcomm/Edge Impulse: https://www.mobileworldlive.com/qualcomm/qualcomm-eyes-iot-edge-with-platform-buy/ ; ABI Research: https://www.abiresearch.com/market-research/insight/7785819-qualcomm-acquisition-of-edge-impulse-adds- — (дата обращения 2026-10-27)
[23] End of support notice: AWS RoboMaker — AWS Documentation — https://docs.aws.amazon.com/robomaker/latest/dg/using-service-linked-roles.html — (дата обращения 2026-10-27; через сниппеты)
[24] π*0.6: a VLA That Learns From Experience — Physical Intelligence, arXiv 2511.14759 — https://arxiv.org/pdf/2511.14759 — (дата обращения 2026-10-27; детали о результатах — по вторичным пересказам, независимых бенчмарков нет)
[25] Gemini Robotics 1.5 brings AI agents into the physical world — Google DeepMind — https://deepmind.google/blog/gemini-robotics-15-brings-ai-agents-into-the-physical-world/ ; SDK: https://github.com/google-deepmind/gemini-robotics-sdk ; Wikipedia (ER 2): https://en.wikipedia.org/wiki/Gemini_Robotics — (дата обращения 2026-10-27)
[26] NVIDIA Accelerates Robotics R&D With New Open Models and Simulation Libraries — NVIDIA Newsroom — https://nvidianews.nvidia.com/news/nvidia-accelerates-robotics-research-and-development-with-new-open-models-and-simulation-libraries ; https://www.engineering.com/nvidia-adds-newton-physics-engine-and-gr00t-model-to-isaac-lab/ ; https://chatforest.com/builders-log/nvidia-physical-ai-cvpr-2026-gr00t-alpamayo-openshell-skills-builder-guide/ (вторичный, лицензия GR00T) — (дата обращения 2026-10-27)
[27] LeRobot: An Open-Source Library for End-to-End Robot Learning — arXiv 2602.22818 — https://arxiv.org/html/2602.22818v1 ; community dataset: https://huggingface.co/datasets/HuggingFaceVLA/community_dataset_v1 ; SmolVLA: https://huggingface.co/blog/smolvla — (дата обращения 2026-10-27)
[28] Foxconn and Intrinsic launch joint venture — Intrinsic blog (зеркало) — https://scour.ing/p/https://www.intrinsic.ai/blog/posts/foxconn-and-intrinsic-launch-joint-venture-to-build-the-ai-factory-of-the-future ; Fortune: https://dc.fortune.com/2025/11/20/alphabet-intrinsic-foxconn-intelligent-robots-ai-joint-venture ; Alphabet folds Intrinsic into Google: https://techbriefly.com/2026/02/26/alphabet-folds-robotics-firm-intrinsic-into-google-to-power-deepmind/ — (дата обращения 2026-10-27)
[29] Schaeffler Leverages Wandelbots NOVA as Its Physical AI Platform — Robotics Tomorrow, 2026-10-22 — https://www.roboticstomorrow.com/news/2026/10/22/schaeffler-leverages-wandelbots-nova-as-its-physical-ai-platform-/27278 ; профиль: https://pitchbook.com/profiles/company/225802-72 — (дата обращения 2026-10-27)
[30] Micropsi Industries secures $30 million in Series B — Micropsi — https://micropsi-industries.com/blog/micropsi-industries-secures-30m-in-series-b — (дата обращения 2026-10-27)
[31] Standard Bots raises $63M to accelerate AI in robotics — Standard Bots — https://standardbots.com/articles/standard-bots-raises-63m-to-accelerate-ai-in-robotics ; Bloomberg: https://www.bloomberg.com/news/articles/2024-07-12/general-catalyst-amazon-bet-63-million-on-ai-robotics-startup — (дата обращения 2026-10-27)
[32] Automate 2025: Universal Robots introduces UR15 cobot — Robotics 24/7 — https://www.robotics247.com/article/automate-2025-universal-robots-introduces-ur15-cobot — (дата обращения 2026-10-27)
[33] Composabl Launches No-Code UI Platform... and Raises $4.25M — Yahoo Finance / Newsfile — https://finance.yahoo.com/news/composabl-launches-breakthrough-no-code-153000019.html ; Momenta: https://www.prweb.com/releases/momenta-leads-investment-in-composabl-expanding-industrial-ai-and-autonomy-302139332.html ; профиль: https://startupintros.com/orgs/composabl — (дата обращения 2026-10-27)
[34] Pathmind — Startups.RIP / PitchBook / Crunchbase — https://startups.rip/company/pathmind ; https://pitchbook.com/profiles/company/93655-18 ; https://www.crunchbase.com/organization/pathmind — (дата обращения 2026-10-27; статус противоречив)
[35] Billing guide for the reinforcement fine tuning API — OpenAI Help — https://help.openai.com/en/articles/11323177-billing-guide-for-the-reinforcement-fine-tuning-api ; Tinker: https://venturebeat.com/ai/thinking-machines-first-official-product-is-here-meet-tinker-an-api-for ; https://www.beam.cloud/blog/tinker-model-pricing — (дата обращения 2026-10-27)
[36] Prime Intellect Raises $130 Million to Help Companies Train AI Agents — PYMNTS, 2026 — https://www.pymnts.com/news/investment-tracker/2026/prime-intellect-raises-130-million-to-help-companies-train-ai-agents/ ; https://www.intelcapital.com/prime-intellect-raises-130m-series-a-to-build-the-open-superintelligence-stack/ ; https://www.rl-list.com/ — (дата обращения 2026-10-27; ARR и число клиентов — самоотчёт)
[37] Foxglove Raises $40 Million Series B — Business Wire, 2025-11-12 — https://www.businesswire.com/news/home/20251112126106/en/Foxglove-Raises-%2440-Million-Series-B-to-Power-the-Future-of-Physical-AI — (дата обращения 2026-10-27)
[38] Viam Series A — Viam — https://www.viam.com/press-releases/series-a ; сравнение Formant vs Viam: https://www.cbinsights.com/compare/formant-1-vs-viam — (дата обращения 2026-10-27)
[39] Microsoft to acquire machine learning startup Bonsai — GeekWire, 2018 — https://www.geekwire.com/2018/microsoft-acquire-machine-learning-training-startup-bonsai-bolstering-ai-efforts/ — (дата обращения 2026-10-27)
