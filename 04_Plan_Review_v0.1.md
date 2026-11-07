# G4 — Plan Review: Mini Issue Tracker

Версія: 0.1  
Дата: 07.11.2026  
Reviewer: ChatGPT у цьому самому чаті; це не незалежний рецензент.  
Метод: повторне читання вихідної специфікації та зіставлення змісту AC/BR із Input Pack, Screen Map, Screen Contracts, матрицями й тестами.

## 1. Перевірені матеріали та межі

- SD_Spec.docx.pdf: §1, §3, §5, §8; джерело доступне та повторно прочитане.
- 01_Input_Pack_v1.0.md; Decision_Log.md v1.0, APPROVED D-01–D-08.
- 02_Screen_Map_v0.1.md; 03_Screen_Contracts_v0.1.md.
- Методичні рекомендації §11–12: формат G4 та контроль B.

Перевірено зміст усіх 33 AC, а не тільки кількість рядків. COVERED означає наявність вимоги та запланованого доказу у тексті контракту, а не виконання тесту. Жоден макет, Figma layer або прототип у цій перевірці не оглядався: їх ще не надано.

## 2. Coverage matrix

| Source | Статус | Доказ у Screen Contracts | Змістовна перевірка |
|---|---|---|---|
| AC-01.1 | COVERED | M-01 C-05/06, TEST-01 | Лише Title і Description як inputs |
| AC-01.2 | COVERED | M-01 missing-title, TEST-02 | Title required; точний текст із Gherkin |
| AC-01.3 | COVERED | M-01 missing-description, TEST-03 | Description required; текст позначено UX-пропозицією |
| AC-01.4 | COVERED | S-03 new, TEST-04 | ID/Open/author/time відокремлені від inputs; автоматичність потребує I |
| AC-01.5 | COVERED | C-11, N-05/07, TEST-04/05 | Початковий priority відсутній, Not Set — display state |
| AC-02.1 | COVERED | S-02-A, TEST-06 | All доступний членам команди |
| AC-02.2 | COVERED | S-02 поля, TEST-07 | Усі п’ять потрібних полів, assignee за наявності |
| AC-02.3 | COVERED | C-04, T-02, TEST-08 | Відкриття деталей правильного ID |
| AC-02.4 | COVERED | S-03 таблиця полів, TEST-09 | ID/Title/Description/Status/Priority/Assignee/Author/Created at |
| AC-02.5 | COVERED | S-02-C, TEST-10 | Empty dataset без вигаданого error або delete |
| US-03, AC, пункт 1 | COVERED | C-09/10, TEST-11 | Один assignee; не multi-select |
| US-03, AC, пункт 2 | COVERED | C-09 options, TEST-12 | Лише три члени команди |
| US-03, AC, пункт 3 | COVERED | Permission matrix, TEST-13 | Призначає лише Lead; BR-06 не підміняє джерело цього права |
| US-03, AC, пункт 4 | COVERED | S-03 current assignee, TEST-11/14 | Поточний виконавець видимий |
| AC-04.1 | COVERED | C-11/12, TEST-15 | Чотири рівні; Not Set не п’ятий рівень |
| AC-04.2 | COVERED | Permission matrix, TEST-16 | Лише Lead; assignee status не дає priority permission |
| AC-05.1 | COVERED | S-02/S-03, TEST-17 | Поточний status у кожного issue |
| AC-05.2 | COVERED | S-03 C-13, TEST-17 | Status видно незалежно від права зміни |
| AC-05.3 | COVERED | S-02 Status column, TEST-17 | Status присутній у списку |
| AC-06.1 | COVERED | C-15/16, N-06, TEST-18 | Порожній comment не створюється |
| AC-06.2 | COVERED | Comment-saved, TEST-19 | Запис відображається; storage позначено рівнем I |
| AC-06.3 | COVERED | Comment author, TEST-19 | Author присутній; справжня identity потребує I |
| AC-06.4 | COVERED | Comment created at, TEST-19 | Дата/час присутні; справжнє збереження потребує I |
| AC-06.5 | COVERED | Comment-save-error, TEST-20 | Error і відсутність нового saved entry |
| AC-07.1 | COVERED | S-03 new, TEST-04 | Open при створенні |
| AC-07.2 | COVERED | Матриця §6, TEST-21 | Усі чотири статуси |
| AC-07.3 | COVERED | T-14–17, TEST-22–26 | Новий status та повторний перегляд; persistence не доводиться P |
| AC-07.4 | COVERED | Permission matrix, TEST-27/28 | Lead non-assignee не має права; unassigned теж враховано |
| AC-07.5 | COVERED | C-13, TEST-21/29 | Невідомий Archived відсутній; backend rejection тільки I |
| AC-08.1 | COVERED | S-02-B, TEST-30 | High + будь-який status крім Closed |
| AC-08.2 | COVERED | S-02-B, TEST-31 | Critical + будь-який status крім Closed |
| AC-08.3 | COVERED | N-04, TEST-32 | Low/Normal виключені, Not Set окремо враховано |
| AC-08.4 | COVERED | N-04, TEST-33 | Усі Closed виключені незалежно від priority |

Підсумок: **33 COVERED, 0 MISSING, 0 AMBIGUOUS щодо змісту вихідних AC**. Статуси UX-погодження та прототипного scope оцінено окремо нижче; вони не приховані цією матрицею.

## 3. Перевірка бізнес-правил та граничних сценаріїв

| Перевірка | Результат текстового review | Доказ |
|---|---|---|
| Scope визначено остаточним §8, а не Candidate MVP | Узгоджено | Input Pack §3; Contracts §1 |
| Lead не assignee на ISS-003 | Status disabled; право priority/assignee не дає status | Contracts §3–5; TEST-27 |
| Lead як assignee | Дозволені лише чотири переходи BR-08.1 | Матриці §5/6 |
| Open → Closed | Заборонено, хоча Closed є допустимим статусом | Матриця §6; TEST-29 |
| Resolved → In Progress | Дозволено поточному assignee | T-16; TEST-24 |
| Closed → будь-який інший status | Немає виходу | Матриця §6; TEST-25/29 |
| High + Resolved | Входить до Important | ISS-003; TEST-30 |
| Critical + Closed | Не входить до Important | ISS-004; TEST-33 |
| Not Set + Open | Не входить до Important; Not Set не selectable reset | ISS-006; TEST-05/32 |
| Unassigned | Ніхто не може змінити status до призначення | Contracts §5; TEST-28 |
| Member assignee | Status доступний за BR-08.1, але priority/assignee disabled | Permission matrix |
| Create з Important, потім Return | Origin Important збережено; нова Not Set заявка не з’являється там | D-10 proposal; Contracts §7; TEST-35 |
| Empty All → Create → Cancel | Повернення до empty без нового issue | T-05/T-06; TEST-34 |
| Comment save failure | Error; жодного нового saved comment | AC-06.5, TEST-20 |
| HTTPS/backup | Немає окремих продуктових екранів, I outstanding | N-07, TEST-37 |

Жодного критичного дефекту прав, незаконного status transition або втрати вихідного AC у тексті плану не виявлено. Це обмежений результат цього review, а не гарантія відсутності інших помилок.

## 4. Findings та мінімальні дії

### Вимогові дефекти

Підтверджених дефектів невідповідності вихідним AC/BR не виявлено. Штучні DEF-ID для відсутніх проблем не створюються.

### Питання готовності та UX-пропозиції

| Finding ID | Клас / важливість | Source | Місце | Проблема | Мінімальна дія / статус |
|---|---|---|---|---|---|
| REV-01 | Readiness / blocker для фінального brief | Методичні рекомендації §11–12 | Contracts §2 | D-09–D-14 ще PROPOSED; включати їх як остаточні правила у brief передчасно | Подати конкретні рішення на погодження автору роботи; OPEN |
| REV-02 | Verification planning / до початку P1 | Методичні рекомендації §17–18; Contracts §10 | TEST-01–38 | Для тестів розрізнено V/P/I, але мінімальний набір обов’язкових wired P-маршрутів ще не вибрано | Пропозиція нижче; не вимагати wiring усіх 38 тестів; OPEN |
| REV-03 | Process evidence / контроль B ще не виконано | Методичні рекомендації §11 | Усі draft artifacts | Немає запису людської перевірки матриць і граничних сценаріїв; цей AI-review не незалежний | Автор/інший учасник/викладач реально перевіряє наведені кейси та фіксує результат; OPEN |
| REV-04 | Fixture completeness / перед генерацією | Contracts §3/4.4 | Sample data | Title/status/priority/assignee задані, але повні Description/Author/Created at та конкретний comment example ще не заповнені | У фінальному brief підставити узгоджені фіктивні значення з чіткими labels; не справжні дані; OPEN до G5 |

REV-ID — локальні findings цього review. REV-01/03 не є новими бізнес-вимогами. REV-04 не означає втрату AC-02.4: поля в контракті є, конкретні демонстраційні значення ще не виписано.

## 5. Конкретний мінімальний план прототипування — пропозиція до REV-02

На F1 Agent створює редаговані frames та анотації переходів; реальні connections перевіряються пізніше у P1, вручну. Не просити Agent реалізувати backend або справжні умовні права.

**Обов’язково зв’язати для базової демонстрації:**
- T-03/T-04: All ↔ Important.
- T-02: ISS-003 відкривається з обох tabs у відповідні деталі.
- T-05/T-06: Create/Cancel із All та Important з поверненням у правильну вкладку.
- T-09: підготовлений valid Create → S-03 new, не переплутати його з ISS-003.
- T-10: Return з details зберігає origin tab, включно з new issue з Important.

S-02-C і його Create/Cancel також перевірити з окремого empty fixture. Для збереження origin у Figma дозволені технічні копії details/overlay з різними connections; їх не називати новими продуктовими екранами. Базовий початковий inventory — 7 frames; кількість технічних копій буде зафіксована після wiring, а не вигадана зараз.

**Дозволено представити як V-only component examples у REF-01:** Create validation; assignee/priority Apply; усі чотири status transitions та заборони; comment success/empty/failure. Їхні P-тести залишаються NOT RUN / NOT WIRED, якщо connections не створено. Розширити wiring можна за наявності часу; наявність annotation не стає PASS P.

**I outstanding:** authentication, server permissions, persistence, automatic IDs/time, реальна фільтрація, response time, HTTPS, backup. Ці вимоги не відкидаються, але базовий прототип їх не доводить.

Це рекомендований scope перевірки навчального прототипу, не твердження про вже виконані переходи.

## 6. Питання, які можна відкласти

- Технічний механізм authentication: Q-01 лишається частково UNRESOLVED; D-02 визначає достатню межу для wireframes.
- Формат БД для Not Set, генерація ID, time zone storage, API та backup architecture: не потрібні для складання brief.
- Точні ліміти довжини та whitespace-only input: не визначені у джерелі; не перетворювати їх на приховані вимоги.
- Future AI та Deferred attachments: не включати в поточний дизайн.

## 7. Вердикт

**NOT READY для запуску Figma / випуску фінального APPROVED brief.**

Причина — не втрата AC, а незавершене погодження UX-деталей D-09–D-14 і відсутність зафіксованого людського контролю B. Рекомендація AI: прийняти D-09–D-14 та мінімальний P-scope §5, заповнити fixtures на G5 і після реальної перевірки граничних сценаріїв перейти до brief.

Коли це виконано, вердикт можна оновити до PLAN READY із посиланням на автора рішення та точні версії. Не підставляти READY/APPROVED автоматично. Усі 38 acceptance tests майбутнього макета залишаються NOT RUN.

## 8. Запис для контролю B — ще не заповнений результат

| Поле | Поточний стан |
|---|---|
| Human reviewer | Не зафіксовано |
| Date | Не зафіксовано |
| Versions | Input Pack 1.0; Decision Log 1.0; Screen Map 0.1; Screen Contracts 0.1 |
| Accepted decisions | D-01–D-08 вже погоджені раніше; D-09–D-14 pending |
| Boundary scenarios | Перевірка людиною ще не зафіксована; кейси наведені в §3 |
| Open blockers | REV-01, REV-03; REV-02/04 закриваються конкретизацією scope/fixtures до відповідних етапів |

Review не змінює специфікацію або історичні чернетки. Виправлені/погоджені artifacts випускаються наступними версіями після фактичного рішення.
