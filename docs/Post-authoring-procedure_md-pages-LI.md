---
published: false
---

# Post-authoring-procedure_md-pages-LI

The local Markdown file is the source of truth. [Quid scio?](https://quidscio.github.io/) is the primary public version. LinkedIn Articles distribute selected posts and point readers to the corresponding page on Quid scio?.

The author chooses the publication date and channels, edits the text, and approves the draft. The processor prepares the files, verifies the rendered post, and supplies LinkedIn-ready copy when requested. Treat content approval, a local commit, a push, and a LinkedIn update as distinct actions. Follow the scope the author gives for each one.

## Name and structure the Markdown file

| Channel | File in `_posts/` | Front matter title |
| --- | --- | --- |
| GitHub Pages only | `2026-02-10-AI-Tooling-One-Year-Later.md` | `title: "AI Tooling One Year Later"` |
| GitHub Pages and LinkedIn Article | `YYYY-MM-DD-LI-I-am-a-LinkedIn-Post.md` | `title: "I am a LinkedIn Post"` |

- Start the filename with the publication date in `YYYY-MM-DD` format. Use the approved date for a new post and the original `Published on` date for a LinkedIn import.
- Use hyphens between words in the filename. Keep the title's capitalization in the slug and omit punctuation that does not belong in a URL. Preserve the original spelling and punctuation in the display title. The `LI-` prefix belongs in dual-channel filenames and their URLs.
- Use `layout: default`, the exact `title`, the same `date` as the filename, and a relevant `categories` value. Start a new article body with its title as an H1, then use H2 and H3 for sections. The shared layout displays the publication date above the body.
- Preserve the filename of an already published article when revising it so bookmarks and backlinks stay valid. The current permalink is `/posts/<filename without its date and .md>/`.

Example front matter for a dual-channel article:

```yaml
---
layout: default
title: "I am a LinkedIn Post"
date: 2026-11-27
categories: security
---
```

Place accessible, credited images under `assets/images/<post-slug>/`. For Jekyll image URLs, use `relative_url`. Keep full-width banners short, preserve the artwork's proportions, and use meaningful alt text. Save usable image files locally so the public post does not depend on an expiring LinkedIn media URL.

## Author and processor handoff

1. The author provides the local Markdown path, intended publication date, channel choice, and any image files or credits. For a revision, also provide the current public URL. If LinkedIn is in scope, specify a full Article or an excerpt with a link to the complete version.
2. The processor checks the filename, front matter, headings, links, image placement and credits. Preserve the author's wording unless editing has been requested. Report missing sources, unavailable images, and formatting differences.
3. Preview the page using the [WSL setup in the README](../README.md). Run `script/cibuild` before publishing. Use an isolated checkout for the production build if the preview server is already serving the same generated directory.
4. Return the local preview URL, expected public URL, and verification results. For a dual-channel post, also return the LinkedIn title, the formatted Article body, and a list of images to upload with their locations, captions, and credits.
5. After approval and authorization to push, publish the GitHub Pages version first. Check CI and the Pages deployment for the pushed commit. Open the public URL, confirm it returns HTTP 200, and check the date, images, and self-referencing canonical tag before using that link on LinkedIn.

## Prepare and review LinkedIn copy

Use Jekyll's rendered article body as the rich-text copy/paste source. For the handoff, provide a rendered excerpt or a local browser-readable copy view outside the publishing tree. Put the title in LinkedIn's Title field. Exclude the repeated H1, site navigation, generated date line, and footer from the pasted body. Convert site-relative links that belong in the article to full `https://quidscio.github.io/...` URLs. Leave Liquid expressions and YAML front matter in the Markdown source.

Provide a plain-text fallback if formatting is lost on paste. Use LinkedIn's Article editor to restore headings, links, lists, quotations, or code as needed. Upload the cover and inline images separately using the handoff list. Review the LinkedIn draft and click the source link before publishing. [LinkedIn Article publishing help](https://www.linkedin.com/help/linkedin/answer/a522427) · [LinkedIn Articles media help](https://www.linkedin.com/help/linkedin/answer/a521719)

For a new article that went live on GitHub Pages first, put this source line near the top and link **Read the current version** to the live article URL.

> Originally published on Quid scio? Read the current version.

After a LinkedIn Article is published, record its permanent URL. When the author requests a reciprocal link, add it to the site as **Also available on LinkedIn**. For historical imports, keep the existing **Originally published on LinkedIn** credit.

## Link existing LinkedIn Articles back to GitHub Pages

1. Open LinkedIn on desktop. Under **Me → Posts & Activity → Articles**, open the article's menu and select **Edit article**.
2. Add a short source line immediately after the introduction or near the top of the body. Link the words **Read the current version on Quid scio?** to that specific article's full GitHub Pages URL.
3. Check the destination, then use **Update** to save. Keep the historical publication credit accurate. [LinkedIn edit instructions](https://www.linkedin.com/help/linkedin/answer/a515989)

Suggested wording for these migrated articles:

> I maintain the current version of this article on Quid scio? [Read it on my website](https://quidscio.github.io/posts/LI-I-took-the-CSSLP-exam-and/).

The site declares its own URLs as canonical. A LinkedIn body link gives readers a direct path to the maintained copy. LinkedIn's documented Article SEO settings cover title and description, and search engines choose which URL to show. A distinct excerpt gives LinkedIn readers a reason to click through if a full duplicate is unnecessary. [LinkedIn SEO settings](https://www.linkedin.com/help/linkedin/answer/a6278775) · [Google canonicalization guidance](https://developers.google.com/search/docs/crawling-indexing/canonicalization)

### Backlink destinations for the seven imported articles

| LinkedIn Article | GitHub Pages destination |
| --- | --- |
| [I took the CSSLP exam and ...](https://www.linkedin.com/pulse/i-took-csslp-exam-robert-hines) | [Read on Quid scio?](https://quidscio.github.io/posts/LI-I-took-the-CSSLP-exam-and/) |
| [Equifax Breach - Not Technical?](https://www.linkedin.com/pulse/equifax-breach-technical-robert-hines-cissp-csslp-pmp-pe) | [Read on Quid scio?](https://quidscio.github.io/posts/LI-Equifax-Breach-Not-Technical/) |
| [🚨 IoT Security Alert: 2.7B Records and Network Credentials Found Exposed (but that's not the point!)](https://www.linkedin.com/pulse/iot-security-alert-27b-records-network-credentials-found-robert-hines-fcdpe) | [Read on Quid scio?](https://quidscio.github.io/posts/LI-IoT-Security-Alert-2-7B-Records-and-Network-Credentials-Found-Exposed-but-thats-not-the-point/) |
| [Merry Christmas Condé Nast & Wired Subscribers](https://www.linkedin.com/pulse/merry-christmas-cond%C3%A9-nast-wired-subscribers-robert-hines-dnnke) | [Read on Quid scio?](https://quidscio.github.io/posts/LI-Merry-Christmas-Conde-Nast-Wired-Subscribers/) |
| [CES 2026: Cloud AI Everywhere, Ownership Nowhere, Security Remains an Afterthought](https://www.linkedin.com/pulse/ces-2026-cloud-ai-everywhere-ownership-nowhere-security-robert-hines-j0zle) | [Read on Quid scio?](https://quidscio.github.io/posts/LI-CES-2026-Cloud-AI-Everywhere-Ownership-Nowhere-Security-Remains-an-Afterthought/) |
| [A Risk Management Perspective on AI Catastrophe Risk](https://www.linkedin.com/pulse/risk-management-perspective-ai-catastrophe-robert-hines-nlmie) | [Read on Quid scio?](https://quidscio.github.io/posts/LI-A-Risk-Management-Perspective-on-AI-Catastrophe-Risk/) |
| [They Opened the Gate. Malicious JavaScript Rode In.](https://www.linkedin.com/pulse/opened-gate-malicious-javascript-rode-robert-hines-d0fae) | [Read on Quid scio?](https://quidscio.github.io/posts/LI-They-Opened-the-Gate-Malicious-JavaScript-Rode-In/) |
