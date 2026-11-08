# AI Interaction Log — Mini Issue Tracker

Версія: 1.0  
Дата створення: 07.11.2026

Журнал складено ретроспективно на G4 за діями поточного чату. Це стислий index, а не повний verbatim transcript. Повні запити/відповіді ще потрібно зберегти з чату для відтворюваності; цього файла самого недостатньо як копії діалогу.

Operator: автор роботи (користувач чату). Tool: ChatGPT Work; тариф користувача Plus. Точну назву моделі/показаний режим не зафіксовано — не вигадується. Тексти нижче — резюме взаємодій, крім явно позначених коротких цитат користувача.

| Запис | Дата / етап | Контекст | Запит / результат | Рішення / перевірка | Ліміти / fallback |
|---|---|---|---|---|---|
| AI-01 | 07.11.2026 / підготовка | Методичні рекомендації PDF, потім SD_Spec.docx.pdf | Прочитано методичку й специфікацію; пояснено MVP та порядок роботи | Спочатку запропоновано загальний Word-звіт; після перевірки §22 уточнено, що потрібен комплект artifacts | Повідомлень про ліміти не зафіксовано |
| AI-02 | 07.11.2026 / G1 | Повна прочитана специфікація; методичка §5 | На прохання продовжити підготовлено Input Pack, далі оформлено 01_Input_Pack_v0.1.md | Включено 8 US, 33 AC; Q-01–08; SOURCE/DERIVED відокремлено | Не зафіксовано |
| AI-03 | 07.11.2026 / Decision Log | Input Pack; методичка §6 | Підготовлено D-01–D-08 PROPOSED; користувачу пояснено зміст погодження | Після цитати «да, делаем так» випущено D-Log 1.0 APPROVED та Input Pack 1.0. Це не людський контроль усіх AC | Не зафіксовано |
| AI-04 | 07.11.2026 / формат результатів | Публічний приклад https://github.com/NureKurinnaDaria/Mini_Issue_Tracker_UX_UI | Переглянуто структуру, readme і окремі журнали прикладу; обрано Markdown artifacts | Приклад — орієнтир організації, не продуктові вимоги чи докази нашої роботи | Не зафіксовано |
| AI-05 | 07.11.2026 / G2 | Input Pack 1.0; D-Log 1.0; методичка §7–8 | На продовження роботи створено 02_Screen_Map_v0.1.md | T-01–24, UF-01–13; 7 planned frames; UX-деталі залишено PROPOSED | Не зафіксовано |
| AI-06 | 07.11.2026 / G3 | Screen Map; Input Pack; D-Log; методичка §9–10 | На запит «давай некст» створено 03_Screen_Contracts_v0.1.md | C-01–17, UIR-01–33, TEST-01–38, permission/status matrices; перевірено структуру скриптом; майбутні tests NOT RUN | Не зафіксовано |
| AI-07 | 07.11.2026 / G4 | Повторно прочитана специфікація; artifacts G1–G3; методичка §11–12 | На запит «хорошо, работаем дальше» виконано змістовний review; створено 04_Plan_Review_v0.1.md і ці журнали | 33 COVERED у плані; NOT READY для Figma до людського контролю B та погодження UX; REV-01–04 OPEN. AI у тому самому чаті не є незалежним reviewer | Не зафіксовано |

## Що додати як доказ

- Копію повного діалогу за етапами або повні тексти prompt/response; не замінювати їх вигаданими «точними промптами з методички», бо користувач переважно давав короткі команди продовження.
- Реальні mode/model labels, лише якщо їх видно в інтерфейсі та вони зафіксовані.
- Після F1/P1/G6 — конкретні Figma prompts, відповіді, screenshot evidence, version і результати ручних кліків.

Генерація Figma ще не виконувалась; Figma credits, edits, PASS transitions або screenshots у цьому журналі не стверджуються.

## AI-08 — підтвердження G4 та підготовка G5

- Date / operator / step: 07.11.2026 / автор роботи / G4–G5.
- Tool / plan / mode: ChatGPT Work / Plus; точну назву моделі та показаний режим не зафіксовано.
- Context: актуальні D-Log, Screen Map, Screen Contracts, Plan Review та журнали; специфікацію прочитано на G4.
- Prompt / response: користувач відповів «да» після переліку UX-деталей і трьох граничних правил. Підготовлено фінальні Screen Map/Contracts/Plan Review та self-contained English Figma brief; повний текст цього діалогу ще треба зберегти окремо.
- Decision / evidence: D-09–D-14 APPROVED зафіксовано в D-Log 1.1. Людське підтвердження обмежено представленими деталями/кейсами; незалежний reviewer не вигаданий. Усі майбутні acceptance tests NOT RUN.
- Checks: структура Traceability, 38 тестів, 17 controls, 24 transitions; правила прав/status/Important та sample data у brief. Конкретні результати механічної перевірки — CHK-06.
- Limit / fallback: повідомлень про ліміт не зафіксовано. Figma ще не використовувалась; кредити й виконані edits не заявляються.

## AI-09 — F1 report та static evidence review

- Date / operator / step: 07–08.11.2026 / автор роботи / F1 та огляд до P1; журнал доповнено 08.11.2026.
- Tool: Figma Agent, потім ChatGPT. План Figma та назва моделі Agent не зафіксовані. Не переносити тариф Plus із ChatGPT на Figma.
- Context: brief 1.0 для першої генерації, далі PNG основних frames та читабельні фрагменти першого REF.
- Prompt / response: launcher наведено в цьому чаті; автор вставив Agent report із 7 frames, N-01–07, 5 definitions/98 instances. Повний native Figma chat ще не надано як окремий файл. Заявлені components/Auto Layout — reported Agent.
- Decision / evidence: перша static review не виявила mandatory defects; optional Title height observation. Другий correction prompt не був потрібний за результатом того огляду; фактична кількість пізніших Agent calls не відома.
- Limits: повідомлень/балансу Figma credits не надано, не виводити їх із кількості frames.

## AI-10 — нові screenshots, P1 та G6

- Date: 08.11.2026; operator: автор роботи; tool: ChatGPT Work. Точний показаний режим/модель не зафіксовано.
- Context: змінені exports S-02/S-03/M-01/REF-01, нова ISS-009, screenshot prototype connections; Screen Contracts 1.0 та історичний brief.
- Prompt / response: після переліку семи маршрутів користувач відповів «да». Створено Prototype_Test_Record.md та 06_Review_Report.md; оновлено журнали.
- Decision / evidence: сім PASS — reported, не незалежно спостережені кліки. Current REF недостатньо читається. DEF-01/Q-UI-01/Q-EV-01 лишаються відкритими; current fixtures зафіксовані без переписування історії першого brief.
- Unknowns: повні prompts/метод пізніших змін, точний version/file URL Figma, факт збереження BEFORE_REVIEW.fig не підтверджені.
- Checks: структура 33 AC rows у Review Report; сім P-records; source/claim boundaries V/P/I. Implementation tests outstanding.
- Limit / fallback: ліміти не повідомлялися; потрібні читабельні поточні reference exports, а не припущення з першої версії.


## AI-11 — точковий correction prompt та повторна візуальна перевірка

- Date / operator: 08.11.2026 / автор роботи.
- Context: findings Unassigned/initial Apply; поточні Figma frames. У чаті підготовлено один targeted English prompt для Agent зі збереженням connections; факт виконання саме цього prompt і повний Agent response не надані.
- Response / evidence: автор надав 20 readable REF fragments і шість оновлених основних exports. Reviewer ChatGPT підтвердив Unassigned та disabled initial Apply; current permissions/status/comment states читаються.
- Outputs: Review Report 1.0, logs 0.4, archive of review updates. DEF-01, Q-UI-01, Q-EV-01 CLOSED visual. DOC-02 — stale annotations — лишається OPEN до повідомлення про виправлення.
- Limits: screenshots не доводять збереження prototype interactions, native components чи backend. Regression після correction не повідомлена; сім попередніх scenarios залишаються PASS-reported до останньої правки.
- Agent credits/plan/model: не надано; не вигадуються. Повні native Figma prompts/responses слід зберегти як історію, якщо вони доступні автору.

## AI-12 — Figma URL та README

08.11.2026 користувач надав Design URL і назву «Mini Issue Tracker — Final». ChatGPT спробував відкрити URL, отримав недоступність через інструмент; не робив висновків про private/public доступ. Підготовлено README.md, оновлено Review Report/Prototype Record та журнали. Новий Figma generation, screenshot capture або повторний walkthrough не виконувалися.

## AI-13 — остаточне підтвердження автора

08.11.2026 користувач відповів «да» після питання про виправлення REF-01 та повторне проходження семи маршрутів після останніх правок. Результат внесено як reported evidence, не independent review. DOC-02 закрито reported; повторні P-01–P-07 — PASS-reported after correction. Підготовлено оновлені документи та узгоджений архів для репозиторію. Автоматичних Figma edits, нової generation або remote git push у цьому кроці не було.
