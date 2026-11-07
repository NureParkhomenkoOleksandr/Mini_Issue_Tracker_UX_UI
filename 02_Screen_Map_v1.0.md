# Screen Map — Mini Issue Tracker

Версія: 1.0  
Дата: 07.11.2026  
Етап: G2  
Статус: APPROVED design plan після G4; не готовий макет.

## 1. Вхід і межі

Вхід: SD_Spec.docx.pdf; 01_Input_Pack_v1.0.md; Decision_Log.md v1.1 (D-01–D-14 APPROVED). Методичні рекомендації, §7–8, визначають формат цього етапу. Приклад іншої роботи не використовується як доказ виконання.

Позначення: SOURCE — вимога специфікації; DERIVED — висновок із неї; APPROVED — погоджене D-рішення; PROPOSED — деталізація цього плану, яка ще підлягає перевірці.

Продуктові можливості обмежено US-01–US-08. Не додаються attachments, AI, видалення, історія змін або нові ролі. Контроль A студентом ще не зафіксовано: автор підтвердив UX-деталі й три граничні правила після G4; незалежний source audit не заявляється.

## 2. Архітектура та кількість frames

| ID | Назва | Тип | Призначення |
|---|---|---|---|
| S-01 | Authentication boundary | Службова межа входу | Позначити вимогу входу без форми пароля або SSO |
| S-02 | Issues List | Продуктовий екран | Перегляд одного набору заявок |
| S-02-A | All | Стан S-02 | Усі зареєстровані заявки |
| S-02-B | Important | Стан S-02 | High/Critical AND Status != Closed |
| S-02-C | Empty All | Порожній стан S-02 | Зареєстрованих заявок немає |
| M-01 | Create Issue | Modal / overlay над S-02 | Введення Title та Description |
| S-03 | Issue Details | Продуктовий екран | Деталі, assignee, priority, status, comments |
| REF-01 | Verification reference | Службові анотації та приклади компонентів | Права, дозволені переходи, validation/error/success states |

Мінімальний inventory: **2 продуктові екрани** (S-02, S-03), **1 modal** (M-01), **1 boundary** (S-01). Для демонстрації планується **7 верхньорівневих Figma frames**: S-01, S-02-A, S-02-B, S-02-C, M-01, S-03, REF-01. M-01 є frame для overlay, а не окремою сторінкою. REF-01 — не екран продукту; приклади усередині нього не рахуються як окремі продуктові екрани.

Додаткові стани можна показувати variants або компактними прикладами в REF-01. За потреби реалізації кліків кількість технічних копій frames уточнюється пізніше; це не розширює продуктову архітектуру. Підстава: D-01/02/08; методичні рекомендації §7–8.

## 3. Опис surfaces та states

### S-01 — Authentication boundary

- **Purpose:** позначити межу доступу; не проєктувати спосіб входу.
- **Actors:** неавтентифікований відвідувач лише як контекст вимоги; після автентифікації — Team Member або Team Lead.
- **Entry:** концептуальна точка входу до системи. Основна демонстрація починається із S-02-A.
- **Visible data:** назва Mini Issue Tracker; нейтральна анотація «Authentication required — mechanism TBD».
- **Inputs:** немає.
- **Actions:** справжній login не реалізується; можливий службовий перехід до демонстрації, позначений як симуляція.
- **Role/state conditions:** реальна система потребує автентифікації; прототип не доводить її виконання.
- **Errors/empty:** помилки пароля/SSO не вигадуються.
- **Exit:** після концептуального проходження межі — S-02-A або S-02-C за відсутності даних.
- **Source:** BR-01, NFR-02; APPROVED D-02/08. Службове оформлення — APPROVED D-14.

### S-02-A — All Issues

- **Purpose:** перегляд усіх зареєстрованих заявок, включно із Closed.
- **Actors:** усі три автентифіковані користувачі.
- **Entry:** початок демонстрації; вкладка All; повернення із S-03; Cancel із M-01, відкритого над All.
- **Visible data:** для кожного issue — ID, Title, Status, Priority, Assignee за наявності. Not Set відображає відсутній priority; відсутнього виконавця запропоновано показувати як Unassigned.
- **Inputs:** не потрібні для зміни даних списку.
- **Actions:** Important; Create Issue; відкрити деталі через Title конкретної заявки.
- **Role/state conditions:** перегляд та Create доступні Team Member і Team Lead; керування assignee/priority/status виконується в S-03.
- **Errors/empty:** немає заявок → S-02-C. Помилка завантаження окремо джерелом не визначена й не видається за AC.
- **Exit:** S-02-B, M-01 або S-03 вибраного issue.
- **Source:** AC-02.1–AC-02.3, AC-05.3, BR-02; APPROVED D-01/03/07. Відкриття через Title та текст Unassigned — APPROVED D-09/11.

### S-02-B — Important Issues

- **Purpose:** показати відфільтрований стан того самого набору даних.
- **Actors:** Team Member, Team Lead.
- **Entry:** вкладка Important; повернення з деталей, відкритих із Important; Cancel із modal над Important.
- **Visible data:** ті самі колонки, що в All; лише High/Critical зі статусом не Closed. Resolved включається; Low, Normal, Not Set та Closed виключаються.
- **Inputs:** немає окремих параметрів фільтра.
- **Actions:** All; Create Issue; Title → S-03 конкретного issue.
- **Role/state conditions:** доступно всім автентифікованим користувачам. Фільтрація не створює незалежні копії заявок.
- **Errors/empty:** якщо збігів немає, запропоновано порожній стан у цьому самому view «No important issues». Це APPROVED D-11, UX-деталізація, не новий AC; окремий верхньорівневий frame не потрібний.
- **Exit:** S-02-A або S-02-C залежно від даних; M-01; S-03.
- **Source:** AC-08.1–AC-08.4, BR-09/09.1; APPROVED D-01/07.

### S-02-C — Empty All

- **Purpose:** пояснити відсутність зареєстрованих заявок.
- **Actors:** Team Member, Team Lead.
- **Entry:** All, коли загальний набір порожній; Cancel із modal над порожнім All.
- **Visible data:** структура списку, активна вкладка All, повідомлення «No issues yet» (погоджений текст D-11/12).
- **Inputs:** немає.
- **Actions:** Create Issue; Important → порожній стан Important в межах S-02-B.
- **Role/state conditions:** жодного issue не можна відкрити за відсутності рядків.
- **Errors/empty:** це відсутність даних, а не помилка завантаження.
- **Exit:** M-01; S-02-B (empty).
- **Source:** AC-02.5, BR-02; APPROVED D-01.

### M-01 — Create Issue

- **Purpose:** створити заявку з Title та Description.
- **Actors:** Team Member, Team Lead.
- **Entry:** Create Issue із S-02-A/B/C; зберігається calling list state.
- **Visible data:** заголовок Create Issue, labels Title/Description, позначення обов’язковості; локальні помилки за потреби.
- **Inputs:** лише Title та Description. ID, status, author, created_at, assignee, priority не вводяться користувачем.
- **Actions:** Create; Cancel.
- **Role/state conditions:** обидва поля обов’язкові; за invalid даних issue не створюється. За успіху: ID, Open, created_at, author; priority Not Set; assignee відсутній за D-04.
- **Errors/empty:** default; missing Title («Title is required» — SOURCE Gherkin); missing Description («Description is required» — погоджений текст D-11/12); обидва порожні. Це стани modal, не нові екрани.
- **Exit:** Cancel → точний calling list state без створення; successful Create → S-03 підготовленого нового issue (APPROVED D-10).
- **Source:** AC-01.1–AC-01.5; BR-02–BR-05; APPROVED D-01/04/08.

### S-03 — Issue Details

- **Purpose:** переглянути заявку та виконувати дозволені дії в одному контексті.
- **Actors:** Team Member/Team Lead, кожен у контексті assignee або non-assignee.
- **Entry:** Title у S-02-A/B; успішний Create у M-01.
- **Visible data:** ID, Title, Description, поточні Status/Priority/Assignee, Author, Created at; збережені коментарі з текстом, автором, датою й часом.
- **Inputs:** вибір одного assignee; priority з Low/Normal/High/Critical; тільки дозволені наступні status; текст коментаря.
- **Actions:** Apply біля assignee/priority/status; Add Comment; Return to Issues List.
- **Role/state conditions:** assignee/priority змінює лише Team Lead; status — лише поточний assignee, включно з Team Lead. Заборонені controls disabled. Not Set — відображення відсутності, не selectable рівень і не reset. У Closed наступної зміни status немає; інші можливості автоматично не блокуються.
- **Errors/empty:** no assignee; Not Set; відсутність коментарів (PROPOSED нейтральний placeholder); empty-comment validation; comment-save-error без нового коментаря; saved-comment state. Чотири контексти прав та всі статуси показуються компактно в REF-01.
- **Exit:** Return → попередня вкладка списку; успішні Apply/Add Comment залишають S-03. Після Create origin зберігається від calling list state (APPROVED D-10, деталізація D-07).
- **Source:** AC-02.4, US-03 AC, AC-04.1/2, AC-05.2, AC-06.1–AC-06.5, AC-07.1–AC-07.5; BR-08.1; APPROVED D-03–D-08.

### REF-01 — Verification reference

- **Purpose:** зробити права, переходи та негативні стани перевірними без дублювання повних деталей заявки.
- **Actors:** студент/рецензент; це не додаткова роль у продукті.
- **Entry/Exit:** перегляд design file; продуктових переходів немає.
- **Visible data:** чотири контексти Member non-assignee / Member assignee / Lead non-assignee / Lead assignee; таблиця дозволених переходів; Unassigned; Not Set; приклади validation Create; comment ready/empty/saved/failure; приклад нової заявки.
- **Inputs/Actions:** немає продуктових inputs або перемикача ролей.
- **Role/state conditions:** підписи фіксують test actor, issue ID, current status. REF пояснює стани, але не доводить їх інтерактивність.
- **Errors/empty:** компактні приклади станів із посиланнями на source та D-ID.
- **Source:** методичні рекомендації §8; AC-01.2/01.3, AC-06.1–AC-06.5, AC-07.4/07.5, BR-08.1; D-05/08. Організація REF — APPROVED D-14.

## 4. Права та статуси

| Контекст | Assignee | Priority | Status | Comments |
|---|---|---|---|---|
| Team Member, non-assignee | Disabled | Disabled | Disabled | Доступні |
| Team Member, assignee | Disabled | Disabled | Лише дозволені переходи | Доступні |
| Team Lead, non-assignee | Доступний | Доступний | Disabled | Доступні |
| Team Lead, assignee | Доступний | Доступний | Лише дозволені переходи | Доступні |

Джерело: US-03 AC, AC-04.2, AC-07.4, US-06; D-05. Для всіх контекстів у Closed немає наступного status. Для unassigned ніхто не може змінити status до призначення (DERIVED із AC-07.4). Після перепризначення права status перераховуються за новим поточним assignee.

| Поточний status | Дозволені наступні |
|---|---|
| Open | In Progress |
| In Progress | Resolved |
| Resolved | In Progress, Closed |
| Closed | Немає |

SOURCE: BR-08.1. Поточний status показано як значення, а не запропоновано як новий перехід. Лише наявність assignee без дозволеного переходу не робить status enabled.

## 5. Таблиця переходів та результатів дій

T-ID — локальні ID цього плану, не ID вихідних вимог. Рядки відхилення позначають відсутність успішного переходу. Усі дії тут є намірами дизайну; у прототипі вони можуть бути симуляціями D-08.

| T-ID | From | Actor | Trigger | Preconditions | To | Visible result | Requirement / D-ID |
|---|---|---|---|---|---|---|---|
| T-01 | S-01 | Член команди | Концептуальне проходження межі | Для справжньої системи authentication; у демо підготовлений контекст | S-02-A/C | All або порожній All; login не імітується як реальний | BR-01; D-02/08 |
| T-02 | S-02-A/B | Усі | Title | Існує вибраний issue | S-03 | Деталі саме вибраного ID; origin збережено | AC-02.3/02.4; D-07 |
| T-03 | S-02-A/C | Усі | Important | Автентифікований контекст | S-02-B | Лише High/Critical, не Closed; або empty | AC-08.1–AC-08.4; D-01 |
| T-04 | S-02-B | Усі | All | Автентифікований контекст | S-02-A/C | Повний набір або empty | AC-02.1/02.5; D-01 |
| T-05 | S-02-A/B/C | Усі | Create Issue | Право створення | M-01 | Modal над calling state | BR-02; D-01 |
| T-06 | M-01 | Усі | Cancel | Modal відкритий | Calling S-02-A/B/C | Modal закрито, issue не створено | D-01/08; D-10 |
| T-07 | M-01 | Усі | Create | Title порожній | M-01 validation | «Title is required»; issue не створено | AC-01.2; Gherkin US-01 |
| T-08 | M-01 | Усі | Create | Description порожній | M-01 validation | Помилка Description; issue не створено | AC-01.3 |
| T-09 | M-01 | Усі | Create | Обидва обов’язкові поля заповнено | S-03 new | Новий ID, Open, Not Set, author, created_at, Unassigned | AC-01.1–AC-01.5; D-04/08; D-10 |
| T-10 | S-03 | Усі | Return to Issues List | Origin відомий | Попередня вкладка S-02 | Збережено вкладку; поточний набір повторно відповідає предикату | D-07; AC-08.1–AC-08.4 |
| T-11 | S-03 | Team Lead | Assignee → Apply | Один член команди вибраний | S-03 assigned | Виконавець показаний, права status оновлено | US-03 AC; D-04/06 |
| T-12 | S-03 | Team Lead | Інший Assignee → Apply | Є поточний виконавець | S-03 reassigned | Один новий виконавець замінює попереднього | D-04/06; US-03 |
| T-13 | S-03 | Team Lead | Priority → Apply | Вибрано Low/Normal/High/Critical | S-03 updated | Новий priority відображено | AC-04.1/04.2; BR-05/06; D-06 |
| T-14 | S-03 Open | Поточний assignee | In Progress → Apply | Користувач є assignee | S-03 In Progress | Поточний status оновлено | BR-08.1; AC-07.3/07.4; D-06 |
| T-15 | S-03 In Progress | Поточний assignee | Resolved → Apply | Користувач є assignee | S-03 Resolved | Status Resolved; High/Critical залишається Important | BR-08.1/09.1; AC-07.3/07.4 |
| T-16 | S-03 Resolved | Поточний assignee | In Progress → Apply | Користувач є assignee | S-03 In Progress | Роботу поновлено | BR-08.1; AC-07.3/07.4 |
| T-17 | S-03 Resolved | Поточний assignee | Closed → Apply | Користувач є assignee | S-03 Closed | Наступного переходу немає; при поверненні issue відсутнє в Important | BR-08.1; AC-08.4 |
| T-18 | S-03 | Усі | Add Comment | Текст непорожній, успіх збереження | S-03 comment-saved | Додано текст, автора, дату й час | AC-06.1–AC-06.4; D-08 |
| T-19 | S-03 | Усі | Add Comment | Текст порожній | S-03 comment-validation | Помилка; новий коментар відсутній | AC-06.1 |
| T-20 | S-03 | Усі | Add Comment | Непорожній текст, збій збереження | S-03 comment-save-error | Помилка; нового збереженого коментаря немає | AC-06.5 |
| T-21 | S-03 | Team Member | Спроба керувати assignee/priority | Немає права | Без успішного переходу | Controls disabled, значення незмінні | US-03, AC, пункт 3; AC-04.2; D-05 |
| T-22 | S-03 | Non-assignee, включно з Lead | Спроба змінити status | Не є поточним assignee | Без успішного переходу | Status control disabled | AC-07.4; D-05 |
| T-23 | S-03 | Поточний assignee | Недозволений перехід / невідомий status | Значення не дозволено правилами | Без успішного переходу | Значення недоступне; status не змінено | BR-08.1; AC-07.5 |
| T-24 | S-03 Closed/unassigned | Усі | Спроба змінити status | Немає наступного переходу або виконавця | Без успішного переходу | Зміна status недоступна | BR-08.1; AC-07.4; D-05 |

При T-07/T-08 обидві помилки можуть бути представлені одночасно. Відсутні рядки у списку не є клікабельними. Cancel не запускає T-09. Якщо issue після зміни перестало відповідати Important, повернення все одно відкриває вкладку Important, але без цього issue. Нова заявка з Not Set після повернення до Important також не з’являється там; у All вона присутня. Це наслідок D-07 та предиката US-08, а не новий фільтр.

## 6. User flows

| Flow | Сценарій та очікуваний результат |
|---|---|
| UF-01 | Створення: S-02-A/B/C → T-05 → M-01 → T-09 → S-03 new. Лише Title/Description вводяться; решта значень показана як підготовлений результат |
| UF-02 | Валідація: M-01 → T-07/T-08 → M-01 validation; issue не створено. Виправлення полів → T-09 |
| UF-03 | Скасування: S-02-B → M-01 → T-06 → S-02-B. Аналогічно для All та Empty All |
| UF-04 | Перегляд: S-02-A/B → T-02 → S-03 правильного ID → T-10 → та сама вкладка |
| UF-05 | Призначення: Lead, S-03 Unassigned → T-11 → S-03 assigned; T-12 → reassigned. Нові права status залежать від нового assignee |
| UF-06 | Priority: Lead, S-03 Not Set → T-13 → High/Critical; Return → Important включає issue, якщо воно не Closed. Low/Normal виключають його |
| UF-07 | Життєвий цикл: assignee, S-03 Open → T-14 → In Progress → T-15 → Resolved → T-17 → Closed |
| UF-08 | Повернення в роботу: assignee, S-03 Resolved → T-16 → In Progress; інші переходи недоступні |
| UF-09 | Comment success: S-03 → непорожній текст → T-18 → запис з автором і часом, користувач залишається в деталях |
| UF-10 | Comment errors: S-03 → T-19 або T-20 → validation/error; нового коментаря немає |
| UF-11 | Important: S-02-A → T-03 → S-02-B; High/Critical + Resolved видно, Closed/Low/Normal/Not Set не видно; T-04 повертає All |
| UF-12 | Заборонені дії: Member → T-21; non-assignee Lead/Member → T-22; assignee → T-23; Closed/unassigned → T-24. Успішного переходу та зміни даних немає |
| UF-13 | Порожня система: S-02-C → Create → M-01 → Cancel → S-02-C; або Create success → S-03 new → Return до All з новою заявкою |

## 7. Що не додавати

1. Окремі сторінки Assignment, Priority, Status та Comments: пов’язані дії виконуються у S-03.
2. Attachments та AI recommendations: US-09 відкладено, SR-10/SR-11 — майбутні.
3. Search, sorting, pagination, bulk actions, dashboards, редагування Title/Description після створення, видалення, user administration або додаткову роль Reviewer: такі функції не включено в погоджений scope.

Перший пункт — архітектура D-01 та методичні рекомендації §7. Другий — SOURCE §8. Третій — обмеження цього плану (відсутність вимоги не видається за універсальну заборону); видалення прямо заборонено BR-10.

## 8. Підсумкова перевірка та наступний етап

| US | Покриття маршрутом / станом |
|---|---|
| US-01 | M-01; T-07–T-09; REF-01 new/validation |
| US-02 | S-02-A/B/C, S-03; T-02/T-04/T-10 |
| US-03 | S-03; T-11/T-12/T-21; матриця прав |
| US-04 | S-03; T-13/T-21; Not Set та чотири рівні |
| US-05 | Status у списках і деталях |
| US-06 | S-03 та REF-01; T-18–T-20 |
| US-07 | S-03 та REF-01; T-14–T-17, T-22–T-24 |
| US-08 | S-02-B; T-03/T-04; перевірка предиката після змін |

Під час підготовки AI звірено наявність маршрутів восьми US, негативних сценаріїв, матриці прав, чотирьох дозволених status transitions та повернення до попередньої вкладки. Це перевірка тексту плану, а не тест виконаного прототипу або незалежне погодження.

**Unresolved:** технічний механізм authentication (Q-01) поза дизайном. UX-деталі попереднього draft прийнято як D-09–D-14 у Decision_Log.md v1.1. Вони не змінюють прав або складу MVP.

**Межі:** Traceability та 38 запланованих tests наведені в 03_Screen_Contracts_v1.0.md. Жоден тест майбутнього макета ще не виконано. Persistence, server permissions і NFR потребують реалізації. Людське підтвердження стосується представлених UX-рішень та трьох сценаріїв G4; повний незалежний review не стверджується.

Історія: 0.1 збережено як draft; 1.0 — після G4, синхронізовано погоджені D-ID. T-01–T-24 та UF-01–UF-13 збережено. Базовий P-scope визначено в Screen Contracts 1.0; V-only examples не видаються за wired interactions.
