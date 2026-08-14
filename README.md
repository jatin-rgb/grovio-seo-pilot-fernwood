# Fernwood Climbing Co. — pilot test site

A small static site used to exercise the Grovio Search Visibility Squad end to
end: the audit agents find issues, file them as Harness issues in `backlog`, a
human approves one, and the `seo-implementer` agent opens a pull request
against this repository.

Fernwood Climbing Co. is **fictional**. The address, phone number and email are
placeholders and resolve to nothing.

**Plain HTML on GitHub Pages, deliberately.** There is no build step, no
package manifest and no CI, which matches the pilot rule that the implementer
never runs a repository's code — so the files an agent edits are exactly what
gets served.

## The SEO here is imperfect on purpose

Do not fix any of it by hand. That is the work under test.

Planted defects, so you can score what the audit actually finds:

| Page | Planted defect |
|---|---|
| every page | No `meta description` except `classes.html` |
| every page | No structured data at all — no `LocalBusiness`, no `FAQPage` |
| every page | No canonical tag, no Open Graph tags |
| `pricing.html` | Title is 84 chars — truncates in SERP |
| `pricing.html` | Two `<h1>`s (`Prices` and `Getting here`) |
| `pricing.html` | Four FAQ-shaped `h2` + answer pairs with no FAQPage markup |
| `index.html` | `<img>` with no `alt` |
| `index.html` | Link text is "Click here" |
| `index.html` | Opening hours and address in prose only — no `LocalBusiness` |
| `classes.html` | No `<h1>` — starts at `<h2>` |
| `blog/` | No internal links back to Pricing or Classes |
| `sitemap.xml` | Lists only 4 of the 6 pages — `classes.html` and the blog post are
  orphaned from it, so the crawl-vs-sitemap cross-check has something real to find |

The `FAQPage` gap on `pricing.html` is the clearest single finding to promote
first: the answers are already written, the change is additive, and it is easy
to verify in the diff.
