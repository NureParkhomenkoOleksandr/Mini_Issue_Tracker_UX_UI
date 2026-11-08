# G6 — Review Report: Mini Issue Tracker

Версія: 1.1 — повторний візуальний аудит та додане посилання автора на Figma. Named version і доступ ще не підтверджені.  
Дата: 08.11.2026  
Reviewer: ChatGPT у цьому самому чаті.  
Прототипні результати: повідомлення автора роботи; кліки незалежно не виконувалися.

## 1. Джерела, версії та читабельність первинного огляду

Вимоги: SD_Spec.docx.pdf (§3/5/8); 01_Input_Pack_v1.0.md; Decision_Log.md 1.1; 03_Screen_Contracts_v1.0.md; історичний 05_Figma_Brief_v1.0.md. Попередні зображення 07.11.2026 використовуються лише як історія, не як доказ стану зміненого REF-01.

Поточні докази — надані автором PNG від 08.11.2026:

| Surface / state | Файл | Читабельність та висновок |
|---|---|---|
| S-01 | S-01.png | Межа authentication читається; не login form |
| S-02-A | S-02-A.png | Читабельні 8 baseline records, усі колонки |
| S-02-B | S-02-B.png | Читабельні 4 Important records |
| S-02-C | S-02-C.png | Читабельний empty All, Create доступний |
| S-03 | S-03.png | Читабельні деталі ISS-003, controls та comment |
| S-03 new | S-03-CREATED.png; S-03-CREATED-FROM-EMPTY.png | Читабельні ISS-009, Title/Description, Open, Not Set, author/time; Assignee порожній |
| M-01 default/valid | M-01-DEFAULT.png; M-01-VALID.png; M-01-VALID-FROM-EMPTY.png | Поля та кнопки читаються; Title став однорядковим |
| M-01 before/error | M-01-BEFORE-ERR-TITLE..png; M-01-ERR-TITLE.png; M-01-BEFORE-ERR-DESC.png; M-01-ERR-DESC.png | Обидва окремі validation outcomes читаються |
| All after create | S-02-A-AFTER-CREATE.png | 8 старих записів + нова ISS-009 |
| Empty after create | S-02-C-AFTER-CREATE.png | Лише ISS-009; попри C в назві це populated All, не порожній стан |
| REF-01 | REF-01.png | Загальна структура видима; дрібний текст недостатній для надійного детального аудиту |
| Connection overview | image(20261108-125047).png | Зв’язки видно, біля Return помітний Back; усі destinations/settings не читаються |

Статуси:
- **PASS — visual:** потрібний статичний доказ видно; не означає реалізацію.
- **PASS — reported:** автор повідомив про успішні кліки; незалежно не спостережено.
- **PARTIAL:** видно лише частину вимоги або контексту.
- **FAIL — design:** видно суперечність погодженому дизайну.
- **NOT VERIFIABLE:** поточних доказів недостатньо або потрібна реалізація.

## 2. Навчальні дані та зміна fixtures (порожні labels згодом виправлено, §8)

| ID | Title | Status | Priority | Assignee у PNG | У Important |
|---|---|---|---|---|---|
| ISS-001 | Login fails | Open | Critical | Member A | Так |
| ISS-002 | Search results do not load | In Progress | High | Member B | Так |
| ISS-003 | Profile update fails | Resolved | High | Member A | Так |
| ISS-004 | Payment page crashes | Closed | Critical | Member B | Ні |
| ISS-005 | Button label is unclear | Open | Normal | Порожньо | Ні |
| ISS-006 | Settings page freezes | Open | Not Set | Порожньо | Ні |
| ISS-007 | Report download fails | Resolved | Critical | Lead | Так |
| ISS-008 | Footer spacing is uneven | In Progress | Low | Member A | Ні |
| ISS-009 | Notifications panel does not open | Open | Not Set | Порожньо | Ні; нова заявка |

У деталях ISS-003: Description — “Saving an updated display name returns an error.”; Author Member B; Created at 2026-11-03 11:00; comment Member A, 2026-11-07 10:30, “The fix is ready for verification.”

У формі та деталях ISS-009 збігаються Title та Description — “Clicking the notifications button does not open the panel.”; Author Member A; Created at 2026-11-07 12:00. Це фіксовані fixture values, не доказ роботи годинника, автоматичної генерації або реального створення.

Змінено fixtures, а не продуктові функції: згадування notifications/search/payment у тексті заявки не означає додавання цих функцій у сам tracker. Нові назви не є бізнес-дефектом, якщо стани між frames узгоджені. Brief 1.0 з ISS-007 new і canonical Lead зберігається як історичний вхід генерації; не переписується заднім числом. Поточна відповідність задокументована тут. Поточний actor має бути явно підписаний у review annotation: автора заявки недостатньо для визначення того, хто її зараз переглядає.

## 3. Part A — первинний результат для 33 AC (до додаткових доказів)

V = screenshot design; P = reported prototype; I = implementation outstanding. Для кожного номера джерело — §5 специфікації. Посилання на PNG — §1 цього документа.

| Source | Expected | Screen/State | Observed evidence | Result | Remaining test |
|---|---|---|---|---|---|
| AC-01.1 | Title та Description вводяться | M-01 default/valid | Обидва поля та заповнені fixtures видно | PASS — visual; P-04 reported | I: реальний input/create |
| AC-01.2 | Title required, без нього не створювати | M-01-ERR-TITLE | Title is required; відповідний before-state | PASS — visual; P-07 reported | I: server validation; both-empty окремо |
| AC-01.3 | Description required | M-01-ERR-DESC | Description is required; Title збережений | PASS — visual; P-07 reported | I: validation |
| AC-01.4 | ID/Open/author/created_at після Create | S-03-CREATED | ISS-009, Open, Member A, 2026-11-07 12:00 | PASS — visual fixture; P-04 reported | I: automatic/unique ID, author identity, time, storage |
| AC-01.5 | Priority не встановлено | S-03-CREATED | Not Set | PASS — visual fixture | I: реальне початкове значення |
| AC-02.1 | Перегляд списку | S-02-A | 8 baseline records; updated list з 9 | PASS — visual | I: authenticated access, повнота даних |
| AC-02.2 | ID/Title/Status/Priority/Assignee за наявності | S-02-A/B | Усі колонки; призначені виконавці видно | PASS — visual | I: реальні дані; D-11 окремо має дефект |
| AC-02.3 | Вибір → деталі правильного issue | S-02-A/B → S-03 | ISS-003 збігається між списками та деталями | PASS — visual; P-01/02 reported | I: довільні ID; незалежний P walkthrough |
| AC-02.4 | Усі поля деталей | S-03 | ID/Title/Description/Status/Priority/Assignee/Author/Created at | PASS — visual | I: actual data; actor annotation уточнити |
| AC-02.5 | Empty list або повідомлення | S-02-C | No issues yet, немає рядків | PASS — visual; P-06 reported для success-route | I: empty dataset; Cancel з empty не підтверджено |
| US-03, AC, пункт 1 | Один assignee | S-03 | Одне поле з Member A | PARTIAL | Читабельні options/single-select example; P/I assignment |
| US-03, AC, пункт 2 | Assignee є членом команди | S-03 / REF-01 | Member A видно; повний список options не читається | PARTIAL | Options усіх трьох users; I membership checks |
| US-03, AC, пункт 3 | Призначати може лише Lead | S-03 / REF-01 | Assignment available, current actor явно не показаний | NOT VERIFIABLE | Чотири permission contexts у читабельному REF; I authorization |
| US-03, AC, пункт 4 | Поточний assignee видно | S-03 | Member A | PASS — visual | P assignment update; I persistence |
| AC-04.1 | Лише Low/Normal/High/Critical | S-02 / S-03 | У даних є рівні та Not Set; dropdown options не показано | PARTIAL | Читабельні options без selectable Not Set; I validation |
| AC-04.2 | Priority змінює лише Lead | S-03 / REF-01 | Priority available, actor не визначено | NOT VERIFIABLE | Permission contexts; I authorization |
| AC-05.1 | Current status кожного issue видно | S-02 / S-03 | Statuses у рядках та деталях | PASS — visual | I: актуальність після реальних змін |
| AC-05.2 | Status у деталях | S-03 / new | Resolved для ISS-003, Open для ISS-009 | PASS — visual | I: actual data |
| AC-05.3 | Status у списку | S-02-A/B/after-create | Status column заповнена | PASS — visual | I: actual data |
| AC-06.1 | Empty comment не допускається | S-03 / REF-01 | Порожній input є; outcome у новому REF не читається | NOT VERIFIABLE | Читабельний empty-comment error або reported P |
| AC-06.2 | Saved comment показаний і збережений | S-03 | Існуючий comment показаний | PARTIAL | Окремий new-comment success; I storage |
| AC-06.3 | Author comment показаний і збережений | S-03 | Member A | PASS — visual existing entry | I: identity/storage; новий success example |
| AC-06.4 | Creation date/time comment показані і збережені | S-03 | 2026-11-07 10:30 | PASS — visual existing entry | I: time/storage |
| AC-06.5 | Failed save → error, без нового comment | REF-01 | Потрібний outcome недостатньо читається | NOT VERIFIABLE | Читабельний failure fixture; I transactional failure |
| AC-07.1 | Нове issue Open | S-03-CREATED / new lists | ISS-009 Open | PASS — visual fixture; P-04 reported | I: реальний default |
| AC-07.2 | Чотири допустимі статуси | S-02-A | Open/In Progress/Resolved/Closed представлені | PASS — visual values | I validation; current-status options окремо |
| AC-07.3 | Новий status зберігається для повторного перегляду | REF-01 | Читабельного before/after status route не надано | NOT VERIFIABLE | P status route та repeat view; I persistence |
| AC-07.4 | Non-assignee не змінює status | S-03 | Status disabled, actor явно не підписаний | PARTIAL | Чотири контексти та unassigned; I permission checks |
| AC-07.5 | Невідомий status не допускається | REF-01 / selector | Dropdown options не показані читабельно | NOT VERIFIABLE | Читабельні destinations; I invalid-input rejection |
| AC-08.1 | High і не Closed входить | S-02-B | ISS-002 In Progress/High та ISS-003 Resolved/High | PASS — visual fixture | I: arbitrary dataset filtering |
| AC-08.2 | Critical і не Closed входить | S-02-B | ISS-001 Open/Critical; ISS-007 Resolved/Critical | PASS — visual fixture | I: arbitrary dataset filtering |
| AC-08.3 | Low/Normal виключені | S-02-A/B | ISS-005 Normal і ISS-008 Low відсутні у Important; Not Set теж | PASS — visual fixture | I: actual filtering |
| AC-08.4 | Closed виключений незалежно від priority | S-02-A/B | ISS-004 Closed/Critical відсутній у Important | PASS — visual fixture | I: усі комбінації |

## 4. Первинна оцінка BR/D/NFR та межі доказів

| Source / expected | Доказ / результат | Залишається |
|---|---|---|
| BR-01, D-02: authentication boundary | S-01 нейтральна межа — PASS visual; login не доведено | I: authentication |
| BR-02, D-01: Create доступний членам команди, modal | Create є у списках; modal exports та routes reported | Права всіх трьох actors не доведено PNG |
| BR-03/04, D-04: new Open/absent priority/assignee | ISS-009 Open, Not Set, assignee порожній; default values видимі, але D-11 display порушено | I defaults; виправити label |
| BR-05/06, D-03: чотири priority levels, лише Lead | Значення показані, options/role matrix нової версії не читаються — PARTIAL | REF та I |
| BR-08/08.1: assignee-only, лише чотири transitions | Current Status disabled у S-03; актуальна повна матриця не читається — PARTIAL | Читабельний REF; I authorization/transitions |
| BR-09/09.1: Resolved не Closed | У Important є High/Critical Resolved, немає Critical Closed — PASS visual | I predicate |
| BR-10/11: немає delete/history | У наданих основних frames таких controls не видно — PASS visual scope check | Повний layer audit не виконано |
| D-05: forbidden controls disabled | Disabled видно, але current actor не позначено — PARTIAL | Permission contexts |
| D-06/13: Apply після іншого допустимого вибору | C-10/C-12 виглядають enabled з поточними значеннями; staged контекст не показаний — потребує уточнення | Q-UI-01; див. findings |
| D-07/10: origin-preserving Return, Create result | P-01–P-06 PASS reported у межах описаних маршрутів | Create success з Important → Return ще не підтверджено |
| D-08: simulated data | Підготовлені before/error/valid/new/after-create frames представлені | Це не storage |
| D-09: Title link | Підкреслені Titles; ISS-003 detail routes reported | Усі інші рядки не протестовані |
| D-11: Unassigned label | Assignee порожній у new/list — FAIL design display | DEF-01 |
| D-12: errors та comment input outcomes | Missing Title/Description тексти видно; нові comment outcomes не читаються — PARTIAL | Читабельний REF |
| D-14: compact state reference | REF-01 існує; повний content недостатньо читається — PARTIAL | Export sections; layer naming не перевірено |
| NFR-01–04 | NOT VERIFIABLE: actual response time, login, HTTPS, backup/restore | Реалізація та технічні тести |

## 5. Історичні findings первинного огляду; актуальні статуси — §8

| ID | Клас / severity | Location | Source | Evidence | Minimal correction / статус |
|---|---|---|---|---|---|---|
| DEF-01 | Порушення погодженого display / Minor | S-03-CREATED, S-03-CREATED-FROM-EMPTY, unassigned rows у S-02-A та after-create | D-11 | Замість Unassigned показано порожнє поле/cell | Додати Unassigned у всі відповідні відсутні значення; перевірити read-only/disabled presentation. OPEN |
| Q-UI-01 | Контекст staged values / Medium, не підтверджений бізнес-дефект | S-03 C-10/C-12 | D-13 | Apply виглядає enabled біля Member A/High, але немає доказу іншого staged значення | Якщо це initial state — disabled до зміни; якщо staged — підписати actor/current saved values/staged values зовні продуктового frame. OPEN |
| Q-EV-01 | Прогалина доказів / до завершення review | REF-01.png | AC-06.1/06.5, AC-07.4/07.5, BR-08.1 | Текст нового REF дрібний | Надати читабельні permission/status/comment/priority sections. Це не доказ відсутності станів у Figma. OPEN |
| DOC-01 | Синхронізація fixtures / інформаційне | Поточні PNG vs історичний brief | Узгодженість версій | 8 baseline + ISS-009 замість 6 baseline + ISS-007 | Поточну таблицю збережено в §2; історію генерації не переписано. DOCUMENTED |

UX: поле Title у новому modal однорядкове — попереднє необов’язкове зауваження до його висоти більше не актуальне. Окремих нових косметичних правок не пропонується без потреби. Огляд не є accessibility certification або user testing.

## 6. Part P — підсумок прототипу

Prototype_Test_Record.md містить сім сценаріїв PASS — reported. Вкладки All ↔ Important також підтверджені автором раніше. Загальний screenshot connections узгоджується з наявністю прототипних зв’язків, але не доводить settings кожного маршруту.

Приклади assignment/status/comments у REF не отримують PASS P автоматично. Усі не підтверджені користувачем TEST-ID залишаються NOT RUN або NOT VERIFIABLE відповідно до рівня перевірки. Прохід P не доводить backend persistence.

## 7. Історичний висновок первинного огляду; замінено результатом §8

1. **UI design coverage — PARTIAL за поточними доказами.** Основні екрани, Create validation, Important та new-issue states читаються; новий REF потребує читабельного export. Є DEF-01 і невизначеність Q-UI-01.
2. **Prototype evidence — REPORTED**, сім сценаріїв підтверджені автором, незалежний walkthrough не виконано.
3. **Implementation tests — OUTSTANDING:** authentication, server permissions, persistence, automatic ID/time, real filtering, response time < 1 s, HTTPS, backup/restore.

Не оголошується «всі AC виконано». Для завершення: автор приймає/відхиляє findings із причиною, робить потрібні правки, повторно перевіряє змінені стани, надає читабельний REF та посилання на точну версію Figma. Після правок цей report оновлюється, а зміни після останнього AI-review позначаються явно.


## 8. Повторна перевірка виправлень — актуальний результат

Дата: 08.11.2026. Reviewer: ChatGPT, аналіз наданих автором зображень. Повторний audit враховує шість нових основних exports та 20 читабельних фрагментів поточного REF-01. Наведені вище PARTIAL/OPEN через недостатню читабельність відображають первинний етап; актуальні results нижче їх замінюють. Історичні спостереження не видалено.

### 8.1. Докази виправлень основних frames

| Frame | Новий export | Видимий результат |
|---|---|---|
| S-03 | S-03 (1).png | Assignee Member A та Priority High доступні для вибору; їхні Apply disabled при unchanged values; Status Resolved і Apply disabled для canonical Lead non-assignee |
| S-03-CREATED | S-03-CREATED (1).png | ISS-009, Open, Not Set, Unassigned; усі керуючі controls disabled у Member A context без assignee |
| S-03-CREATED-FROM-EMPTY | S-03-CREATED-FROM-EMPTY (1).png | Той самий новий issue та коректне Unassigned |
| S-02-A | S-02-A (1).png | Unassigned у ISS-005/006, решта baseline даних збережена |
| S-02-A-AFTER-CREATE | S-02-A-AFTER-CREATE (1).png | 9 records; Unassigned у ISS-005/006/009 |
| S-02-C-AFTER-CREATE | S-02-C-AFTER-CREATE (1).png | Єдина ISS-009 із Unassigned |

Перевірка PNG підтверджує видиму зміну; не доводить програмної disabled-поведінки або збереження prototype connections. Сім раніше підтверджених автором маршрутів залишаються історичними PASS — reported до останніх правок; повторний walkthrough після правок ще не повідомлений.

### 8.2. Повторна оцінка REF-01

Читабельні screenshots від Screenshot 2026-11-08 154713.png до Screenshot 2026-11-08 155107.png надані як частини одного актуального REF-01. Перевірено:

- Чотири role/assignee contexts: Member і Lead × assignee/non-assignee. Лише Lead має assignment/priority; status лише assignee; у Lead non-assignee status disabled.
- Single-assignee options: Member A, Member B, Lead. Є assignment та reassignment before/pending/applied без multi-assignee.
- Priority options: Low/Normal/High/Critical. Not Set окремо пояснено як display absence, не selectable/reset.
- Чотири current statuses та всі дозволені transitions. Open → In Progress; In Progress → Resolved; Resolved → In Progress; Resolved → Closed. У Closed немає destinations.
- Unassigned не дає нікому права status. Closed не вимикає автоматично comments або Lead assignment/priority.
- Initial Apply disabled, pending дозволений вибір робить Apply enabled, applied value знову має disabled Apply, доки немає іншої зміни.
- Comment ready/empty/saved/error; saved містить Member B, 2026-11-07 12:30 та “I will check the fix today.”; при failure нового entry немає, draft збережено.
- Both-fields-empty Create reference із двома errors; success не показаний як наслідок invalid input.
- Important before/after closing: після Closed у ISS-003 він виключений, залишаються ISS-001/002/007; High/Critical Resolved до закриття включені.
- Populated creation зберігає 8 старих rows та додає ISS-009; independent empty creation дає лише ISS-009. Сценарії не об’єднані в нібито один history stream.

Ці приклади — **PASS visual**, а не PASS P або I. Кліки Apply/status/comments не отримують нового reported PASS лише через надані before/pending/applied images.

### 8.3. Актуальне UI-покриття всіх 33 AC

PASS visual тут означає, що необхідне представлення поля/правила/стану видно в screenshots або review reference. Умови про реальне збереження, authentication та server authorization усе одно потребують I. Не слід читати цю таблицю як «реалізація всіх AC завершена».

| Source | Поточний результат | Новий/збережений доказ | Поза доведеним |
|---|---|---|---|
| AC-01.1 | PASS — visual | M-01 Title/Description; prepared valid inputs | I input/create |
| AC-01.2 | PASS — visual | Missing Title і both-empty reference | I validation |
| AC-01.3 | PASS — visual | Missing Description і both-empty reference | I validation |
| AC-01.4 | PASS — visual | ISS-009 ID/Open/author/time | I auto-ID, author/time, persistence |
| AC-01.5 | PASS — visual | New priority Not Set | I default |
| AC-02.1 | PASS — visual | All/Important lists | I access/data |
| AC-02.2 | PASS — visual | П’ять columns, Unassigned labels виправлено | I actual data |
| AC-02.3 | PASS — visual | Titles + reported P-01/02 | I routing; P після останніх правок не повторено |
| AC-02.4 | PASS — visual | S-03 усі required detail fields | I actual data |
| AC-02.5 | PASS — visual | Empty All message; independent populated result | I empty data |
| US-03, AC, пункт 1 | PASS — visual | Single select та before/pending/applied reference | P/I assignment |
| US-03, AC, пункт 2 | PASS — visual | Options Member A/Member B/Lead | I membership |
| US-03, AC, пункт 3 | PASS — visual | Чотири permissions contexts; Member disabled | I authorization |
| US-03, AC, пункт 4 | PASS — visual | Current assignee та applied update видно | I persistence |
| AC-04.1 | PASS — visual | Чотири selectable priority options | I validation |
| AC-04.2 | PASS — visual | Lead-only priority у чотирьох contexts | I authorization |
| AC-05.1 | PASS — visual | Statuses у списку та деталях | I freshness |
| AC-05.2 | PASS — visual | Current Status у S-03 та references | I actual data |
| AC-05.3 | PASS — visual | Status column у All/Important | I actual data |
| AC-06.1 | PASS — visual | Empty comment error, без new entry | P/I validation |
| AC-06.2 | PASS — visual | Saved success fixture додає entry | I storage; P не заявлено |
| AC-06.3 | PASS — visual | Новий entry має author Member B | I identity/storage |
| AC-06.4 | PASS — visual | Новий entry має creation date/time | I time/storage |
| AC-06.5 | PASS — visual | Error + retained draft, без нового saved entry | I failure/transaction |
| AC-07.1 | PASS — visual | ISS-009 Open | I default |
| AC-07.2 | PASS — visual | Усі чотири current statuses | I validation |
| AC-07.3 | PASS — visual | Before/pending/applied status fixtures | I persistence/revisit; P status route не заявлено |
| AC-07.4 | PASS — visual | Assignee-only; Lead non-assignee та unassigned disabled | I authorization |
| AC-07.5 | PASS — visual | Valid destinations reference; інші заборонені annotation | I invalid-value rejection |
| AC-08.1 | PASS — visual | High+Resolved та High+In Progress включені | I predicate |
| AC-08.2 | PASS — visual | Critical+Open/Resolved включені | I predicate |
| AC-08.3 | PASS — visual | Low/Normal/Not Set виключені | I predicate |
| AC-08.4 | PASS — visual | Closed/Critical виключено; ISS-003 зникає після closing fixture | I predicate |

### 8.4. Resolution findings

| ID | Актуальний статус | Підстава |
|---|---|---|
| DEF-01 | CLOSED — visual recheck | Unassigned підтверджено в усіх шести основних exports |
| Q-UI-01 | CLOSED — visual recheck | Initial Apply у S-03 disabled; staged/applied examples у REF читаються |
| Q-EV-01 | CLOSED — readability | Поточні permissions/status/priority/comment references надані крупними фрагментами |
| DOC-01 | DOCUMENTED | Фактичний набір 8+ISS-009 та current actors описані; historical brief збережено |
| DOC-02 | OPEN — wording only | У REF лишилися застарілі annotations про відсутність prototype wiring, «empty Assignee» та source range D-01–D-09. Потрібно оновити, не змінюючи frames або взаємодії; факт виконання ще не повідомлено |

DOC-02: запропонований текст — “Basic prototype navigation was connected manually. Reference examples show intended states; they do not prove working application logic.” Для display відсутнього виконавця — “Assignee displayed as Unassigned”; source range — D-01–D-14. Це documentation cleanup, не дефект прав чи продуктового scenario.

### 8.5. Відповідність Control IDs

Назви у новому REF змінилися, але source AC не перенумеровані. Ця таблиця зберігає Traceability без вимоги перейменувати дизайн.

| Screen Contracts 1.0 | Current REF ID | Control |
|---|---|---|
| C-01 | C-L01 | All tab |
| C-02 | C-L02 | Important tab |
| C-03 | C-L03 | Create Issue |
| C-04 | C-L04 | Issue Title |
| C-05 | C-M01 | Title input |
| C-06 | C-M02 | Description input |
| C-07 | C-M03 | Create |
| C-08 | C-M04 | Cancel |
| C-09 | C-D01 | Assignee select |
| C-10 | C-D02 | Assignee Apply |
| C-11 | C-D03 | Priority select |
| C-12 | C-D04 | Priority Apply |
| C-13 | C-D05 | Status select |
| C-14 | C-D06 | Status Apply |
| C-15 | C-D07 | Comment input |
| C-16 | C-D08 | Add Comment |
| C-17 | C-D09 | Return to Issues List |

### 8.6. Актуальний підсумок

- **UI design representation — COMPLETE для потрібних полів/правил/станів за сукупністю читабельних доказів.** Основні display findings закриті. Залишається DOC-02, редакційне уточнення annotations.
- **Prototype evidence — REPORTED**, сім scenarios + раніше підтверджені tabs; це результати до останніх правок. Збереження кліків після correction ще не підтверджено повторним проходженням.
- **Implementation — OUTSTANDING:** authentication, backend permissions, persistence, automatic IDs/time, real filtering, response time, HTTPS, backup/restore.
- **Layer structure — не перевірена незалежно.** Компоненти та editable/native/Auto Layout не доводяться PNG; початкові 98 instances були заявою Agent про попередню версію.
- Для здавання треба додати реальні Figma URL та назву/версію збереженого макета; вони ще не надані. Не вставляти вигадане посилання або стверджувати доступ викладача без перевірки.


## 9. Figma handoff — 08.11.2026

Автор надав [Design file — Mini Issue Tracker — Final](https://www.figma.com/design/d9CkiP4T6UUC2oXSpk8au7/Mini-Issue-Tracker-%E2%80%94-Final?node-id=0-1). Назва повідомлена як «Mini Issue Tracker — Final»; номер/назва Version history не надані, не додавати v1.1 до назви макета від імені автора.

URL містить node-id 0-1 та веде на Design file. Автоматичне відкриття посилання не вдалося, тому вміст live file, права доступу викладача та відповідність screenshots останній live-версії незалежно не перевірені. Підставою UI-review залишаються надані images.

Стан завершення: display findings закриті візуально; DOC-02 ще очікує підтвердження; regression після правок не повідомлений; real implementation/NFR outstanding. README.md підготовлено з точним посиланням та цими межами. Файл не оголошується повністю готовим до здавання лише через надання URL.
