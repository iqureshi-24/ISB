# How to build a new ISB week

ISB (International School of Bo) is a one-page website (`index.html`, served by GitHub Pages at https://iqureshi-24.github.io/isb/) that runs the home-school week for Eesa (14, Year 10, out of school in the UK; his school is in the UAE). Ishaaq (growqureshi@gmail.com) runs it. Eesa's progress is saved in his iPad's browser, keyed by the week id, so **never change the saving code**; only replace the week.

Each week the school sends a "Weekly Scheme" PDF. It gets saved into the Google Drive folder "ISB weekly schemes" (id `1nZBfhNF6RhLxzaXIxiR1mUzXFCOa19xL`). Your job is to turn it into next week's lessons and Friday tests.

## What to change in index.html

Only the block between `/* ===== WEEK-START` and `/* ===== WEEK-END ===== */`. It holds the link constants (`W2` style object, `YT`, `CK`), `WEEK` and `TESTS`. Keep the same shapes as the current week. Rename the link object if you like (e.g. `W3`).

- `WEEK.id` = the Monday date (`YYYY-MM-DD`). `label` = "Week N" (count up from Week 2 = 2–6 Nov 2026). `range` like "9–13 Nov 2026". `dates` = Mon..Fri.
- `L(subject, title, specArray, description, options)` makes a lesson. Subjects: `maths physics chemistry biology cs english business`.
- Options: `res:{video, video2, videoNote, notesNote, readLink, practice, practice2, qNote, topic, aiAsk, aiNote, writeTitle, write}`; `steps:[{t, note, links}]` to list steps by hand; `noWarm:1` to skip the warm-up; `prove:1` marks a Prove-it lesson Mama checks.
- A link is always `['Label', 'https://…']`. Use `YT('Title (Channel)', 'videoId', startSeconds)` for YouTube.

## The timetable (fixed)

- 8:00–3:00. Mon–Thu: 5 lessons (8:00, 9:15, 10:30, 12:05, 1:10). Dhuhr break 11:35–12:05, Asr break 2:05–2:35. Friday: 2 test blocks (8:00 and 9:25, three 25-minute tests each), then 3 lessons (10:50, 12:05, 1:10).
- So each day array has exactly 5 items. Friday = 2 test items + 3 lessons.
- **Lessons per week (strict):** English 4, Maths 4, Biology 3, Chemistry 3, Physics 3, Business 3, Computer Science 3 = 23. Never two of the same subject in one day. Friday's 3 lessons come after the tests, so they are "fix your test" lessons or (for CS) whatever the scheme says.

## Lesson rules (from Eesa and Ishaaq)

- Steps are plain tick boxes. No minutes anywhere.
- **Science videos:** Free Science Lessons first. If it has no video for the exact topic, use Cognito (YouTube or cognito.org). Only then IGCSE Science Revision.
- If one video is split across two lessons, say exactly which timestamps to watch each day.
- **Chemistry:** Save My Exams links must match the exact topic. If there is no topic-question page for it, link the exact revision-notes subpage and tell him which questions to do on the chapter page.
- **Business and English:** no videos. Give the exact spec point / topic in `res.topic` (Business: quote the official 4BS1 spec wording) so the "Learn it in ChatGPT" button teaches it. Add a practice task or writing task.
- **Computer Science:** follow the scheme. If it names Classkick slides, use `steps:[CK(n),…]` with `noWarm:1`, spread evenly. Class page: Classkick (constant `CLASSKICK`).
- **Maths:** Cognito / Oak / Maths Genie videos and questions with answers.
- No textbooks. School SharePoint/Edunation/Teams files don't open in the UK, so never link them. YouTube links from the scheme are fine.
- Only use URLs you actually saw in a search result or fetched page. Never invent links.

## Friday tests

- Real past-paper questions only (Physics & Maths Tutor topic PDFs at `https://pmt.physicsandmathstutor.com/download/...`, or real papers). 25 minutes and roughly 18–25 marks each. Quote-check each question part in the PDF.
- Don't reuse question parts listed in `TESTS-USED.md`. Add the new ones there.
- English: a 45-minute writing task every other week; the other weeks a 25-minute reading question. Business: a longer evaluate/justify question every other week (opposite weeks to the English writing). Week 2 had the English reading question and the Business justify question, so Week 3 = English 45-minute writing + Business short answers.
- If the scheme says the school is giving a test in a subject, leave that subject out of `TESTS` and the Friday test items.
- The test blocks list subjects in `tests:[…]`; every subject listed must exist in `TESTS`. Fix the Friday test titles to match.

## Check before publishing

1. `node` syntax check of the script.
2. Open the page in Playwright Chromium (already installed; don't run `playwright install`) with the clock faked to a weekday 10:00 and to Friday 8:10, and check: no page errors, This week grid shows 5 lessons a day, lesson counts per subject are right, each lesson opens, the Tests page shows the right cards.
3. Commit with a clear message and push to `main`. GitHub Pages updates in about a minute.

## Tell Ishaaq

Email growqureshi@gmail.com (subject "ISB: Week N is live") with a short plain-English summary: what each subject covers, the Friday tests, and anything you couldn't find or check.
