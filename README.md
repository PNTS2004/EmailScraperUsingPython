# Email Scraper

This is a small Python script to crawl websites and extract email addresses. Basically, you give it a starting URL, and it goes through the site (up to 100 pages max), looks at the content and links, and grabs any email addresses it finds along the way. It actually works pretty decently for basic use cases.

### How it works

The script starts with the URL you enter. It uses a queue to manage which pages to visit next and keeps track of URLs it’s already seen, so it doesn't visit the same page twice. It uses `requests` to fetch the HTML and `BeautifulSoup` to parse it. Then it pulls out all the `<a>` tags, follows links (even relative ones), and scans the text on each page for anything that looks like an email.

Emails are detected using a regex pattern — it’s pretty straightforward and catches most common formats. Everything it finds is stored in a set, and once it’s done (or hits the 100-page limit), it prints all the unique email addresses it discovered.

### Setup

You’ll need Python installed, and just a few libraries:

* `requests`
* `beautifulsoup4`
* `lxml`

You can install them all in one go with:

```bash
pip install requests beautifulsoup4 lxml
```

After that, run the script with:

```bash
python email_scraper.py
```

It’ll ask for the URL you want to start with, and from there it takes off.

### Example usage

```
Enter Target Url to Scan: https://example.com
[1] Processing https://example.com
[2] Processing https://example.com/about
[3] Processing https://example.com/contact
...
support@example.com
info@anotherdomain.org
```

### A few notes

* It stops crawling after 100 pages (just to avoid hammering a site).
* Doesn’t obey `robots.txt` yet, so don’t use it on websites you don’t have permission to scrape.
* It can’t handle JavaScript-heavy sites — just static HTML.
* If it crashes, it’s probably because the page didn't have a valid `href` or the site blocked the request. I’ve added basic error handling, but it’s not bulletproof.

---

**Disclaimer:** This is for educational use only. Please don’t use this script to spam or harvest emails unethically. Always get permission before scraping a site — or at the very least, double-check the site's terms of use or robots.txt.
