# Are All Rom-Com Women Journalists?

URL: https://alexameirelles.github.io/romcoms-project/

*A data-driven look at the professions of romantic comedy protagonists from 1980 to 2025.*

---

## Project

### Goal

If you're a fan of romantic comedies like I am, you've probably noticed how often the female lead works as a journalist, magazine editor, columnist, or TV producer.

This project aims to investigate whether that perception actually holds up by analyzing the professions of protagonists in romantic comedies released between 1980 and 2025.

The final output is a scroll-driven story built with D3.js as part of the Lede Program for Data Journalism at Columbia University.

---

### Main findings

- Journalists are indeed overrepresented among female protagonists. However, **students** are by far the most common category.

- The stereotype seems to be driven largely by a handful of highly influential films from the late 1990s and early 2000s.

- While female protagonists are frequently portrayed as journalists, male protagonists are much more likely to be **businessmen**, reinforcing another familiar romantic comedy archetype.

---

# Data collection

The analysis combines three publicly available IMDb datasets:

- **title.basics** — Film metadata
- **title.ratings** — Ratings and number of votes
- **title.principals** — Principal cast and character names

IMDb datasets:
https://datasets.imdbws.com/

To build the final dataset, I:

- Selected films tagged as both Comedy and Romance;
- Kept only films released between 1980 and 2025;
- Required at least 10,000 IMDb user ratings;
- Manually reviewed the titles to determine whether it should actually be considered a romantic comedy;
- Identified the protagonists;
- Inferred each protagonist's profession.

The final dataset contains **882 films**.

---

# Data analysis

The analysis required considerably more work than simply filtering IMDb.

### Defining romantic comedies

IMDb genres alone were not sufficient. Many titles classified as Comedy and Romance are generally considered dramas, ensemble films, or comedies with only a romantic subplot.

To speed up the review process, I asked both ChatGPT and Claude to identify potential false positives. Every recommendation was manually reviewed before any title was removed.

### Identifying protagonists

IMDb does not explicitly identify protagonists.

I initially selected the first two billed actors (ordering == 1 and ordering == 2), then manually corrected films where the billing order did not match the central romantic couple, which happened more often than I expected.


### Inferring professions

IMDb does not include character occupations.

I used the OpenAI API with a custom prompt that received the movie title and character name and returned the character's profession, occupation, social role, or primary activity.

Because occupations are often omitted from plot summaries, the prompt intentionally allowed broader social roles (such as widow or single mother) rather than immediately returning `null`.

The inferred professions were then manually reviewed in batches of 100 films.

Even after this process, **Unknown** remained one of the most frequent categories. Since it does not represent an actual occupation, I excluded it from the rankings shown in the visualizations. To display the ten most common professions, I first selected the top 11 categories (`head(11)`), removed **Unknown**, and then plotted the remaining top ten.

---

### Manual review

The dataset went through two complete rounds of manual validation to:

- Verify professions;
- Correct protagonists;
- Remove remaining false-positive romcoms;
- Consolidate the final dataset.

---

# Skills and growth

This project was my first experience building an interactive story entirely from code.

Previously, I had created visualizations with tools such as Flourish and Datawrapper, but I wanted to understand how interactive graphics are actually built from scratch.

During the project I learned how to:

- Build charts directly in D3.js;
- Structure SVG elements;
- Create scales and transitions;
- Connect D3 visualizations with Scrollama;
- Build a complete scrollytelling experience;
- Publish the project with GitHub Pages;
- Integrate the OpenAI API into a Python workflow to annotate data automatically.

The official D3 documentation was my primary reference, while AI-assisted explanations helped me understand unfamiliar concepts and debug the code.

---

# Future improvements

Given more time, I would like to:

- Manually review every film individually instead of relying on billing order as the starting point;
- Improve the profession classification with a more structured taxonomy;
- Annotate additional character attributes besides occupation;
- Add more interactive visualizations;
- Improve the mobile experience with a custom scrollytelling implementation rather than a static adaptation.

---

# Tools

- Python
- Pandas
- OpenAI API
- D3.js
- Scrollama
- HTML
- CSS
- JavaScript