# Mini Issue Tracker — UX/UI

Навчальна робота з проєктування low-fidelity desktop UX/UI та базового клікабельного прототипу Mini Issue Tracker за специфікацією SD_Spec.

## Макет

[Figma Design — Mini Issue Tracker — Final](https://www.figma.com/design/d9CkiP4T6UUC2oXSpk8au7/Mini-Issue-Tracker-%E2%80%94-Final?node-id=0-1)

Назву «Mini Issue Tracker — Final» та URL надав автор 08.11.2026. Це назва файла, а не підтверджений номер іменованої версії в Version history. Доступ викладача та збереження named version незалежно не перевірені.

## Scope

- Release MVP: US-01–US-08, 33 змістові критерії приймання.
- Deferred: US-09 — attachments.
- Future: SR-10 — categorization; SR-11 — priority recommendations.
- Actors: два Team Member та один Team Lead. Assignee — відношення до конкретної заявки, не окрема глобальна роль.
- Результат: editable design і прототип із підготовленими навчальними станами; реалізація вебзастосунку не є частиною цього комплекту.

## Документи

| Файл | Призначення |
|---|---|
| 01_Input_Pack_v1.0.md | Вимоги, scope, source check для всіх 33 AC |
| Decision_Log.md | Погоджені D-01–D-14, історія рішень |
| 02_Screen_Map_v1.0.md | Екрани, стани, переходи та user flows |
| 03_Screen_Contracts_v1.0.md | Controls, права, status matrix, Traceability та план перевірки |
| 04_Plan_Review_v1.0.md | Перевірка плану до генерації |
| 05_Figma_Brief_v1.0.md | Історичний контракт першої генерації |
| 06_Review_Report.md | Актуальна повторна перевірка; підсумок у §8–9 |
| Prototype_Test_Record.md | Сім маршрутів, підтверджених автором у Present; межі доказів |
| Review_Defect_Change_Log.md | Хто, що і як перевіряв; знахідки та повторна перевірка |
| AI_interaction_log.md | Взаємодії з AI та відомі обмеження; не замінює повний діалог |

Файли v0.1 зберігаються як історичні drafts. Для поточного дизайну слід враховувати Review Report: навчальні fixtures змінилися з початкових 6 + ISS-007 на 8 + нову ISS-009; source AC не змінювалися. Mapping змінених Control IDs наведено у Review Report §8.5.

## Екрани та підготовлені результати

- S-01 — нейтральна authentication boundary, без вигаданого login.
- S-02-A/B/C — All, Important та Empty одного списку заявок.
- M-01 і його variants — Create default, valid, validation.
- S-03 — canonical details ISS-003; S-03-CREATED та FROM-EMPTY — нова ISS-009.
- AFTER-CREATE frames — підготовлені результати списку для populated та independent empty datasets.
- REF-01 — службові permissions, status, priority, comment та validation examples, поза продуктовим UI.

Технічні copies/variants не є додатковими продуктовими функціями.

## Правила для демонстрації

- Лише Lead призначає/перепризначає одного виконавця та керує priority.
- Status змінює тільки поточний assignee, включно з Lead.
- Дозволено лише Open → In Progress; In Progress → Resolved; Resolved → In Progress; Resolved → Closed.
- У Closed немає наступного status; це не вимикає автоматично comments або Lead assignment/priority.
- Important: `priority in {High, Critical} AND status != Closed`. Resolved входить за відповідного priority, Closed виключено.
- Not Set — відсутність priority, не selectable рівень/reset. Відсутній assignee показується як Unassigned.

## Результати та межі перевірки

Потрібні UI-поля, правила й стани представлені за результатом візуального огляду основних exports та читабельних REF-фрагментів. Unassigned і initial disabled Apply виправлені та повторно перевірені на PNG.

Сім prototype scenarios автор повідомив як успішні до останніх точкових правок. ChatGPT не виконував кліки незалежно. Повторний regression після correction ще не підтверджений; annotation examples не видаються за пройдені P-тести. Усі 38 запланованих tests не оголошуються виконаними.

Поза перевіркою wireframes: фактичні authentication, server permissions, persistence, automatic IDs/time, real filtering, response time < 1 s, HTTPS, backup/restore. Editable layers, actual component count і Auto Layout не доводяться PNG; початкові 98 instances були повідомленням Agent про першу версію.

## Що завершити перед здаванням

1. Перевірити доступ викладача до Figma та зафіксувати поточну named version або дату фінального знімка.
2. Підтвердити повторне проходження семи маршрутів після останніх правок, додати результат до Prototype_Test_Record.md.
3. Закрити DOC-02: прибрати застарілі пояснення REF про відсутність prototype wiring, «empty Assignee» та source range D-01–D-09; потрібний текст наведено в Review Report. Виконання цих текстових правок ще не підтверджено.
4. Зберегти повні фактичні AI prompts/responses або transcript як доказ відтворюваності; стислий AI log не є повним transcript. Якщо робота командна — додати реальних учасників і розподіл, не вигадувати перевіряльника.
5. Для заочного захисту додати посилання на відеозапис, якщо він здається за форматом заняття.

## Evidence

Попередні update-архіви містять `evidence/2026-11-08/` та `evidence/recheck-2026-11-08/`. Ці папки потрібно додати в репозиторій разом із документами. Поточний README не стверджує, що віддалений GitHub repository вже оновлено.
