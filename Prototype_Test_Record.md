# Prototype Test Record — Mini Issue Tracker

Версія: 1.1  
Дата запису: 08.11.2026  
Виконавець проходження: автор роботи, користувач цього чату.  
Спосіб: ручна перевірка у Figma Present, результат повідомлено користувачем.  
Підтвердження: на запит перевірити сім наведених маршрутів користувач відповів «да».

**Межа доказу:** ChatGPT не виконував ці кліки самостійно. PASS — reported означає підтвердження автора, а не незалежно спостережене проходження. PNG показують стани; загальний screenshot Prototype показує зв’язки, але не всі їхні settings. Момент фактичного виконання кожного кліку окремо не зафіксований; наведена дата — дата підтвердження.

## Перевірені сценарії

| P-ID | Маршрут / дія | Очікуваний результат | Результат | Джерело / докази |
|---|---|---|---|---|
| P-01 | All → ISS-003 → Return | Повернення до All; деталі відповідають ISS-003 | PASS — reported | AC-02.3/02.4; D-07/09; S-02-A.png, S-03.png; підтвердження автора |
| P-02 | Important → ISS-003 → Return | Повернення до Important | PASS — reported | D-07; S-02-B.png, S-03.png; підтвердження автора |
| P-03 | Important → Create → Cancel | Modal закрито, повернення до Important, без створення | PASS — reported | D-01/10; підтвердження автора; connection overview |
| P-04 | Заповнена форма → Create | Відкрито деталі нової ISS-009 із відповідними Title/Description, Open, Not Set | PASS — reported | AC-01.1/01.4/01.5; D-10; M-01-VALID.png, S-03-CREATED.png |
| P-05 | Нова ISS-009 → Return | All зі збереженими попередніми записами та доданою ISS-009 | PASS — reported | AC-02.1; D-10; S-02-A-AFTER-CREATE.png |
| P-06 | Empty All → Create valid → нова заявка → Return | All містить лише ISS-009, без старих baseline records | PASS — reported | AC-02.5; D-10; M-01-VALID-FROM-EMPTY.png, S-03-CREATED-FROM-EMPTY.png, S-02-C-AFTER-CREATE.png |
| P-07 | Окремо порожній Title та окремо порожній Description → Create | Відповідна помилка, заявка не створена | PASS — reported для обох варіантів | AC-01.2/01.3; M-01-BEFORE-ERR-TITLE..png, M-01-ERR-TITLE.png, M-01-BEFORE-ERR-DESC.png, M-01-ERR-DESC.png |

Усього: сім сценаріїв, останній містить два варіанти validation. Це не означає виконання всіх TEST-01–38 із Screen Contracts.

## Додатково підтверджено раніше

07.11.2026 автор відповів «да» після перевірки All → Important → All. Це окреме повідомлення автора про роботу вкладок (T-03/T-04), не незалежний тест алгоритму фільтрації.

## Що не підтверджено цим протоколом

- Create із Important → success → Return саме до Important; його не підміняти P-03 (Cancel) або P-05 (Return до All).
- Create/Cancel із порожнього All; P-06 підтверджує success-route, а не Cancel-route.
- Обидва поля порожні одночасно; P-07 охоплює окремі помилки.
- Реальні кліки assignment/reassignment/priority Apply; status transitions; comment success/empty/failure. Їхній wiring і проходження не заявляються без додаткових даних.
- Перерахунок прав після reassignment та відмова unauthorized action в реалізації.
- Реальна автентифікація, persistence, automatic IDs/time, filtering, response time, HTTPS, backup/restore.

## Версія та джерела

Оцінено комплект PNG, наданий 08.11.2026: baseline All має ISS-001–ISS-008, нова заявка — ISS-009; ISS-003 — Profile update fails. Screenshot загальних connections: image(20261108-125047).png. Ці fixtures відрізняються від історичного brief 1.0; поточний знімок даних описаний у 06_Review_Report.md.

Автор надав [Figma Design — Mini Issue Tracker — Final](https://www.figma.com/design/d9CkiP4T6UUC2oXSpk8au7/Mini-Issue-Tracker-%E2%80%94-Final?node-id=0-1) 08.11.2026. Це назва файла; номер named version не підтверджений. Доступ викладача незалежно не перевірений.

## Стан після correction

Після виправлення Unassigned та initial Apply нові screenshots переглянуто візуально. Автор ще не повідомив про повторне проходження P-01–P-07 саме після цих правок. Попередні PASS — reported не переносяться автоматично на нову revision. Надання посилання Figma не є новим тестом кліків.
