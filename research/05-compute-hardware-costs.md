# 05. Ресурсы и затраты: GPU, железо роботов, данные, команда, бюджет MVP

> Автор: агент «Аналитик ресурсов и затрат» · Дата: 2026-10-27 · Прочитанные файлы research/: README.md (других файлов волны 1 на момент записи в папке нет — перекрёстные ссылки даны по плану из README и будут актуальны после их появления)

## 0. Как читать этот файл и ограничения ресёрча

- Цель: показать **все ресурсы**, которые понадобятся платформе: вычисления, железо, данные, люди, лицензии и «прочее», и свести их в три бюджетных сценария.
- Метки: факт — с `[n]`; `(оценка)` — моя прикидка; `(вывод)` — рекомендация. Уверенность: `[уверенность: высокая/средняя/низкая]`.
- **Честные ограничения (важно):**
  1. Лимит WebSearch в этой сессии исчерпался примерно на половине запланированных запросов. Не успели проверить: прайсы Nebius, Modal, GCP, Azure, Vast.ai, L40S; GPU-часы GRPO для LLM; детали лицензий Isaac Sim/Omniverse Enterprise, Gemini Robotics; стоимость SOC 2, юристов, страхования; зарплаты в Европе и удалённо. Эти места помечены как **пробелы**, цифры там — `(оценка)` без источника.
  2. WebFetch в этой среде открывал только github.com и raw-GitHub. Официальные страницы с прайсами (aws.amazon.com, lambda.ai, runpod.io, nvidia.com) **недоступны**, поэтому цены GPU и роботов — из вторичных обзоров и ритейлеров. Источники сильно расходятся. Все цены нужно сверить с официальными страницами перед использованием в инвестиционных материалах.
  3. Документация, прочитанная напрямую (GitHub): openpi, LeRobot Hardware Guide, Isaac-GR00T, SO-ARM100, Isaac Sim, MuJoCo Playground — это самые надёжные источники здесь.

---

## 1. Вычисления (GPU): цены 2026 и тренд

### 1.1. Сводная таблица цен за GPU-час (USD)

Все данные — вторичные обзоры, не официальные прайсы. Где источники расходятся, показан диапазон.

| Провайдер / тип | H100 | H200 | B200 | RTX 4090 | RTX 5090 | Источник / примечание |
|---|---|---|---|---|---|---|
| Lambda, on-demand (8-GPU SXM) | $3.99 | $4.49 | $6.69–6.99 | — | — | [1] [уверенность: средняя] |
| CoreWeave, on-demand (за GPU из 8-GPU ноды) | $6.16 (нода $49.24) | $6.31 (нода $50.44) | $8.60 (нода $68.80); spot-нода $34.11 | — | — | [1]; старый CloudZero даёт для B200 ~$5.50 [2] — противоречие [уверенность: средняя] |
| AWS p5 (H100), on-demand после снижения июня 2025 | ~$6.88 (p5.48xlarge $55.04/ч) [11] **или** ~$3.90 [3] | p5en: цена сопоставима с H200 | — | — | — | Противоречие источников; AWS подтверждает снижение: -44% для P5, -25% для P5en с 1.06.2025 [10]. Мне кажется, $6.88 правдоподобнее [11] (вывод) [уверенность: низкая] |
| AWS Capacity Blocks (с 1.07.2026) | $5.19 (P5) | $6.87 (P5en) | — | — | — | [13] [уверенность: средняя] |
| AWS Savings Plan 3 года (P5) | ~$3.10 | — | — | — | — | [12] [уверенность: низкая] |
| RunPod Community Cloud | $2.69 (SXM), $1.99 (PCIe) | — | $5.98 | $0.34 | $0.69 | [5] [8] [уверенность: средняя] |
| RunPod Secure Cloud | $3.49 (SXM), $2.89 (PCIe) | — | $6.79 | $0.69–0.74 | ~$1.22 (on-demand по другому обзору) [7] | [6] [7]; [6] сообщает о повышении Secure-цен в сентябре 2026, Community без изменений (одиночный источник) |
| Spheron (маркетплейс) | $2.65 on-demand / $2.21 spot | — | $10.15 on-demand / $5.25 spot | — | — | [4] [уверенность: низкая] |
| Thunder Compute (окт. 2026) | $3.99 | — | — | — | — | [9] |
| Hyperbolic (конец авг. 2026) | $3.19 | — | — | — | — | [34] |

Пробелы: Nebius, Modal, GCP, Azure, Vast.ai, L40S — **не проверены** (исчерпан лимит поиска). (вывод) их нужно добавить перед финальной версией плана.

Диапазон «рыночной» цены H100 на середину 2026: от ~$2.0 до ~$12.3 за GPU-час в зависимости от провайдера [34] (дата данных — июль 2026). Для расчётов ниже я использую **$3.0/ч за H100** и **$0.5/ч за RTX 4090** (оценка, основана на таблице).

### 1.2. Тренд цен 2023 → 2026

| Период | Что известно | Источник |
|---|---|---|
| 2023–2024 | Подтверждённых источников по 2023 г. не найдено. Один вендорский обзор говорит о пике $8–10 за H100-час к Q4 2024 | [34] (cyfuture KB) [уверенность: низкая] |
| 2025 | Падение до ~$2.85–3.50 в Q3–Q4 2025; AWS снизил on-demand на 44% (P5) в июне 2025 | [34], [10] |
| Окт. 2025 → март 2026 | 1-летний контракт на H100: $1.70 → $2.35/ч (+~40% за 6 месяцев) по индексу SemiAnalysis; on-demand ёмкость, по сообщению, распродана по всем типам GPU | [34] (SemiAnalysis через itiger) [уверенность: средняя] |
| Лето 2026 | Hyperbolic H100: рост с ~$1.50 до $3.19 за ~10 недель | [34] |

**Вывод по тренду (вывод):** после падения 2025 года цены 2026 года **растут**, а доступность — проблема. Для бизнес-плана нельзя закладывать «GPU дешевеют каждый год» — закладываем плоскую цену и риск скачка +30–50% (оценка). Сравните с рисками в `07-risks-safety-regulation.md`.

### 1.3. On-demand vs reserved vs spot

| Режим | Типичная скидка к on-demand | Когда подходит платформе |
|---|---|---|
| On-demand | база | интерактивные превью, короткие запуски |
| Spot / interruptible | CoreWeave B200 spot $34.11 против $68.80 за ноду = -50% [1]; Spheron H100 -17%, B200 -48% [4] | основная масса обучения RL и fine-tune (чекпоинты обязательны) |
| Reserved / Savings Plan | «до 60%» [3-обзоры]; AWS 3 года ~$3.10 против ~$6.88 on-demand [11] [12] | базовая нагрузка после появления стабильного спроса |

### 1.4. Покупка своего железа и окупаемость

| Позиция | Цена | Источник |
|---|---|---|
| DGX B200 (8×B200) | ~$562K (реселлер, сент. 2026) | [33] [уверенность: средняя] |
| HGX B200 8-GPU сервер (Supermicro, Newegg) | $384K–394K | [33] |
| Lenovo SR680a V3, 8×B200 | $550K (июнь 2026) | [33] |
| Новый HGX B200 узел (окт. 2026, отчёт по стойкам) | $360K–470K | [33] |
| H100 за карту (по обзору) | $27K–40K | [33] (название статьи intuitionlabs) |

Простая окупаемость (оценка, расчёт мой): сервер 8×B200 ≈ $400K + ~15–25% на сеть, хостинг, электричество в первый год. Аренда эквивалента на Lambda: 8 × $6.69 = $53.5/ч → $469K в год при 100% загрузке [1]. То есть окупаемость ~10–12 месяцев **только при загрузке близкой к 100%**; при 50% — ~2 года и больше, при этом железо устаревает за 2–3 года (оценка). Для pre-seed/seed покупка такого сервера **не оправдана** (вывод): у платформы нагрузка будет рваной (пики запусков пользователей), и она критична к доступности.

Реалистичная альтернатива для ранней стадии: 1–2 рабочие станции на RTX 4090/5090 (оценка: $5–8K за станцию, источник цены не найден) для разработки, QA и бесплатных/демо-запусков, а всё тяжёлое — в spot-облако.

**Важное для архитектуры:** Isaac Sim требует GPU с RT-ядрами: минимум RTX 4080 (локально) или A40/L20 (датацентр), рекомендуется L40S [35]. (вывод) Для Isaac Sim в облаке нужны карты класса L40S/RTX PRO 6000, а не «голые» H100/B200 — это влияет на выбор провайдеров. Для MuJoCo Playground (JAX/MJX) достаточно любой CUDA-12 GPU [36].

---

## 2. Сколько вычислений нужно на типичные задачи

### 2.1. Данные по вычислениям (первичные и вторичные)

| Задача | Данные | Источник |
|---|---|---|
| RL локомоции, Isaac Lab, Humanoid, RSL-RL, 4096 env, 500 итераций (65.5M шагов), одна RTX 4090 | **198 с (~3.3 мин)** | [18] [уверенность: высокая, официальный бенчмарк, но задача лёгкая] |
| Humanoid Fourier GR3, RSL-RL-based, RTX 4090 | ~6 с/итерация, ~8 ч на 5000 итераций | [19] [уверенность: средняя, вендор] |
| MuJoCo Playground | «политики за минуты на одной GPU»; локомоция и манипуляция, раньше требовавшие дни на multi-host, теперь минуты–часы | [20] [уверенность: высокая по утверждению авторов, конкретных таблиц времени не получил] |
| ACT (imitation), ~50 эпизодов, 5 эпох | RTX 4090/3090: 30–60 мин; L4/A10G: 1–2 ч | [22] [уверенность: средняя, ±50%] |
| Diffusion Policy, то же | RTX 4090: 2–4 ч; 4×H100: 30–60 мин | [22] |
| SmolVLA | VRAM 10–16 ГБ; L4/A10G 3–6 ч; A100 40GB 1–2 ч; 4×H100 1–2 ч | [22]; согласуется с [23] |
| π0 / π0.5 | VRAM 24–40 ГБ; A100 40GB 4–8 ч | [22] |
| Измеренный бенчмарк 4×H100, 5000 шагов, batch 32 | Diffusion 16 мин; SmolVLA 28 мин; **π0.5 — 3 ч 41 мин** (≈ 14.7 H100-часа) | [22] |
| openpi (π0, π0-FAST, π0.5) требования к одной GPU | инференс > 8 ГБ (RTX 4090); LoRA fine-tune > 22.5 ГБ (RTX 4090); полный fine-tune > 70 ГБ (A100 80GB / H100) | [21] [уверенность: высокая] |
| GR00T N1.7 (3B) | fine-tune: 1+ GPU с 40+ ГБ VRAM; рекомендуются H100/L40; A6000 работает медленнее; «несколько тысяч шагов» | [25] [24] |
| OpenVLA | полный fine-tune: 8×A100, 5–15 ч на задачу; LoRA: 10–15 ч на одной A100 | [26] [уверенность: высокая] |

Пробел: GRPO/RL-fine-tuning LLM (7B/70B) — **источников не найдено** (лимит поиска). Ниже — только `(оценка)`.

### 2.2. Перевод в доллары: «типичная задача пользователя»

Допущения (оценка): RTX 4090 = $0.5/ч (диапазон $0.34–0.74 [5] [6]); A100 = $1.8/ч (источник цены A100 не найден, оценка); H100 = $3.0/ч (диапазон $2.2–4.0). Накладные расходы (запуск контейнера, загрузка данных, превью, неудачные запуски) +30% (оценка).

| # | Тип задачи | Вычисления на попытку | Попыток у новичка | Стоимость задачи (оценка) | Уверенность |
|---|---|---|---|---|---|
| 1 | **Локомоция RL** (Go2/G1 в Isaac Lab или MJX): подбор reward, 2–4k env | 0.1–4 ч на 4090 [18] [19] | 5–15 | **$5–45**, центр ~$20 | средняя (разброс 10×) |
| 2 | **Манипуляция, imitation learning** (ACT/Diffusion, SO-101, ~50 эпизодов) | ACT 0.5–1 ч, Diffusion 2–4 ч на 4090 [22] | 2–4 | **$1–10**, центр ~$5 | средняя |
| 3а | **VLA fine-tune лёгкий** (SmolVLA) | 1–2 ч A100 [22] | 2–3 | **$5–15** | средняя |
| 3б | **VLA fine-tune большой** (π0.5, 5000 шагов) | A100 4–8 ч [22] или ~14.7 H100-ч [22] | 2–3 | **$15–130**, центр ~$60 | средняя |
| 3в | OpenVLA LoRA | 10–15 A100-ч [26] | 1–2 | $20–55 | средняя |
| 4а | **RL fine-tune LLM-агента, GRPO, модель 7B** | (оценка, без источника) 50–200 H100-ч | 1–3 | **$150–1800**, центр ~$400 | низкая |
| 4б | GRPO, модель 70B | (оценка, без источника) 1000–5000 H100-ч | 1 | $3000–15000+ | низкая |

(Расчёты: пример 3б — 14.7 ч × $3.0 = $44 за прогон; 2–3 прогона с накладными → $60–130. Пример 1 — 10 прогонов × 1 ч × $0.5 × 1.3 ≈ $6.5; верхняя граница 15 × 4 ч × $0.74 × 1.3 ≈ $58, округлено до $45 с учётом, что верхняя оценка встречается редко.)

**Дополнительно:**
- **Инференс политики в облаке** (для демо «робот в браузере»): VLA > 8 ГБ [21], то есть одна RTX 4090 за $0.34–0.74/ч; при 24/7 это ~$250–530/мес на один активный стенд (расчёт мой). В production модель должна работать на стороне пользователя (edge).
- **Рендеринг симуляции:** видео-превью обучения и онлайн-просмотр в Isaac Sim требуют RT-GPU (L40S-класс) [35]. Стоимость L40S не проверена (пробел). Для MJX — рендер дешёвый, есть «MJWarp Batch Renderer» для vision-based сред [36].
- **Edge-инференс на роботе пользователя:** Jetson AGX Thor — 2070 FP4 TFLOPS, 128 ГБ, 40–130 Вт, запуск по $3,499 (10+ штук $3,429) [17]; после повышения цен NVIDIA в июле 2026, по одному источнику, devkit Thor $5,499, AGX Orin devkit $1,999→$3,499, Orin Nano Super $249→$399 [17] [уверенность: низкая — одиночный источник hwbusters, подтверждение: заголовок CNX «до +101%»]. Для SO-101-пользователей инференс идёт на ноутбуке/ПК, Jetson нужен для автономных роботов.

**(вывод)** Типичная задача пользователя стоит платформе **$5–60** на ручной/low-tech уровне (локомоция, IL, SmolVLA, π0.5), а LLM-RL — $150–1800 (с большой неопределённостью). Это важно для ценообразования (см. `06-business-models-pricing.md`): базовый план, включающий «N часов GPU», безопасен для IL/локомоции, но **опасен для VLA и LLM-RL** — нужен лимит или кредиты. Технические детали методов — в `02-rl-tech-state-of-art.md`.

---

## 3. Железо роботов и оснастка (цены 2025–2026)

Цены сильно разнятся по источникам и ритейлерам; ниже — диапазон. Все цены — на конец 2026 г. по вторичным источникам.

| Устройство | Цена, USD | Заметка | Источник |
|---|---|---|---|
| SO-101 (SO-ARM101), комплект 2 руки (leader+follower) | ~$220–250 (Seeed / AliExpress; $247 по акции при $399 прайсе); без 3D-печатных деталей, БП | BOM по репозиторию: $229.88 за обе руки (US), $121.94 одна follower-рука | [15] [16] [уверенность: высокая] |
| Koch, LeKiwi (мобильная база SO-101), Reachy Mini | цены не найдены; LeKiwi — «самый дешёвый вариант — проводной» | Reachy Mini: Lite (к ПК) и Wireless (RPi CM4), сборка 2–3 ч, цену на странице не нашёл | LeKiwi/Reachy: GitHub [неверифицировано по цене] |
| Unitree Go2 | Air ~$1,600; Pro $2,800–3,790; X $4,500 | EDU — существенно дороже | [14] |
| Unitree R1 | ~$6,870 (Air) – $8,990 (Basic); ранее $4,900 | | [14] |
| Unitree G1 | Basic $13,500 (офиц.) – $17,990 (US-ритейл); Pro $28,950; в EDU-конфигурациях до ~$83,900 | Базовая G1 не программируется; для RL/LeRobot нужен EDU | [14] [уверенность: средняя] |
| Unitree H2 | $29,900–41,000 (разные источники) | | [14] [уверенность: низкая] |
| ALOHA Stationary AI (Trossen) | $23,996–29,999 (30,796 с ноутбуком) | | [27] |
| Mobile AI (Trossen) | $33,696 с ноутбуком | исходный Mobile ALOHA: бюджет ~$32,000 | [27] |
| Franka FR3 | $25,000–39,000; ~€30,200 (с НДС) у европейского реселлера | | [28] [уверенность: низкая] |
| UR5e | $30,000–45,000 (официальных цен нет) | | [28] |
| UFactory xArm 6 | $8,000–12,650 | | [28] |
| Hello Robot Stretch 3 | цена не найдена | пробел | — |
| 1X NEO | $20,000 или $499/мес; поставки в США 2H 2026 | ранняя эксплуатация с удалённой телеоперацией; для платформы — не dev-платформа | [29] |
| Booster, K-Scale, Figure | не искал/не нашёл | пробел | — |
| Meta Quest 3 (телеоперация), Intel RealSense, рабочая станция | **источник не найден** | (оценка) Quest 3 ~$500, RealSense D435-класса ~$300–400, станция с 4090/5090 $5–8K | — |

### Сколько стоит «зоопарк» для QA и демо платформы

| Уровень | Состав | Итого (оценка, по таблице выше) |
|---|---|---|
| **Бронза (pre-seed)** | 3–4 пары SO-101 (~$250 каждая) + мобильная база LeKiwi + камеры + Quest 3 + 1 станция с RTX 4090/5090 + Jetson Orin | **~$12–18K** |
| **Серебро (seed)** | Бронза + Go2 Pro ($3–4K) + Unitree R1 ($7–9K) + G1 EDU/Pro ($29K+) + xArm 6 ($8–13K) + Jetson Thor ($3.5–5.5K) + ALOHA Stationary ($24–31K) + Franka FR3 ($25–39K) | **~$110–150K** |
| **Золото (Series A)** | Серебро + Mobile ALOHA ($33.7K) + UR5e ($30–45K) + H2 ($30–41K) + 2–3 запасных комплекта, ремонт, таможня/тарифы, стойки, motion capture | **~$300–400K** |

(Суммы — мой расчёт, диапазоны широкие из-за расхождения цен [уверенность: низкая–средняя].)

**(вывод)** Для no-code платформы ключевая ставка — **«дешёвые» роботы** (SO-101, Go2, R1): они закрывают 80% демо-сценариев за <$20K. Дорогая гуманоидная техника нужна для маркетинга/партнёрств, а не для ежедневной работы. Экосистему железа и партнёрство с вендорами смотрите в `08-ecosystem-community-gtm.md`. LeRobot нативно поддерживает SO101, LeKiwi, Unitree G1, Koch, Reachy2 и др. [38] — это снижает стоимость интеграции.

---

## 4. Данные

### 4.1. Стоимость сбора демонстраций

| Параметр | Значение | Источник |
|---|---|---|
| Телеоперация bimanual: сырой час | $28–60 (амортизация rig $4–9 + оператор $18–38 + QA) | [30] (Dexset, вендор — самореклама, [уверенность: низкая–средняя]) |
| Выход оператора | новичок 8–12 пригодных эпизодов/ч; опытный 25–40 за 2–3 недели | [30] |
| Брак по QA | 10–30% | [30] |
| Аннотация | +$8–25 за час | [30] |
| Egocentric-съёмка (nxted) | от $35 за пригодный час, минимум 500 часов | [30] (robosignal-агрегатор) |
| Альтернатива в исследованиях | 84 демо/ч телеоперацией против 248+ демо/ч у системы DexViTac | [30] |

**Часов на навык (оценка):** простая задача для ACT/SmolVLA — ~50 эпизодов (по ориентиру LeRobot: ~45k кадров, ≈ 25 мин записи при 30 fps [22]) → при 10–30 эпизодах/час это **2–5 часов работы** оператора, то есть $60–300 при покупке у вендора (по ставкам [30]) или несколько часов времени самого пользователя. Для обобщающей политики (VLA, много сцен) нужны сотни–тысячи эпизодов, т. е. сотни часов (оценка, источник не найден). Для no-code платформы это главный «скрытый» ресурс **пользователя**: время и железо для сбора данных. (вывод) Платформа должна минимизировать число демонстраций (sim-генерация, шаблоны, аугментации) — см. `02-rl-tech-state-of-art.md`.

### 4.2. Открытые датасеты (для pre-training и бесплатных стартовых моделей)

Размеры не удалось подтвердить через доступные источники (страницы GitHub не содержат статистики). Из общих знаний, **не проверено в этой сессии** [уверенность: низкая]: Open X-Embodiment — порядка миллиона траекторий и десятков датасетов от десятков организаций; DROID — десятки тысяч траекторий на ~350 ч, собран на 18 идентичных платформах (число платформ подтверждено [38]); AgiBot World — крупнейший промышленный датасет. LeRobotDataset: видео MP4 + Parquet, тысячи датасетов на Hugging Face Hub [38]. Подробности об экосистеме данных — в `08-ecosystem-community-gtm.md`.

### 4.3. Хранение

| Хранилище | Цена хранения | Egress | Источник |
|---|---|---|---|
| Cloudflare R2 | $0.015/ГБ/мес | $0 | [31] |
| AWS S3 Standard | ~$0.023/ГБ/мес | $0.09/ГБ (первые 10 ТБ) | [31] |
| Backblaze B2 | ~$0.006–0.007/ГБ/мес | $0.01/ГБ или бесплатно через Cloudflare (Bandwidth Alliance) | [31]; B2 egress у источников расходится |

Пример (мой расчёт): 10 ТБ видео-данных пользователей — R2 ≈ $150/мес; S3 ≈ $230/мес + 10 ТБ egress ≈ $900 (разово). Для платформы, где данные уходят на GPU-провайдеров вне AWS, **R2 или B2 предпочтительнее S3** из-за egress (вывод).

---

## 5. Команда

### 5.1. Состав

| Роль | MVP (6–12 мес.) | Series A (24 мес.) | Заметки |
|---|---|---|---|
| Основатели / продукт | 2 | 2–3 | CEO/продукт + технический сооснователь |
| RL / robot learning research engineer | 1–2 | 4–6 | самый дефицитный профиль |
| ML infra / DevOps (кластеры, очереди, спот) | 1 | 3–4 | |
| Full-stack (no-code UI, визуальный редактор) | 1–2 | 5–6 | |
| Robotics hardware / sim engineer | 0.5–1 (контрактор) | 2–3 | интеграции роботов, QA |
| Дизайнер / UX | 0.5 | 1–2 | no-code = UX критичен, см. `03-nocode-ml-analogs-ux.md` |
| DevRel / community | 0–1 | 2–3 | см. `08-ecosystem-community-gtm.md` |
| Sales / customer success | 0 | 2–3 | |
| Security / compliance | 0 | 1 | SOC 2 |
| **Итого** | **5–8** | **22–30** | |

### 5.2. Зарплаты (США) — что удалось найти

| Источник | Данные |
|---|---|
| Levels.fyi, ML Engineer, США | медиана total comp **$280K** (обновлено 15.10.2026), смещено к крупным компаниям и лабораториям [32] |
| Glassdoor (по тому же обзору) | средняя для ML Engineer ~$164.7K [32] |
| Robotics engineer, KORE1 | mid $150–205K; senior $205–300K; humanoid/foundation-model $280–475K [32] |
| Robot learning / VLA (там же) | mid $185–240K; senior $250–345K; principal/staff $360–475K [32] |

[уверенность: средняя–низкая; рекрутинговые блоги, а не первичные данные.] Источников по **RL research engineer** отдельно, а также по Европе и удалённо из дешёвых регионов — **не найдено** (пробел).

Мои оценки (оценка, без источника) для бюджета (годовой cash, без equity):

| Роль | США | Европа (западная) | Удалённо, дешёвые регионы (Восточная Европа, Латинская Америка, Индия) |
|---|---|---|---|
| RL / robot learning engineer | $200–300K | €100–160K | $70–130K |
| ML infra | $180–260K | €90–140K | $60–110K |
| Full-stack | $150–220K | €70–120K | $40–90K |
| Robotics hardware engineer | $140–200K | €70–110K | $40–80K |
| DevRel | $130–190K | €60–100K | $40–80K |

Полная стоимость сотрудника (оценка): ×1.2–1.3 к cash (налоги, бенефиты, оборудование).

### 5.3. Сложность найма

(оценка/вывод, основана на разбросе зарплат [32]): профессионалы по RL+sim2real+железу — единицы на рынке, конкурируют с humanoid-стартапами и лабораториями, платящими до $475K [32]. Для MVP реалистична стратегия: основатель с RL-бэкграундом + 1–2 senior-инженера удалённо + контракторы на железо; найм по принципу «сильный генералист в ML, который выучит RL» дешевле. Смотрите также риски в `07-risks-safety-regulation.md`.

---

## 6. Софт, лицензии, юридическое

| Пункт | Что известно | Источник | Вывод |
|---|---|---|---|
| **Isaac Sim** | Репозиторий под Apache-2.0, но при сборке нужно принять Omniverse Licensing Terms; условия коммерческого использования страница не описывает | [35] | Нужна юридическая проверка Omniverse terms и условий хостинга Isaac Sim как сервиса (SaaS) — **ключевой риск** (пробел) |
| Isaac Lab | (из общих знаний, не проверено) открытый, BSD-3 | — | уточнить |
| **MuJoCo / MuJoCo Playground** | Playground — Apache-2.0, «не официальный продукт Google» | [36] | можно использовать коммерчески; самая безопасная основа |
| **GR00T N1.7** | Код — Apache 2.0 (LICENSE-файл) [25]; веса — NVIDIA Open Model License; README при этом называет модель «fully commercially licensable under Apache 2.0» — внутреннее противоречие страницы | [25] | прочитать текст NVIDIA Open Model License перед коммерческим хостингом |
| **openpi (π0, π0-FAST, π0.5)** | Репозиторий Apache-2.0; в репо лежит LICENSE_GEMMA.txt (Gemma Terms of Use): хостинг/API считается Distribution, нужно передавать Prohibited Use Policy вниз; прямого запрета/разрешения «коммерческого использования» в тексте нет | [21] [37] | Лицензия именно **весов π0** на странице не указана (пробел); π0.5 строится на Gemma-подобной базе, условия Gemma на хостинг нужно соблюдать |
| **LeRobot, SO-ARM100** | Apache-2.0 | [38] [16] | свободно |
| **Gemini Robotics** | **не исследовано** (лимит поиска) | — | пробел |
| SOC 2 (Type II) | **источников нет**; (оценка) $25–60K за первый год (платформа автоматизации + аудит) | — | нужен для B2B после seed |
| Юристы (корпоративное право, IP, OSS-лицензии, ToS/privacy) | (оценка) $30–80K в год на seed | — | |
| Страхование (cyber, E&O, product liability для робототехники) | (оценка) $10–40K в год; рост при физических инсталляциях у клиентов | — | см. юридическую ответственность за вред роботов в `07-risks-safety-regulation.md` |
| Облачные сервисы (CI, мониторинг, auth, email, аналитика) | (оценка) $2–5K/мес на seed | — | |

**(вывод)** Самое «дешёвое» и безопасное технологическое основание — MuJoCo Playground + LeRobot + SmolVLA (всё Apache-2.0 [36] [38]); Isaac Sim/GR00T/π0 дают лучший реализм и качество, но тянут лицензионные риски хостинга, которые надо снять юридически **до** вложения в продукт.

---

## 7. Бюджетные сценарии

Допущения: средние ставки с ramp-ом найма (команда растёт линейно), compute по ценам раздела 1 (+30% запас на рост цен, см. 1.2), железо из раздела 3 (разовая закупка плюс ~10% на ремонт), всё `(оценка)`.

### 7.1. Сценарий 1: bootstrap / pre-seed MVP, 9 месяцев

Цель: no-code прототип для 1–2 типов задач (IL на SO-101 + локомоция в симуляции), 50–200 бета-пользователей, весь compute — spot/community-облако.

| Статья | Состав | Сумма за 9 мес. | В месяц |
|---|---|---|---|
| Люди | 2 основателя (по ~$6K/мес) + RL/ML инженер удалённо ($9K) + full-stack ($8K) + hardware-контрактор ($3K) + налоги/бенефиты | ~$315K | ~$35K |
| Compute | разработка, бесплатные запуски бета-пользователей (~200 × 3 задачи × ~$10) и R&D | ~$45K | ~$5K |
| Железо | зоопарк «Бронза» ($12–18K) + 2 станции с RTX 4090/5090 + Jetson ≈ $25K разово | ~$25K | ~$2.8K |
| Данные | сбор демо, хранение, подписки, покупка небольших датасетов | ~$18K | ~$2K |
| Прочее | юристы (инкорпорация, ToS), SaaS, страхование, бухгалтерия, поездки | ~$36K | ~$4K |
| **Итого** | | **~$440K** | **~$49K/мес** |

Запас 15% (оценка) → цель раунда **$0.5–0.6M**.

### 7.2. Сценарий 2: seed, 18 месяцев

Цель: публичный запуск, 3–4 типа задач (IL, локомоция RL, SmolVLA/π0.5, возможно LLM-агенты), платящие клиенты, поддержка нескольких роботов, подготовка к SOC 2.

| Статья | Состав | Сумма за 18 мес. | В месяц (среднее) |
|---|---|---|---|
| Люди | рост 6 → 12 человек; средний FTE ~$15K/мес полная стоимость | ~$2.25M | ~$125K |
| Compute | бесплатный тир + платные запуски + R&D; ~$25K/мес в среднем | ~$450K | ~$25K |
| Железо | зоопарк «Серебро» ($110–150K) + ремонт/запас | ~$150K | ~$8K |
| Данные | сбор/покупка демо, annotation, хранение, egress | ~$270K | ~$15K |
| Прочее | юристы ($80K/год), SOC 2 (~$40K), страхование, инфраструктура SaaS, поездки, маркетинг/конференции | ~$360K | ~$20K |
| **Итого** | | **~$3.5M** | **~$193K/мес** |

Запас 15% → **$4.0M** (оценка; совпадает с типичным размером seed-раунда, см. `01-market-competitors.md` по сопоставимым раундам и `06-business-models-pricing.md`).

### 7.3. Сценарий 3: Series A, 24 месяца

Цель: масштабируемая платформа, enterprise-клиенты, маркетплейс моделей/сред, кластер резервированных GPU.

| Статья | Состав | Сумма за 24 мес. | В месяц (среднее) |
|---|---|---|---|
| Люди | рост 18 → 30; средний FTE ~$17K/мес | ~$8.2M | ~$340K |
| Compute | резервы/Savings Plans (экономия до ~50% к on-demand [11] [12]), spot, инференс-стенды; ~$90K/мес | ~$2.2M | ~$90K |
| Железо | зоопарк «Золото» ($300–400K) + лаборатория | ~$0.4M | ~$17K |
| Данные | собственные датасеты, партнёры-поставщики, хранение 100+ ТБ | ~$1.44M | ~$60K |
| Прочее | SOC 2 Type II, юристы, страхование, GTM, events, офис | ~$1.7M | ~$70K |
| **Итого** | | **~$13.9M** | **~$580K/мес** |

Запас 15% → **~$16M** (оценка).

### 7.4. Сводка сценариев

| Сценарий | Горизонт | Всего | Burn/мес | Люди % | Compute % | Железо % | Данные % | Прочее % |
|---|---|---|---|---|---|---|---|---|
| 1. Pre-seed | 9 мес. | ~$0.44M | ~$49K | 72% | 10% | 6% | 4% | 8% |
| 2. Seed | 18 мес. | ~$3.5M | ~$193K | 64% | 13% | 4% | 8% | 10% |
| 3. Series A | 24 мес. | ~$13.9M | ~$580K | 59% | 16% | 3% | 10% | 12% |

(Доли — мой расчёт из таблиц выше.) Детальный финансовый план и unit-экономика — в синтезирующем `12-resources-financial-plan.md` (волна 2).

**Чувствительность:** рост цен GPU на +50% увеличит сценарий 2 на ~$225K (+6%) — не критично; а вот найм 2 senior RL-инженеров по рыночным ставкам США вместо удалённых добавит ~$300–500K в год (оценка). **Главный драйвер бюджета — люди, а не GPU** (вывод).

---

## Выводы для платформы

1. **Compute на пользователя дёшев, но неоднороден.** Типичные задачи (локомоция, IL, SmolVLA) стоят платформе $1–45 за задачу; π0.5 — $15–130; LLM-RL 7B — $150–1800 (низкая уверенность). Прайс-план должен отделять «лёгкие» задачи (почти безлимит) от «тяжёлых» (кредиты/лимиты). См. `06-business-models-pricing.md`.
2. **Не закладывать падение цен GPU.** После падения 2025 года цены H100 в 2026 году выросли (+~40% за 6 месяцев по SemiAnalysis [34]); on-demand ёмкость местами распродана. Нужны мульти-провайдерная архитектура и spot с чекпоинтами; резерв — после появления стабильной нагрузки.
3. **Не покупать свои B200 на ранних стадиях.** Сервер $360–560K [33] окупается за ~10–12 месяцев лишь при загрузке близкой к 100% (мой расчёт); нагрузка стартапа будет рваной. Хватит 1–2 станций на RTX 4090/5090 + облако.
4. **Isaac Sim ≠ H100.** Isaac Sim требует RT-GPU (L40S-класс) [35]; MuJoCo Playground идёт на любой CUDA-GPU и стоит минуты на одной карте [20] [36]. Для MVP логично начать с MuJoCo/MJX + LeRobot (Apache-2.0), а Isaac добавлять как премиум-опцию после юридической проверки Omniverse terms.
5. **Лицензии моделей — реальный риск.** GR00T: веса под NVIDIA Open Model License при противоречивых заявлениях README [25]; openpi: Gemma Terms при хостинге как Distribution [37], лицензия самих весов π0 на странице не указана. Нужен юрист до коммерческого хостинга (см. `07-risks-safety-regulation.md`).
6. **«Зоопарк» для QA недорог, если делать ставку на дешёвые роботы:** SO-101 (~$250/пара [15]), Go2, R1 — менее $20K на старте; ~$110–150K на seed; дорогие ALOHA/Franka/UR/H2 — по мере необходимости партнёров/клиентов.
7. **Главный скрытый ресурс — демонстрационные данные пользователей:** 2–5 часов оператора на простой навык (оценка), а по рынку $28–60 за сырой час телеоперации [30]. Платформа выигрывает, если сокращает число демо (sim-генерация, аугментация, шаблонные навыки). См. `02-rl-tech-state-of-art.md`.
8. **Хранилище: R2/B2 вместо S3** из-за egress ($0 против $0.09/ГБ [31]) — видео и датасеты будут гоняться между GPU-провайдерами.
9. **Деньги уходят в людей (59–72% бюджета).** Найм RL-инженеров дорог и труден ($185–475K в США по robot-learning ролям [32]); стратегия: основатель-RL + удалённые senior + ML-генералисты; сопоставимые ставки в Европе и дешёвых регионах нужно подтвердить (пробел).
10. **Бюджеты:** pre-seed ~$0.5M (9 мес., ~$49K/мес), seed ~$4M (18 мес., ~$193K/мес), Series A ~$16M (24 мес., ~$580K/мес) — всё `(оценка)`. Перед использованием в материалах для инвесторов закрыть пробелы: прайсы Nebius/Modal/GCP/Azure/L40S, GPU-часы GRPO, SOC 2/юристы/страхование, зарплаты в Европе, лицензии Gemini Robotics и Omniverse.

---

## Источники

Все ссылки — вторичные обзоры, ритейлеры или GitHub-страницы; официальные прайс-страницы провайдеров в этой среде были недоступны (DNS), поэтому проверять цены нужно отдельно. Дата обращения везде 2026-10-27.

[1] CoreWeave, Lambda, Nebius, and GMI: H200 GPU Provider Pricing 2026 — GMI Cloud — https://www.gmicloud.ai/en/blog/h200-gpu-provider-pricing — (дата обращения 2026-10-27). Цифры CoreWeave/Lambda также повторяются в результатах поиска по запросу «H100 B200 H200 cloud GPU price per hour 2026 Lambda CoreWeave» (Spheron, CloudZero, IntuitionLabs).
[2] Cloud GPU pricing comparison 2026: every provider's real rates — CloudZero — https://www.cloudzero.com/blog/cloud-gpu-pricing-comparison/ — (2026-10-27)
[3] H100 Rental Prices Compared: $1.49-$6.98/hr Across 15+ Cloud Providers (2026) — IntuitionLabs — https://intuitionlabs.ai/articles/h100-rental-prices-cloud-comparison — (2026-10-27)
[4] GPU Cloud Pricing Comparison 2026: H100, H200, B200 Rates — Spheron — https://www.spheron.network/blog/gpu-cloud-pricing-comparison-2026/ — (2026-10-27)
[5] Runpod GPU pricing: A complete breakdown and platform comparison — Northflank — https://northflank.com/blog/runpod-gpu-pricing — (2026-10-27)
[6] RunPod Pricing — usagepricing.com — https://www.usagepricing.com/blueprint/runpod — (2026-10-27)
[7] RunPod GPU Pricing: 2026 Comprehensive Pricing Guide — DeployBase — https://deploybase.ai/articles/runpod-gpu-pricing — (2026-10-27)
[8] Runpod GPU Pricing: Compare 39+ GPUs — computeprices.com — https://computeprices.com/providers/runpod — (2026-10-27)
[9] Runpod Pricing vs Thunder Compute (2026) — Thunder Compute — https://www.thundercompute.com/blog/runpod-pricing-vs-thunder-compute — (2026-10-27)
[10] Announcing up to 45% price reduction for Amazon EC2 NVIDIA GPU-accelerated instances — AWS News Blog — https://aws.amazon.com/blogs/aws/announcing-up-to-45-price-reduction-for-amazon-ec2-nvidia-gpu-accelerated-instances/ — (2026-10-27; прочитано через сниппет поиска, страница недоступна для WebFetch)
[11] AWS H100 pricing 2026 — Spheron — https://spheron.network/blog/aws-h100-pricing-2026 — (2026-10-27)
[12] AWS GPU Pricing — Opslyft — https://www.opslyft.com/blog/aws-gpu-pricing — (2026-10-27)
[13] LLM cost optimization on AWS — Usage.ai — https://www.usage.ai/blogs/aws/ai-ml-cost/llm-cost-optimization-aws/ — (2026-10-27)
[14] Unitree prices: Unitree Robot Price Guide 2026 — robotpriceindex.com — https://robotpriceindex.com/guides/unitree-robot-price-guide ; Unitree R1 vs G1 — botinfo.ai — https://botinfo.ai/articles/unitree-r1-vs-g1 ; Unitree G1 Price 2026 — robozaps — https://blog.robozaps.com/b/unitree-g1-review ; Unitree Go2 Price 2026 — robozaps — https://blog.robozaps.com/b/unitree-go2-review ; Unitree Robot Price List 2026 — dijipedya — https://dijipedya.com/en/unitree-robot-price/ — (2026-10-27)
[15] SO-ARM101 open-source dual robotic arm kit works with Hugging Face's LeRobot — CNX Software — https://www.cnx-software.com/?p=149841 ; SO-ARM101 Pro kit — RobotShop UK — https://uk.robotshop.com/products/seeed-studio-so-arm101-ai-arm-servo-motor-kit-pro-lerobot-w-o-3d-printed-parts ; Slickdeals — https://slickdeals.net/f/19902168-seeed-studio-so-arm101-pro-6-axis-open-source-ai-robotics-arm-kit-13-servos-247-free-shipping — (2026-10-27)
[16] TheRobotStudio/SO-ARM100 (BOM) — GitHub — https://github.com/TheRobotStudio/SO-ARM100 — (2026-10-27)
[17] Nvidia's Jetson AGX Thor costs 3499 US dollars as a dev kit — heise — https://heise.de/-10622015 ; NVIDIA Jetson prices jump up to 101% — HWBusters — https://hwbusters.com/news/nvidia-jetson-prices-jump-up-to-101-the-249-orin-nano-super-is-now-399/ ; NVIDIA increases the price of Jetson modules and devkits by up to 101% — CNX Software (2026-07-22) — https://www.cnx-software.com/2026/07/22/nvidia-increases-the-price-of-jetson-modules-and-devkits-by-up-to-101/ — (2026-10-27)
[18] Reinforcement Learning Library Comparison — Isaac Lab docs — https://isaac-sim.github.io/IsaacLab/v2.3.2/source/overview/reinforcement-learning/rl_frameworks.html — (2026-10-27; данные 198 с на RTX 4090 получены из результатов поиска)
[19] Fourier GR3 RL training — Fourier docs — https://support.fftai.com/en/docs/Opensource/RL-Learning/GR3-example/train/ — (2026-10-27)
[20] MuJoCo Playground — arXiv 2502.08844 — https://arxiv.org/html/2502.08844v1 — (2026-10-27; утверждения из аннотации через поиск)
[21] Physical-Intelligence/openpi — GitHub — https://github.com/Physical-Intelligence/openpi — (2026-10-27)
[22] LeRobot Hardware Guide (docs/source/hardware_guide.mdx) — Hugging Face / GitHub — https://github.com/huggingface/lerobot/blob/main/docs/source/hardware_guide.mdx — (2026-10-27)
[23] How to Fine-Tune SmolVLA on SO-101 with LeRobot — OpenELAB — https://openelab.io/blogs/learn/how-to-fine-tune-smolvla-on-so-101-with-lerobot — (2026-10-27)
[24] GR00T N1.7 on SO-101: LeRobot Setup and GPU Requirements — OpenELAB — https://openelab.io/blogs/learn/nvidia-groot-1-7-so-101-lerobot-requirements — (2026-10-27)
[25] NVIDIA/Isaac-GR00T — GitHub (README, LICENSE) — https://github.com/NVIDIA/Isaac-GR00T — (2026-10-27)
[26] OpenVLA: An Open-Source Vision-Language-Action Model — arXiv 2406.09246 — https://arxiv.org/pdf/2406.09246 — (2026-10-27)
[27] Mobile ALOHA — Maginative — https://www.maginative.com/article/stanfords-unveils-a-new-low-cost-mobile-robotics-training-system/ ; Trossen Stationary AI — https://www.trossenrobotics.com/stationary-ai ; Trossen Mobile AI — https://www.trossenrobotics.com/mobile-ai — (2026-10-27)
[28] The 5 Robot Arm Price Tiers — Robotics Center — https://www.roboticscenter.ai/guides/robot-arm-pricing-2026 ; Universal Robots price guide — Standard Bots — https://standardbots.com/articles/universal-robot-price — (2026-10-27)
[29] 1X Opens Pre-Orders for NEO Humanoid Robot at $20,000 — Humanoids Daily — https://www.humanoidsdaily.com/news/1x-opens-pre-orders-for-neo-humanoid-robot-at-20000 — (2026-10-27)
[30] Teleoperation Data Collection: 2026 Guide, Rigs & Costs — Dexset — https://dexset.ai/blogs/teleoperation-data-collection-robot-learning-complete-2026/ ; Robot Training Data Costs & Pricing Guide (2026) — Dexset — https://dexset.ai/blogs/robot-training-data-costs-pricing-complete-2026/ ; Robotics dataset cost calculator — RoboSignal — https://robosignal.ai/tools/dataset-evidence ; DexViTac — arXiv 2603.17851 — https://arxiv.org/pdf/2603.17851 — (2026-10-27)
[31] Cloudflare R2 pricing explained: real costs vs S3 and Backblaze — mecanik.dev — https://mecanik.dev/en/posts/cloudflare-r2-pricing-explained-real-costs-vs-s3-and-backblaze/ — (2026-10-27)
[32] Machine Learning Engineer Salary in United States — Levels.fyi — https://www.levels.fyi/t/software-engineer/title/machine-learning-engineer/locations/united-states ; How to Hire Robotics Engineers in 2026: Salary + Stack Guide — KORE1 — https://www.kore1.com/hire-robotics-engineers-2026/ — (2026-10-27)
[33] NVIDIA DGX B200 price — DeployBase — https://deploybase.ai/articles/nvidia-dgx-b200-price ; NVIDIA AI GPU Prices — IntuitionLabs — https://intuitionlabs.ai/articles/nvidia-ai-gpu-pricing-guide — (2026-10-27)
[34] Тренд цен H100: Nvidia H100 GPU Rental Costs Jump Nearly 40% Over Six Months: SemiAnalysis — iTiger — https://www.itiger.com/news/1185188896 ; GPU price increase 2026 (Hyperbolic H100) — Spheron — https://www.spheron.network/blog/gpu-price-increase-2026-hyperbolic-h100/ ; H100 GPU Price Trends — Cyfuture — https://cyfuture.cloud/kb/gpu/h100-gpu-price-trends-and-future-expectations ; H100 Rental Price 2026 — Akash — https://akash.network/the-bid/h100-rental-price-2026-cost-per-hour/ — (2026-10-27)
[35] isaac-sim/IsaacSim — GitHub — https://github.com/isaac-sim/IsaacSim — (2026-10-27)
[36] google-deepmind/mujoco_playground — GitHub — https://github.com/google-deepmind/mujoco_playground — (2026-10-27)
[37] Gemma Terms of Use (LICENSE_GEMMA.txt) в openpi — GitHub — https://github.com/Physical-Intelligence/openpi/blob/main/LICENSE_GEMMA.txt — (2026-10-27)
[38] huggingface/lerobot — GitHub; droid-dataset/droid — GitHub — https://github.com/huggingface/lerobot ; https://github.com/droid-dataset/droid — (2026-10-27)
