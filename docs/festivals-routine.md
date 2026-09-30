Festivals page update routine
This file tells the scheduled Claude Code routine how to refresh the
"What's on in Seoul" page. Save it in the repo as `docs/festivals-routine.md`.
Goal
Update `public/festivals.html` for Seoul Genius, a licensed tour company whose
best-selling tours are Gyeongbokgung and Changgyeonggung palace tours and
traditional market experiences near Gyeongbokgung. Audience: foreign visitors,
English only.
What to edit
Edit ONLY the `const GENERATED = ...` line and the `const EVENTS = [ ... ];`
array inside `public/festivals.html`. Do not touch HTML, CSS or the rendering
script below the EVENTS array.
Set GENERATED to today's date in Korea time (YYYY-MM-DD).
Keep each event object in the existing shape:
id, name, kr, start, end, cat, tags, when, where, transit, fee, summary,
booking (optional), tip (optional), link, image (optional).
cat: "palace" | "arts" | "daytrip"
tags: any of "palace", "night", "free", "daytrip"
image: { src, alt, credit, license }
Include events that are running now or start within the next 42 days.
Remove events that have ended.
Aim for 8 to 15 events. Quality over quantity.
Sources (in this order)
PALACES (highest priority)
kh.or.kr/fest (Royal Culture Festival, English/foreigner sessions)
royal.khs.go.kr (palace night openings, guard ceremonies)
kh.or.kr (Korea Heritage Agency programs: moonlight tours, media art, Korea House)
TourAPI (Korea Tourism Organization), if `TOUR_API_KEY` is set:
searchFestival2 on KorService2 with areaCode=1 (Seoul), eventStartDate = today
Also check EngService2 for official English names
SEOUL FESTIVALS
Seoul Open Data cultural events API, if `SEOUL_API_KEY` is set
seoul.go.kr/festa and culture.seoul.go.kr
festival.seoul.go.kr (FUN SEOUL) blocks automated access. Use web search
results only. Do not fetch it directly.
FOREIGN-VISITOR SOURCES: english.visitkorea.or.kr, english.visitseoul.net
Selection
Rank higher: palace and royal heritage events, traditional culture,
food and markets, big free outdoor festivals, anything in Jongno or near
Gyeongbokgung, programs with English sessions. Skip events aimed only at
residents (sports leagues, business expos, children's classes in Korean).
Accuracy rules
Verify every date, time, venue and price on an official source
(organizer page, government page, or TourAPI). News articles may be used to
find events but not as the only source for dates.
If a detail cannot be confirmed, leave it out or write "Check the official
page". If the dates cannot be confirmed, leave the event out entirely.
Never reuse dates from previous years.
Writing rules
Write every summary, booking note and tip in your own words, 1 to 3
sentences each. Never copy or closely paraphrase any website's sentences.
Some sources carry KOGL Type 4 (no commercial use, no modification):
take only facts from them.
Plain, friendly English. No hype words.
Add a "tip" (linking the event to a Seoul Genius palace tour) to at most
3 events, only where it fits naturally.
"kr" is the official Korean name of the event.
Images
Use only these images:
TourAPI `firstimage` where `cpyrhtDivCd` is Type1 or Type3.
Change http to https. credit: "Korea Tourism Organization (TourAPI)",
license: "KOGL Type 1" or "KOGL Type 3".
Existing files in `public/img/` that match the event's venue
(for example `public/img/changgyeonggung.jpg`), keeping their current
credit line from `public/img/credits.json` if present.
Never hotlink or download posters or photos from any other website.
If no allowed image exists, omit the image field (a colored tile is shown).
Output
Update `public/festivals.html` as described above.
Save a copy to `public/festivals-archive/festivals_YYYY-MM-DD.html`.
Keep only the 15 most recent archive files; delete older ones.
Check the file: the script must still parse (run
`node --check` on the extracted script if Node is available) and every
event must have id, name, start, end, link.
Commit with the message `Update festivals page YYYY-MM-DD` and push.
End with a short summary: events added, events removed, anything you could
not verify.
