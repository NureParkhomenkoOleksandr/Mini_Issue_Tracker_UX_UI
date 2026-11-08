# Review / Defect / Change Log — Mini Issue Tracker

Версія: 0.5  
Дата створення: 07.11.2026

Журнал створено на етапі G4. Раніше описані перевірки фіксуються ретроспективно лише в межах видимих дій цього чату. Нові перевірки додаються окремими записами. Усі review тут виконані ChatGPT у тому самому чаті, якщо явно не вказано іншого перевіряльника. Незалежна людська перевірка не вигадується.

| CHK-ID | Дата / reviewer | Документ / версія | Як перевіряли | Результат | Виправлення / доказ |
|---|---|---|---|---|---|
| CHK-01 | 07.11.2026 / ChatGPT | 01_Input_Pack_v0.1.md | Зіставлення US/AC із прочитаною специфікацією; програмна перевірка наявності 29 нумерованих та 4 ненумерованих AC | 33 AC присутні; це не контроль A студентом | Файл 01_Input_Pack_v0.1.md; чернетка збережена |
| CHK-02 | 07.11.2026 / ChatGPT; рішення — автор роботи | Decision_Log.md 1.0; Input Pack 1.0 | Після повідомлення користувача «да, делаем так» оновлено D-01–D-08; повторно перевірено 33 критерії та 8 APPROVED rows | Погодження UX зафіксовано; технічний login відкритий | Decision_Log.md 1.0; 01_Input_Pack_v1.0.md. Перша спроба скрипта мала помилковий count assertion, виправлена перевірка підтвердила всі конкретні AC; продуктові вимоги через це не змінювалися |
| CHK-03 | 07.11.2026 / ChatGPT | 02_Screen_Map_v0.1.md | Зіставлення маршрутів із US, D-01–D-08 та шаблоном G2 | Підготовлено 2 продуктові екрани, modal, boundary, REF; 24 T-ID, 13 UF | 02_Screen_Map_v0.1.md. Це self-review плану, не тест Figma |
| CHK-04 | 07.11.2026 / ChatGPT | 03_Screen_Contracts_v0.1.md | Формалізація controls і станів; скрипт перевірив UIR-01–33, TEST-01–38, C-01–17 та посилання T-01–24 | 33 Traceability rows, 38 tests, 17 controls; D-09–D-14 PROPOSED | 03_Screen_Contracts_v0.1.md; усі майбутні acceptance tests NOT RUN |
| CHK-05 | 07.11.2026 / ChatGPT | G4: Input Pack 1.0, D-Log 1.0, Screen Map 0.1, Contracts 0.1 | Повторне читання специфікації; змістовне зіставлення кожного AC; права, status matrix, Important, negative states; межі V/P/I | 33 COVERED на рівні плану; вимогових дефектів не підтверджено. NOT READY через pending UX та людський контроль B | 04_Plan_Review_v0.1.md §2–8; REV-01–REV-04 відкриті, пропозиції закриття конкретизовані |

## Відкриті findings

| ID | Статус | Потрібна дія |
|---|---|---|
| REV-01 | RESOLVED | Автор відповів «да»; D-Log 1.1, Contracts 1.0 |
| REV-02 | RESOLVED як план | P-scope визначено в Contracts/Brief, виконання NOT RUN |
| REV-03 | PARTIALLY RESOLVED | Підтвердження автором трьох кейсів зафіксовано; незалежний review не виконано |
| REV-04 | RESOLVED | Конкретні fixture values наведено в Brief 1.0 |

Не всі findings є дефектами вимог. DEF-ID створюється для підтвердженої помилки; тут REV-ID позначають питання готовності. Результати майбутніх перевірок макета та прототипу додаються тільки після фактичного огляду/проходження.

## CHK-06 — завершення G4 / G5

- Дата: 07.11.2026. Reviewer: ChatGPT; рішення щодо UX — автор роботи, відповідь «да» після переліку деталей і трьох правил.
- Artifacts: Decision Log 1.1; Screen Map 1.0; Screen Contracts 1.0; Plan Review 1.0; Figma Brief 1.0.
- Метод: синхронізовано D-ID та approval status; повторно перевірено 33 Traceability rows, 38 тестів, controls і transition references; перевірено збереження правил прав/status/Important у brief; sample metadata та comment success/failure виписано явно.
- Результат: текстовий brief підготовлено; REV-01/02/04 закриті на рівні планування. REV-03 частково закрито обмеженим людським підтвердженням, незалежний контроль не стверджується.
- Змінено: статуси D-09–14, фінальні версии документів, P-scope, sample metadata; джерело не змінено.
- Доказ: перелічені фінальні файли та повідомлення автора. Жоден майбутній V/P/I test не отримав PASS. Figma generation не запускалась.

## CHK-07 — F1, огляд першої версії та зміна дизайну

- Дата доказів: 07–08.11.2026; запис складено 08.11.2026. Reviewer: ChatGPT, зображення надано автором роботи.
- F1 report від Agent: заявлено 7 canonical frames, N-01–N-07, 5 definitions, 98 actual instances, Auto Layout. Це REPORTED Agent, не independently verified layer audit.
- Перша версія 07.11: основні екрани та окремі читабельні REF screenshots оглянуто в чаті; mandatory defects не підтверджено, висота Title була optional UX observation.
- 08.11 автор надав змінені екрани та fixtures, current connection overview. Спосіб/повні промпти всіх змін не надано; не приписувати їх ручному редагуванню або конкретному Agent request без доказу.
- Поточний REF-01 відрізняється від першого та недостатньо читається; попередній review не переноситься автоматично.
- Докази та current findings: 06_Review_Report.md §1–5. Зображення не доводять editable layers, Auto Layout або backend.

## CHK-08 — P1 reported walkthrough та поточний G6

- Дата підтвердження: 08.11.2026. Виконавець проходження: автор роботи; ChatGPT сам кліки не виконував.
- На перелік семи сценаріїв автор відповів «да». У Prototype_Test_Record.md P-01–P-07 записано PASS — reported, а не independent PASS.
- Review: усі 33 AC отримали окремий result із поділом V/P/I; частина NOT VERIFIABLE через unreadable current REF та implementation boundary. Не заявлено «всі AC виконано».
- Current data: 8 baseline records + new ISS-009; синхронізацію зафіксовано в 06_Review_Report.md §2, історичний brief не підмінено.
- Findings: DEF-01 (порожній Assignee замість Unassigned) OPEN; Q-UI-01 (initial/staged Apply) OPEN; Q-EV-01 (читабельність нового REF) OPEN. Немає доказів, що вони вже виправлені.
- Висновок: основні маршрути REPORTED; design review PARTIAL; backend/NFR outstanding. До остаточного здавання потрібні resolution findings, readable REF та Figma URL/version.

## Current design findings — 08.11.2026

| ID | Статус | Рішення / повторна перевірка |
|---|---|---|
| DEF-01 | OPEN | Потрібно додати Unassigned або явно відхилити зауваження з причиною; виправлення не надано |
| Q-UI-01 | OPEN | Уточнити initial/staged Apply; за initial — disabled до іншого вибору |
| Q-EV-01 | OPEN | Надати читабельний current REF-01 sections; не називати unreadability відсутністю станів |
| DOC-01 | DOCUMENTED | Фактичні fixtures описано в Review Report; це не доказ відповідності всіх hidden states |

Ранні REV-01–04 стосуються readiness G4/G5; DEF-01 та Q-ID цього розділу — поточного design review. Ідентифікатори не підмінюють одне одного.


## CHK-09 — повторний огляд REF та шести виправлених frames

- Дата: 08.11.2026; reviewer: ChatGPT; метод: аналіз 20 читабельних REF screenshots та шести нових основних PNG із суфіксом (1).
- Artifacts: 06_Review_Report.md 1.0; поточні Figma screenshots, exact file/version URL ще не надано.
- DEF-01 CLOSED visual: Unassigned у new details, populated/empty after-create та baseline lists.
- Q-UI-01 CLOSED visual: Apply у initial S-03 disabled; before/pending/applied reference відокремлює вибір від збереженої зміни.
- Q-EV-01 CLOSED: прочитано current permissions, single-assignee options, priority options, усі чотири status transitions, comment outcomes, Important before/after closing та both-empty validation.
- Додано mapping усіх 17 Control IDs між Contracts та новим REF, щоб зберегти Traceability.
- DOC-02 OPEN: застарілий wording про wiring, empty Assignee та D-range. Виправлення рекомендовано в чаті; після цього підтвердження виконання ще не отримано.
- Результат: потрібні UI state representations присутні; відомі display findings закриті. Не заявлено PASS реальної authorization/persistence або незалежний P walkthrough.
- Регресія прототипу після останніх правок: NOT REPORTED. Попередні сім PASS-reported лишаються історичним записом; не переписуються як новий тест.
- Доказ: 06_Review_Report.md §8, current evidence files. Останній запис CHK-09 є актуальним resolution status, попередні OPEN entries збережено як історію.

## CHK-10 — посилання та README

08.11.2026 автор надав URL Design file та назву «Mini Issue Tracker — Final». ChatGPT додав їх до README, Review Report 1.1 та Prototype Record 1.1. Автоматичне відкриття URL не вдалося; live content, sharing permission і named version не перевірені. Це документаційне оновлення, не повторний UI/P audit. DOC-02 та regression confirmation лишаються pending.
