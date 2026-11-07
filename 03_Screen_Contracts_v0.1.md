# Developer-Verifiable Screen Contracts — Mini Issue Tracker

Версія: 0.1  
Дата: 07.11.2026  
Етап: G3  
Статус: DRAFT — контракт для review; макет і прототип ще не створено.

## 1. Контекст, джерела, статус доказів

Вхідні документи:
- SD_Spec.docx.pdf: §1 Open Questions; §3 BR; §5 US/AC; §8 Release Scope та Updated NFRs.
- 01_Input_Pack_v1.0.md: 8 US, 33 змістові AC.
- Decision_Log.md v1.0: D-01–D-08 APPROVED автором роботи.
- 02_Screen_Map_v0.1.md: draft G2; T-01–T-24, UF-01–UF-13.
- Методичні рекомендації §9–10: формат контракту та логічні перевірки, не нові продуктові вимоги.

SOURCE — пряма вимога специфікації; DERIVED — висновок із неї; APPROVED D — погоджений UX-вибір; PROPOSED D — деталізація, що підлягає review.

Поточний документ формалізує draft G2. Погодження всього Screen Map та контроль A студентом окремо не зафіксовані. Дозвіл продовжувати підготовку не видається за виконану перевірку. Контроль B перед Figma ще попереду.

UIR-ID, C-ID, N-ID та TEST-ID — локальні ідентифікатори контракту; вони не замінюють вихідних AC-ID. S-/M-/REF- та T-ID з G2 збережено.

Рівні перевірки:
- **V** — статичний макет: видимі значення, disabled, validation/error examples, анотації.
- **P** — прототип: фактично зв’язані переходи та підготовлені результати, перевірені у Present mode.
- **I** — реалізація: справжні дані, серверні права, persistence та NFR.

Наразі всі тести мають **NOT RUN**. Заплановане покриття не є PASS. Приклад стану V не доводить взаємодію P або роботу I.

## 2. Реєстр додаткових UX-пропозицій

Нижче формалізовано лише пропозиції, вже позначені PROPOSED у G2. Вони не стають APPROVED через включення до контракту.

| D-ID | Пропозиція | Підстава | Статус |
|---|---|---|---|
| D-09 | Відкривати S-03 натисканням Title; назва заявки читається повністю в деталях | G2 S-02-A; AC-02.3/02.4 | PROPOSED |
| D-10 | Після Create відкривати S-03 нового issue; origin для Return брати зі списку, який відкрив modal. Cancel закриває modal без створення та повертає точний calling state | G2 M-01, T-06/T-09; D-07 | PROPOSED |
| D-11 | Відсутній assignee показувати як Unassigned. Empty All: «No issues yet». Empty Important: «No important issues». Це стани списку без нових сторінок | G2 S-02-A/B/C; AC-02.5, US-08 | PROPOSED |
| D-12 | Validation missing Description: «Description is required»; empty comment: «Comment cannot be empty»; failed save: «Could not save comment». При помилці коментаря зберігати введений текст; після успішного додавання очищати input | G2 згадує не визначені джерелом тексти; AC-01.3, AC-06.1/06.5. Поведінка input — додаткова UX-деталізація | PROPOSED |
| D-13 | Apply disabled, доки немає іншого допустимого вибраного значення. Status selector містить лише дозволені наступні статуси; за їх відсутності selector та Apply disabled | G2 §4; D-05/06; BR-08.1. Умова changed-value — UX-деталізація | PROPOSED |
| D-14 | REF-01 містить N-01–N-07 та компактні приклади; 7 верхньорівневих frames. Старт P у S-02-A; S-01 має лише службову анотацію без кнопки справжнього login | G2 inventory, REF-01; D-02/08 | PROPOSED |

Потрібних нових бізнес-правил для основного MVP не виявлено. D-09–D-14 — UX-пропозиції для review. Технічний спосіб authentication залишається UNRESOLVED поза межами прототипу.

## 3. Дані та контексти демонстрації

Навчальні користувачі: Member A, Member B, Lead. Це фіктивні імена двох Team Member та одного Team Lead за BR-01 і D-08; вони не вводять нові ролі. Assignee — відношення користувача до конкретного issue.

Набір нижче — PROPOSED fixture, не реальні збережені записи. Для кожного issue у деталях також підготувати Description, Author і Created at; для коментаря — text, author, created date/time. Значення ID/часу в макеті не є доказом автоматичної генерації.

| ID | Title | Status | Priority | Assignee | Important |
|---|---|---|---|---|---|
| ISS-001 | Login fails | Open | Critical | Member A | Так |
| ISS-002 | Form layout breaks | In Progress | Normal | Member B | Ні |
| ISS-003 | Export produces empty file | Resolved | High | Member A | Так |
| ISS-004 | Old crash report | Closed | Critical | Lead | Ні |
| ISS-005 | Help text typo | Open | Low | Unassigned | Ні |
| ISS-006 | Missing image | Open | Not Set | Unassigned | Ні |
| ISS-007 | New issue example | Open | Not Set | Unassigned | Ні; результат Create, спочатку не входить до базового набору |

S-02-A показує ISS-001–ISS-006. S-02-B показує ISS-001 і ISS-003. S-02-C — окремий fixture з порожнім набором, а не результат видалення. Канонічний S-03: Lead переглядає ISS-003, assignee Member A; assignee/priority enabled за умовами вибору, status disabled.

## 4. Контракти surfaces та states

### 4.1. S-01 — Authentication boundary

**Призначення:** позначення вимоги authentication. Actors: відвідувач як контекст межі; Team Member/Lead після входу. Entry: концептуальна точка входу; демонстрація P починається зі S-02-A за D-02.

**Visible data:** Mini Issue Tracker; N-01 «Authentication required — mechanism TBD». Це annotation, а не форма входу. Inputs та продуктові C-ID відсутні. Не додавати пароль, email/SSO або перемикач ролей.

**States:** default boundary; login errors не визначено. Incoming: немає в межах MVP-дизайну. Outgoing: T-01 лише концептуально; не позначати його як виконану автентифікацію. PROPOSED D-14 не потребує wiring S-01.

**Verification:** V — boundary annotation; P — старт у підготовленому authenticated context; I — фактичний login і захист доступу. Source: BR-01, NFR-02; D-02/08.

### 4.2. S-02 — Issues List: спільний контракт

Actors: усі автентифіковані користувачі. Entry: старт демо, T-01 концептуально, T-04, T-06 або T-10. Зберігається активна вкладка та issue ID для відкриття деталей.

#### Visible data

| Поле | Обов’язковість у списку | Відсутнє значення / presentation | Source |
|---|---|---|---|
| ID | Для кожного запису | Не вигадувати запис без ID | AC-02.2 |
| Title | Для кожного запису | Непорожній; повний текст у S-03; клікабельний за D-09 | AC-01.2, AC-02.2/02.3 |
| Status | Для кожного запису | Лише визначені чотири статуси | AC-02.2, AC-05.1/05.3, BR-07 |
| Priority | Колонка для кожного запису | Not Set як відсутність, а не п’ятий встановлений рівень | AC-02.2; BR-04/05; D-03 |
| Assignee | Показати призначеного | Unassigned за D-11, якщо відсутній | AC-02.2; D-04 |

#### Controls

| C-ID | Label / type | Visible / enabled | Trigger → результат | Source / D |
|---|---|---|---|---|
| C-01 | All / tab | Видимий завжди у S-02; активний tab не створює нової операції | Click → T-04, All з даними або empty | AC-02.1/02.5; D-01 |
| C-02 | Important / tab | Видимий завжди у S-02 | Click → T-03, відфільтрований той самий набір | AC-08.1–08.4; D-01 |
| C-03 | Create Issue / button | Видимий/enabled для всіх трьох authenticated users, також у empty | Click → T-05, M-01; calling state збережено | BR-02; D-01 |
| C-04 | Issue Title / link у рядку | Лише для існуючих рядків | Click → T-02, S-03 правильного ID; origin tab збережено | AC-02.3; D-07/09 |

#### States та transitions

| State | Entry / visible result | Empty/error | Incoming | Outgoing |
|---|---|---|---|---|
| S-02-A All | Загальний набір; All active | Нуль issues → S-02-C; loading error не вигадується як AC | T-01, T-04, T-06, T-10 | T-02, T-03, T-05 |
| S-02-B Important | Important active; предикат §7 | Нуль збігів → empty Important у цьому самому view за D-11 | T-03, T-06, T-10 | T-02 для рядків, T-04, T-05 |
| S-02-C Empty All | All active, жодного рядка; «No issues yet» | Це відсутність даних, не збій | T-01/T-04/T-06/T-10, коли набір порожній | T-03 → empty Important; T-05 |

V: колонки, дані, предикат на fixture та empty states. P: tabs, Create, правильний issue, return context. I: фактичне отримання даних, доступ і коректна фільтрація довільного набору. Порожній fixture не потребує функції видалення.

### 4.3. M-01 — Create Issue modal

Actors: authenticated Team Member/Lead. Entry: T-05 із S-02-A/B/C; modal зберігає calling state, а поля починаються порожніми як PROPOSED default цього контракту.

| C-ID | Label / type | Visible / enabled | Trigger → результат | Source / D |
|---|---|---|---|---|
| C-05 | Title / text input, required | Видимий та editable | Input → draft Title; Create перевіряє обов’язковість | AC-01.1/01.2 |
| C-06 | Description / multiline input, required | Видимий та editable | Input → draft Description; Create перевіряє обов’язковість | AC-01.1/01.3 |
| C-07 | Create / button | Видимий/enabled у default та validation для демонстрації помилок | Click → T-07/T-08 при invalid, T-09 при valid | AC-01.1–01.5; D-10 |
| C-08 | Cancel / button | Видимий/enabled, доки modal відкрито | Click → T-06; не створює issue, повертає calling state | D-10 |

SOURCE визначає обов’язковість полів, але не максимальну довжину або алгоритм trim. Не вводити вигаданий numeric limit; обробку whitespace-only уточнюють при реалізації, не видаючи її за прямий AC. У тестах empty означає рядок нульової довжини.

Автоматичні дані результату: ID, Open, created_at, author (AC-01.4), priority відсутній (AC-01.5), assignee відсутній (D-04). Це вихідні дані у S-03, не editable поля M-01. Поточний користувач — джерело author; час та унікальний ID задаються системою, конкретний механізм не визначено. Source: US-01 Gherkin, AC-01.4; D-08 для симуляції.

| State | Умова | Visible result | Transition |
|---|---|---|---|
| default | Новий modal | Порожні Title/Description, labels та required | T-05 |
| missing-title | Title empty, Description заповнений | «Title is required», issue не створено | T-07 |
| missing-description | Description empty, Title заповнений | «Description is required» за D-12, issue не створено | T-08 |
| missing-both | Обидва empty | Обидві помилки; issue не створено | T-07 + T-08 |
| valid-submit | Обидва непорожні | Modal закрито; S-03 нового ISS-007 | T-09, D-10 |
| cancelled | Cancel | Попередній view без нового issue | T-06, D-10 |

Помилка сервера при Create не визначена окремим AC; її не підміняти станом успіху й не оголошувати покритою comment-save-error.

V: поля, required, validation examples, new-issue fixture. P: overlay, Cancel і підготовлений valid route; validation лише якщо фактично зв’язана. I: справжнє створення, автоматичні поля, uniqueness, persistence.

### 4.4. S-03 — Issue Details

Actors: authenticated Member/Lead; для конкретного issue кожен є assignee або non-assignee. Entry: T-02 або T-09. Вибраний ID визначає всі поля; origin tab зберігається.

#### Visible data

| Поле | Обов’язковість / presentation | Відсутність | Source |
|---|---|---|---|
| ID | Показати ID вибраного issue | Не допускається для існуючого запису | AC-02.4 |
| Title | Показати повний текст; read-only після створення в цьому scope | Порожнє значення не очікується | AC-01.2; AC-02.4 |
| Description | Повний зміст; read-only у поточному scope | Порожнє значення не очікується | AC-01.3; AC-02.4 |
| Status | Поточне значення завжди видно, незалежно від права зміни | Не допускається | AC-05.1/05.2; BR-03/07 |
| Priority | Not Set або один із чотирьох встановлених рівнів | Not Set за D-03 | AC-02.4; BR-04/05 |
| Assignee | Один поточний член команди | Unassigned за D-11 | US-03 AC; D-04 |
| Author | Автор створення | Placeholder замість автора не є доказом AC | AC-01.4; AC-02.4 |
| Created at | Дата й час створення, формат читабельний | Не очікується для існуючого запису | AC-01.4; AC-02.4 |
| Comment text / author / created at | Для кожного успішно доданого коментаря | До додавання список може бути порожнім | AC-06.2–06.4 |

Керовані значення не дублюються непотрібно як окремі editable/read-only копії. Поточне значення selector або сусідній label може виконувати вимогу відображення, якщо його чітко видно. Жодної додаткової metadata, історії, attachments, категорії, Reviewer або Approve.

#### Controls

| C-ID | Label / type | Visible / enabled conditions | Trigger → результат | Source / D |
|---|---|---|---|---|
| C-09 | Assignee / single select | Видимий усім; enabled лише Lead. Options: Member A, Member B, Lead; один вибір | Вибір staged; C-10 застосовує | US-03 AC, пункти 1–3; D-04/05 |
| C-10 | Apply / adjacent button для Assignee | Видимий; enabled лише Lead + інший допустимий вибір за D-13 | T-11/T-12 → один поточний assignee; права status перераховано | US-03 AC, пункт 4; D-04/06/13 |
| C-11 | Priority / select | Видимий усім; enabled лише Lead. Current Not Set показується, але не є selectable level. Options: Low/Normal/High/Critical | Вибір staged; C-12 застосовує | BR-04–06; AC-04.1/04.2; D-03/05 |
| C-12 | Apply / adjacent button для Priority | Enabled лише Lead + інший допустимий вибір | T-13 → priority оновлено на S-03 | AC-04.1/04.2; D-06/13 |
| C-13 | Status / select | Видимий усім; enabled тільки current assignee + є allowed destinations. Current value видно, але не selectable transition | Вибір зі списку §6; C-14 застосовує | BR-08/08.1; AC-07.4/07.5; D-05/13 |
| C-14 | Apply / adjacent button для Status | Enabled тільки current assignee + інший allowed destination | T-14/T-15/T-16/T-17 → новий status на S-03 | AC-07.3; BR-08.1; D-06/13 |
| C-15 | Comment / multiline input | Видимий/editable усім authenticated users; також у Closed | Input → draft comment | US-06; AC-06.1 |
| C-16 | Add Comment / button | Видимий/enabled усім, включно з empty draft для перевірки validation | T-18 success, T-19 empty, T-20 save failure | AC-06.1–06.5; D-12 |
| C-17 | Return to Issues List / link або button | Видимий/enabled | T-10 → origin All/Important; предикат перераховано | D-07/10 |

Assignee Unassigned показується як відсутність. D-04 погоджує призначення/перепризначення, але не окрему дію зняття виконавця: Unassigned не додається як нова reset-операція. Це межа поточного дизайну, не універсальна заборона специфікації.

#### Component states

| State | Visible result / поведінка | Source / D |
|---|---|---|
| canonical | Lead non-assignee, ISS-003 Resolved/High, assignee Member A; C-09/C-11 доступні, C-13/C-14 disabled | AC-07.4; D-05 |
| new-issue | ISS-007 Open, Not Set, Unassigned; author/current user та created time присутні | AC-01.4/01.5; D-04 |
| unassigned | Status disabled для кожного користувача | DERIVED BR-08 + AC-07.4 |
| no-priority | Not Set видно, він не selectable reset | D-03; BR-04/05 |
| role-restricted | C-09–C-12 disabled для Member; C-13/C-14 disabled для non-assignee | US-03; AC-04.2/07.4; D-05 |
| Closed | Поточний Closed видно; немає наступного status. Comments та Lead assignee/priority автоматично не блокуються | BR-08.1; US-06; D-05/13 |
| comments-empty | Записів немає; форма додавання присутня | PROPOSED presentation; US-06 |
| comment-validation | Error «Comment cannot be empty»; нового запису немає | AC-06.1; D-12 |
| comment-saved | Новий запис: text, author/current user, date/time; input очищено за D-12 | AC-06.2–06.4; D-12 |
| comment-save-error | Error «Could not save comment»; нового запису немає; draft збережено за D-12 | AC-06.5; D-12 |

Incoming: T-02, T-09. Local actions: T-11–T-20; rejected/no-op cases T-21–T-24. Outgoing: T-10. Кожен Apply залишається на S-03. Статус не можна змінити обхідним шляхом через Lead permission; після reassignment право попереднього assignee втрачається.

V: поля, controls, матриця прав, state examples. P: конкретні wired Apply/comment routes і Return. I: persistence, атомарність, відсутність несанкціонованої зміни, повторний перегляд після реального збереження.

### 4.5. REF-01 — annotation frame

Не є продуктом або екраном нової ролі. Entry/exit: перегляд design file, без продуктової навігації. Inputs/C-ID відсутні. Test actor/issue ID/current status підписуються зовні продуктових frames, без user-facing role switcher.

| N-ID | Зміст / приклади | Source / D |
|---|---|---|
| N-01 | Authentication boundary; login/БД simulated; V/P/I distinction | BR-01, NFR-02; D-02/08 |
| N-02 | Чотири permission contexts §5; unassigned status disabled | US-03; AC-04.2/07.4; D-05 |
| N-03 | Повна матриця status transitions §6, включно з Closed | BR-08.1; AC-07.2/07.5 |
| N-04 | Important predicate, fixtures High+Resolved / Critical+Closed / Not Set | BR-09/09.1; AC-08.1–08.4 |
| N-05 | Create default/missing-title/missing-description/missing-both/new-issue result | AC-01.1–01.5; D-04/10/12 |
| N-06 | Comment ready/empty/saved/failure, author/time, відсутність нового запису при failure | AC-06.1–06.5; D-12 |
| N-07 | Not Set versus selectable priority; Return origin, Apply stays on details; NFR не доведено | BR-04/05; D-03/06/07; NFR-01–04 |

Компонентні приклади не потребують 16 повних копій S-03. Наявність annotation не замінює visible control, якщо вимога стосується самого продуктового екрана. Усі компоненти та frames мають бути редагованими; це критерій майбутнього Figma deliverable, а не вже отриманий результат.

## 5. Permission matrix

Для всіх колонок передумова — користувач автентифікований; assignee є поточним відношенням до issue, не глобальною роллю.

| Дія | Member non-assignee | Member assignee | Lead non-assignee | Lead assignee | Source |
|---|---|---|---|---|---|
| View list/details | Так | Так | Так | Так | US-02 |
| Create issue | Так | Так | Так | Так | BR-02 |
| Comment | Так | Так | Так | Так | US-06 |
| Assign/reassign | Ні | Ні | Так | Так | US-03; D-04 |
| Change priority | Ні | Ні | Так | Так | BR-06; AC-04.2 |
| Change status | Ні | Лише BR-08.1 | Ні | Лише BR-08.1 | BR-08; AC-07.4 |

Для Closed дозволених наступних статусів немає. Для unassigned status нікому не доступний. UI disabled — D-05; серверна заборона потребує I-тесту. Для view/create відношення assignee не є необхідною умовою.

## 6. Повна матриця status transitions

Умова кожного дозволеного переходу: actor == current assignee. SOURCE BR-08.1; права BR-08 + AC-07.4.

| From / To | Open | In Progress | Resolved | Closed |
|---|---|---|---|---|
| Open | Поточний, не перехід | Дозволено T-14 | Заборонено | Заборонено |
| In Progress | Заборонено | Поточний, не перехід | Дозволено T-15 | Заборонено |
| Resolved | Заборонено | Дозволено T-16 | Поточний, не перехід | Дозволено T-17 |
| Closed | Заборонено | Заборонено | Заборонено | Поточний, не перехід |

Значення поза чотирма статусами також недопустимі за AC-07.5. Матриця переходів перевіряється окремо від membership у переліку: валідне значення Closed не означає дозволений Open → Closed.

## 7. Important predicate

`isImportant(issue) = issue.priority in {High, Critical} AND issue.status != Closed`

| Priority | Status | У Important? | Пояснення |
|---|---|---|---|
| High | Resolved | Так | Resolved не Closed; BR-09.1 |
| Critical | Closed | Ні | AC-08.4 |
| Not Set | Open | Ні | Відсутність не є High/Critical |
| High | Open | Так | AC-08.1 |
| Critical | In Progress | Так | AC-08.2 |
| Low / Normal | Open / In Progress / Resolved | Ні | AC-08.3 |

При зміні priority/status у S-03 список Important наступного разу відображає актуальний результат предиката. D-07 зберігає вкладку, а не зобов’язує зберігати рядок, який перестав відповідати фільтру. Після Create з Important нова Not Set заявка до Important не входить, але є в All. V перевіряє fixture; P — підготовлений результат, якщо wired; I — довільні дані та реальну фільтрацію.

## 8. Traceability: усі 33 AC

UIR-01–UIR-33 — локальні одиниці перевірки, не нові продуктові вимоги. У колонці Level наведено запланований рівень, а не результат. Для SOURCE ID розділ джерела — §5 специфікації, якщо не вказано інше.

| Source ID / пункт | UIR-ID | Screen/State | C-ID / annotation | Test ID | Level |
|---|---|---|---|---|---|
| AC-01.1 | UIR-01 | M-01 default | C-05/06/07 | TEST-01 | V/P; I для справжнього input |
| AC-01.2 | UIR-02 | M-01 missing-title | C-05/07, N-05 | TEST-02 | V/P/I |
| AC-01.3 | UIR-03 | M-01 missing-description | C-06/07, N-05 | TEST-03 | V/P/I |
| AC-01.4 | UIR-04 | S-03 new | C-07, N-05 | TEST-04 | V/P fixture; I автоматичні дані |
| AC-01.5 | UIR-05 | S-03 new | C-11, N-05/07 | TEST-04/05 | V/P fixture; I initial value |
| AC-02.1 | UIR-06 | S-02-A | C-01 | TEST-06 | V/P; I доступ/дані |
| AC-02.2 | UIR-07 | S-02-A/B | C-04, таблиця полів | TEST-07 | V; P/I вибрані дані |
| AC-02.3 | UIR-08 | S-02 → S-03 | C-04 | TEST-08 | P; V link intent |
| AC-02.4 | UIR-09 | S-03 | C-09/11/13, таблиця полів | TEST-09 | V/P; I реальні дані |
| AC-02.5 | UIR-10 | S-02-C | C-03, empty message | TEST-10 | V/P; I empty dataset |
| US-03, AC, пункт 1 | UIR-11 | S-03 assigned | C-09/10 | TEST-11 | V/P/I |
| US-03, AC, пункт 2 | UIR-12 | S-03 selector | C-09, N-02 | TEST-12 | V/P; I membership |
| US-03, AC, пункт 3 | UIR-13 | S-03 role-restricted | C-09/10, N-02 | TEST-13 | V/P; I authorization |
| US-03, AC, пункт 4 | UIR-14 | S-03 assigned | C-09, visible assignee | TEST-11/14 | V/P; I persistence |
| AC-04.1 | UIR-15 | S-03 priority | C-11/12, N-07 | TEST-15 | V/P; I validation |
| AC-04.2 | UIR-16 | S-03 role-restricted | C-11/12, N-02 | TEST-16 | V/P; I authorization |
| AC-05.1 | UIR-17 | S-02, S-03 | Status column, C-13 | TEST-17 | V/P; I актуальність |
| AC-05.2 | UIR-18 | S-03 | C-13 | TEST-17 | V/P; I актуальність |
| AC-05.3 | UIR-19 | S-02-A/B | Status column | TEST-17 | V/P; I актуальність |
| AC-06.1 | UIR-20 | S-03 comment-validation | C-15/16, N-06 | TEST-18 | V/P/I |
| AC-06.2 | UIR-21 | S-03 comment-saved | C-15/16, N-06 | TEST-19 | V/P fixture; I storage |
| AC-06.3 | UIR-22 | S-03 comment-saved | Comment author, N-06 | TEST-19 | V/P fixture; I identity |
| AC-06.4 | UIR-23 | S-03 comment-saved | Comment created at, N-06 | TEST-19 | V/P fixture; I time/storage |
| AC-06.5 | UIR-24 | S-03 comment-save-error | C-15/16, N-06 | TEST-20 | V/P failure fixture; I transactional save |
| AC-07.1 | UIR-25 | S-03 new | C-13, N-05 | TEST-04 | V/P fixture; I default |
| AC-07.2 | UIR-26 | S-03, REF-01 | C-13, N-03 | TEST-21 | V/P; I enum validation |
| AC-07.3 | UIR-27 | S-03 updated | C-13/14 | TEST-22/23/24/25/26 | V state; P simulation; I persistence |
| AC-07.4 | UIR-28 | S-03 role-restricted | C-13/14, N-02 | TEST-27/28 | V/P; I authorization |
| AC-07.5 | UIR-29 | S-03 selector | C-13, N-03 | TEST-21/29 | V/P; I rejected invalid input |
| AC-08.1 | UIR-30 | S-02-B | C-02, N-04 | TEST-30 | V/P fixture; I predicate |
| AC-08.2 | UIR-31 | S-02-B | C-02, N-04 | TEST-31 | V/P fixture; I predicate |
| AC-08.3 | UIR-32 | S-02-B | C-02, N-04 | TEST-32 | V/P fixture; I predicate |
| AC-08.4 | UIR-33 | S-02-B | C-02, N-04 | TEST-33 | V/P fixture; I predicate |

### Додаткова простежуваність BR, D та NFR

| Source / decision | Місце / controls | Tests / level |
|---|---|---|
| BR-01; NFR-02; D-02 | S-01, N-01; демонстрація S-02 | TEST-36; V/P intent, I authentication |
| BR-02; D-01 | C-03/05–08; S-02/M-01 | TEST-01/10/34; V/P/I |
| BR-03/04/05; D-03/04 | S-03 new; C-09/11/13; N-05/07 | TEST-04/05/15/32 |
| BR-06; US-03; D-05 | C-09–12; N-02 | TEST-11–16 |
| BR-07/08/08.1 | C-13/14; N-02/03 | TEST-21–29 |
| BR-09/09.1 | S-02-B; N-04 | TEST-30–33 |
| BR-10/11; Deferred/Future §8 | Відсутність delete/history/attachments/AI | TEST-38; V scope review |
| D-04 reassignment | C-09/10 | TEST-14/28 |
| D-06 | C-10/12/14; S-03 після успіху | TEST-11/15/22–25 |
| D-07; D-10 | C-08/17, origin tab | TEST-34/35 |
| D-08 | Усі fixtures та N-01/07 | Усі P-тести — лише симуляція; TEST-36/37 |
| D-09–D-14 PROPOSED | Controls та states §4 | Перевірити й прийняти/відхилити на G4, не ставити APPROVED автоматично |
| NFR-01 | N-07 | TEST-37; I performance < 1 s |
| NFR-03 | N-07 | TEST-37; I HTTPS |
| NFR-04 | N-07 | TEST-37; I backup/restore |

## 9. Acceptance test plan

**Для кожного рядка:** Status = NOT RUN. Контекст — навчальні users/fixtures §3. Action означає дію у P лише якщо вона фактично wired; для V перевіряється зображений стан. Відсутній wired шлях не отримує PASS через наявність screenshot. У I потрібні реальні дії та дані.

| Test ID | Actor / context | Preconditions | Action | Expected visible result | Що тест V/P не доводить |
|---|---|---|---|---|---|
| TEST-01 | Member A, повторити Lead | M-01 відкритий | Ввести Title/Description у C-05/06 | Обидва поля editable, draft видно, немає полів автоданих | Реальну обробку input у backend |
| TEST-02 | Member A | Title empty, Description заповнений | C-07 | M-01 missing-title; «Title is required»; без нового issue | Серверну validation/persistence |
| TEST-03 | Member A | Title заповнений, Description empty; повторити both empty | C-07 | Missing Description; у both-empty обидві помилки; без нового issue | Backend validation |
| TEST-04 | Member A, повторити Lead | Valid Title/Description | C-07 → T-09 | S-03 new: ID, Open, current user author, created time, Not Set, Unassigned | Справжнє створення, унікальність, джерело часу, storage |
| TEST-05 | Lead | S-03 new Not Set | Перевірити current priority та відкрити C-11 | Not Set видно; selectable лише чотири рівні; reset відсутній | Технічне null/enum представлення |
| TEST-06 | Member A/Lead | Dataset ISS-001–006 | Відкрити All | Усі шість записів, зокрема Closed | Реальну authorization та completeness БД |
| TEST-07 | Member A | S-02-A/B | Перевірити всі рядки | ID/Title/Status/Priority; assignee або Unassigned; без вигаданої metadata | Коректність даних backend |
| TEST-08 | Member A | Існує ISS-003 у All та Important | C-04 з обох вкладок | S-03 саме ISS-003; Title/дані відповідають вибраному ID | Коректну маршрутизацію будь-якого реального ID |
| TEST-09 | Member A | S-03 ISS-003 | Перевірити всі поля §4.4 | Повні Title/Description, ID/Status/Priority/Assignee/Author/Created at | Реальне завантаження/збереження |
| TEST-10 | Усі три users | Empty fixture | Відкрити S-02-C; C-03 | Empty All, Create доступний; modal відкривається | Реальний запит порожньої БД |
| TEST-11 | Lead | S-03 Unassigned | Вибрати Member A, C-10 | Один assignee Member A у S-03, користувач залишається тут | Membership validation та storage |
| TEST-12 | Lead | C-09 відкритий | Переглянути доступні options | Лише Member A, Member B, Lead; single select; немає сторонніх users | Server-side membership checks |
| TEST-13 | Member A/B, assignee/non-assignee | S-03 у кожному контексті | Перевірити/спробувати C-09/10 | Disabled, assignee не змінено | Захист від прямого API request |
| TEST-14 | Lead | Assignee Member A | Вибрати Member B → Apply | Єдиний assignee Member B; попередній не збережений як другий | Persistence після reload |
| TEST-15 | Lead | Not Set, потім встановлений priority | Вибрати/застосувати кожен із 4 рівнів | Лише Low/Normal/High/Critical; current value видно в S-03 | Серверну перевірку довільних значень |
| TEST-16 | Member A/B | Будь-яке assignee relation | Перевірити C-11/12 | Disabled, priority незмінний | Backend authorization |
| TEST-17 | Member A | Узгоджені fixtures списку й деталей | Зіставити status для кожного issue | Current status видно в списку та S-03, значення збігаються | Свіжість даних при конкурентних змінах |
| TEST-18 | Member A | S-03, comment draft empty | C-16 | Validation, жодного нового comment entry | Backend empty-check |
| TEST-19 | Member A, повторити Lead | Непорожній comment draft | C-16, success fixture | Текст, правильний author, date/time; input cleared за D-12 | Реальний запис, identity/time та persistence |
| TEST-20 | Member A | Непорожній draft, failure fixture | C-16 → T-20 | Save error; кількість saved comments не зростає; draft збережено за D-12 | Transaction rollback і справжній збій БД |
| TEST-21 | Assignee | По черзі кожен current status | Перевірити C-13 та N-03 | Чотири current status; options лише allowed destinations; невідомих немає | Backend enum validation |
| TEST-22 | Member A assignee | ISS-001 Open | In Progress → C-14 | Status In Progress у S-03 | Persistence реальної зміни |
| TEST-23 | Current assignee | In Progress | Resolved → C-14 | Resolved у S-03, не Closed | Persistence реальної зміни |
| TEST-24 | Current assignee | Resolved | In Progress → C-14 | Роботу поновлено, current In Progress | Persistence реальної зміни |
| TEST-25 | Current assignee | Resolved | Closed → C-14 | Current Closed, наступних transitions немає | Persistence та actual filtering |
| TEST-26 | Current assignee | Виконана зміна status | Return, знову відкрити той самий issue | Підготовлений новий status зберігається у route fixture; у I — після reload/relogin | V/P не доводять AC-07.3 storage |
| TEST-27 | Member non-assignee та Lead non-assignee | Assignee інший user | Перевірити/спробувати C-13/14 | Disabled для обох; Lead не має винятку | Server-side authorization |
| TEST-28 | Lead і Member A | Спочатку Unassigned, потім reassignment A → B | Перевірити контексти прав | Unassigned: нікому status; після A → B право у B, не A; Lead лише якщо він assignee | Динамічні права в реалізації |
| TEST-29 | Current assignee | Усі чотири current status | Звірити всі 16 клітин §6; invalid value «Archived» у I | Лише 4 allowed transitions; diagonal не перехід; Closed без виходу; Archived відсутній | Відсутній option не доводить backend rejection |
| TEST-30 | Member A | High+Open/In Progress/Resolved, High+Closed | C-02, перевірити набір | Перші три включені, Closed виключено; fixture ISS-003 видно | Реальний предикат на довільній БД |
| TEST-31 | Member A | Critical+Open/In Progress/Resolved/Closed | C-02 | Перші три включені, Closed виключено | Реальну фільтрацію |
| TEST-32 | Member A | Low, Normal, Not Set для всіх чотирьох status | C-02/перевірити N-04 та fixture | Жодне поєднання не включено | Виконання предиката на сервері |
| TEST-33 | Member A | Closed з кожним priority і Not Set | C-02 | Усі Closed виключені, зокрема Critical+Closed ISS-004 | Реальну фільтрацію |
| TEST-34 | Усі authenticated contexts | По черзі All, Important, Empty All | Create → Cancel | Повернення у точний calling state; нового issue немає | Реальну відсутність побічного запису |
| TEST-35 | Member A/Lead | Вхід у S-03 з обох tabs; також Create з Important | C-17; окремо змінити priority/status у fixture | Попередня вкладка збережена; видимий набір відповідає актуальному predicate; new Not Set не у Important | Реальне оновлення dataset |
| TEST-36 | Рецензент | S-01, REF-01, старт P | Перевірити boundary та запустити демо | Немає вигаданого login; старт S-02-A; simulation позначено | Справжню автентифікацію NFR-02 |
| TEST-37 | Рецензент / developer | N-07; згодом реалізована система | V: перевірити межі; I: performance, HTTPS, backup/restore | V: NFR явно outstanding; I: результати вимірювань/відновлення фіксуються окремо | V/P не доводять NFR-01/03/04 |
| TEST-38 | Рецензент | Усі surfaces | Scope review та перевірка ролей | Немає delete/history/attachments/AI/нових ролей або окремих сторінок assignment/priority/status/comments | Поведінку прихованих API |

Тести TEST-30/31/32/33 параметризовані: перелічені поєднання мають бути перевірені в annotation matrix V; лише фактично наявні wired fixtures перевіряються P. Для повного автоматичного покриття предиката потрібен I-тест усіх 5 станів priority × 4 status.

## 10. Перевірка підготовленого контракту та наступний крок

Під час формалізації AI перевірено наявність 33 рядків Traceability, 4 ненумерованих пунктів US-03, чотирьох permission contexts, повної status matrix та окремого обліку Not Set/Resolved. Це самоперевірка тексту, не незалежний review або PASS майбутнього макета.

Перед Figma на G4 потрібно:
1. Звірити контракт зі специфікацією та перевірити всі 33 AC, не лише кількість рядків.
2. Розглянути D-09–D-14; прийняти, змінити або відхилити та оновити Decision Log.
3. Визначити, які маршрути реально зв’язуються P, а які представлені тільки V; майбутній протокол не має називати static examples пройденими кліками.
4. Зафіксувати автора, спосіб і результат контролю A/B та знайдені дефекти. Не вигадувати перевірки, яких не виконували.
5. Підготувати фінальний Figma brief тільки після усунення блокувальних питань.

Screen Inventory не розширено: S-01; S-02-A/B/C; M-01; S-03; REF-01 — 7 демонстраційних frames, 2 продуктові екрани та один modal. Додаткові component variants не є новими продуктовими екранами.
