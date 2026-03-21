---
layout: post
title: linkedin job filter, chrome extension
tldr: a lightweight chrome extension that hides spammy linkedin job posts using keyword filters
date: 2025-09-25
---
i was extremely tired of seeing spammy recruiter posts and job listings clutter my linkedin jobs feed, so i created a lightweight tool that can take these keywords and hides those posts instantly.<br><br>
<a href="https://github.com/itsabiral/LinkedIn-Job-Filter" target="_blank" rel="noopener noreferrer">
**_github repo_**
</a><br>

**installation**<br>
```
clone the repository: 
git clone https://github.com/itsabiral/LinkedIn-Job-Filter.git

open chrome and navigate to chrome://extensions/
enable "developer mode" (toggle in the top right)
click "load unpacked"
select the folder containing this extension
```
**usage**<br>
```
navigate to linkedin job listings (e.g., https://www.linkedin.com/jobs/)
click the extension icon in your chrome toolbar
enter keywords you want to filter out (e.g., "contractor", "recruiter", "part-time")
click "add" to add the keyword to your filter list
jobs containing any of your keywords will be automatically hidden
use "remove" to delete individual keywords or "clear all" to remove all filters
```
**privacy**<br>
```
all data (keywords) is stored locally in chrome's sync storage
no data is sent to external servers
the extension only runs on linkedin job pages
```
<div style="display: flex; gap: 1rem; flex-wrap: wrap; justify-content: center;">
  <img
    src="{{ '/assets/images/portfolio/linkedin-hide/linkedin.jpg' | relative_url }}"
    alt="linkedin-hide"
    style="width: 400px; max-width: 100%; display: block;"
  />
  <img
    src="{{ '/assets/images/portfolio/linkedin-hide/linkedin-2.jpg' | relative_url }}"
    alt="linkedin-hide"
    style="width: 600px; max-width: 100%; display: block;"
  />
</div>