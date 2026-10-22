---
layout: home
title: Tochukwu Uzochukwu
heading: Hi, I'm Tochukwu.
lede: >-
  I'm a programmer. I build and maintain web applications used by
  thousands of people. This is where I share what I'm working on and what
  I've learned.
---

## What I do

I've been writing software professionally for more than six years, mostly on
the backend: web applications, APIs, background jobs and the tests that keep
them working.

- **Make systems faster and more reliable.** I find where the time goes and
  cut it. For example, I took our CI test suite from 40 minutes to 9, a 77%
  speedup, and moved our browser tests to a more reliable setup.
- **Keep long-lived applications current and secure.** I handle upgrades and
  keep dependencies up to date and free of known security vulnerabilities.
- **Ship features end to end.** From API design and background jobs to
  containers for development and deployment, working closely with the people
  building the frontend.
- **Work well with AI coding agents.** These days agents write much of the
  code. I review it, steer it, and build the workflows around it.
  I wrote about [my current setup]({% post_url 2026-10-22-why-i-switched-from-vscode-to-herdr %}).

### Tools and languages

- **Languages and frameworks:** Ruby and Rails, Python and Django, Elixir and
  Phoenix, HTML and CSS
- **Databases:** PostgreSQL, MySQL, SQLite
- **Testing:** RSpec, Capybara, Cuprite, Turnip
- **Infrastructure:** Docker, Sidekiq, Linux, CI/CD
- **Workflow:** Git, GitHub, GitLab, Claude Code, opencode, herdr

## Recent writing

{% include post-list.html limit=3 %}

[All posts]({{ '/blog/' | relative_url }})

## Experience

### Velaluqa GmbH, Berlin, Germany

Software developer, March 2022 to present. I build and maintain Rails
applications for healthcare and education clients, including a medical imaging
platform used in clinical trials.

- **Upgrades:** took two production applications from Rails 6.0 to 8.1 and
  Ruby 2.7 to 3.3, including the Devise 5 and Sidekiq 8 migrations.
- **Performance:** cut the CI suite from 40 minutes to 9, then added parallel
  and changed-only test runs; found and fixed N+1 queries, added database
  monitoring, and streamed multi-gigabyte downloads.
- **APIs:** REST and GraphQL APIs, including GraphQL mutations with
  authorization for a React frontend.
- **Testing:** moved browser tests from Selenium to Cuprite, and wrote
  acceptance tests with Turnip and Capybara alongside RSpec.
- **Security:** added Brakeman, bundler-audit and container scanning to CI,
  and fixed vulnerabilities as they came up.
- **Background jobs:** built a Sidekiq job system with progress tracking,
  cancellation and retries, plus user-scheduled recurring tasks.

### Creative Works, Lagos, Nigeria

Backend developer, February 2020 to November 2021. I built web applications
and REST APIs at a fast-moving startup, working with frontend developers to
ship features on tight timelines.

My [resume]({{ site.links.resume | relative_url }}) has the details.

## Background

I studied Pure and Industrial Chemistry at the University of Nigeria, which is
where the little element tile at the top of this page comes from. I moved into
software later, starting with Georgia Tech's computer science fundamentals
course on edX.

Outside of work I play video games, watch football (I'm a staunch Liverpool
fan) and enjoy a good horror movie.
