# spine

An iOS app that turns the books you've read into a bookshelf.

Search for a book. spine builds a spine for it, using the colors from the real
cover and the thickness from the real page count. That's most of what it does.

---

## Why

Most reading apps do too much. They want to be a social network, a
recommendation engine, a stats dashboard, and a review site at the same time.

But reading is an analog thing. You finish a book, you put it on a shelf, and
sometimes you show the shelf to someone. A bookshelf doesn't recommend your next
read. It doesn't calculate your pace. It just holds what you've read.

When you want to show a friend your books, you take a photo of the shelf and
text it to them. You don't post it to a feed.

spine is the shelf, without the rest.

There's a practical side too. In a lot of cities, having room for a physical
bookshelf is a luxury. Plenty of people read constantly and have nowhere to put
anything. This gives them a shelf anyway.

---

## What it does

**Builds a spine from a real book.** Search a title. spine pulls the cover,
finds its dominant color, and uses the page count to set the thickness. A short
novel gets a thin spine. A long one gets a thick spine.

**Sets the type like a real book.** Seventeen different typefaces, assigned per
book, so a shelf looks like books from different publishers instead of one
template. Korean titles are set vertically in MaruBuri, the way Korean spines
are actually printed.

**Lets you hide a book.** Tap any spine to turn it around. You see the page
edges instead of the title. Not everything you read is everyone's business.

**Exports the shelf as a photo.** One image, or several pages if your shelf is
long. Meant to be texted to a friend, not posted.

**Works across languages.** Search in English, Korean, or any language Google
Books covers. Korean titles get their own catalog chain and vertical typography.

---

## What it doesn't do

No recommendations. No reading goals. No streaks. No social feed. No account.

I'll probably add bulk import later, because typing in a hundred books one at a
time is genuinely annoying. But the core stays the same. Keep track of what
you've read. Look at it. Show someone.

---

## Some things I learned building it

**Three book APIs shut down during this project.** Goodreads killed its API in
2020. Naver ended its book search in July 2026 with no replacement. Aladin
announced it would stop accepting new applications in September 2026 and shut
down entirely on November 1.

That changed how I built it. Book data is now cached on the device when you add
a book. If every API disappeared tomorrow, your existing shelf still works. You
just couldn't add new books. API calls also go through a proxy I control, so a
dead service is a server-side fix instead of an App Store release.

**Naive color extraction fails on book covers.** My first version picked the
most common color. That kept returning white, because a white title block is one
uniform color while a photographic background spreads across dozens of shades.
The count was right and the answer was wrong. I weight colors now by how
distinctive they are, so saturated mid-tones beat near-white.

**Korean spines aren't rotated, they're stacked.** I built the first version
with the whole title rotated ninety degrees, which is how Western spines work.
Korean spines stack each character upright. iOS also ships no Korean serif font,
so Hangul was rendering in a UI font next to carefully chosen Latin serifs. Both
had to be fixed separately.

**I cut a feature because it didn't do anything.** I built a shuffle button
early on. Then I asked what it was for. Spotify shuffle works because it picks
something for you. Randomizing a shelf you're already looking at does nothing. I
replaced it with sort.

---

## Status

Built in Swift and SwiftUI. Currently in review for the App Store.

The source is in a private repo. This one holds the project notes and the
privacy policy.

---

## Credits

Book data from Google Books, Open Library, Kakao, and Aladin.
Korean type set in MaruBuri by NAVER, under the SIL Open Font License.
