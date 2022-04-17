---
author:
    name: Hamza Mogni

title: How I code for 8 hours without feeling tired.
description: I thought it was okay to just sit down at my desk, open my laptop, take a task from my To-Do list, and code until I felt tired.
img: https://miro.medium.com/max/700/1*rX8eWKG10xtW_8Ojiq_OBg.jpeg
alt: How I code for 8 hours without feeling tired.
---

# Documentation

## What is it? 🤔

In a nutshell, Mouhim Scrapers are a set of scripts with the purpose of downloading, parsing, and extracting news articles from online Moroccan newspapers. We extract the article content and save its image to serve it to our client applications.

For now, and this is subject for change in the near future, this repository is providing 2 services, the first one being the very act of scraping articles and downloading images, while the second one is serving articles’ images through a Restful API.

The scrapers are built using [BeautifulSoup](https://beautiful-soup-4.readthedocs.io/en/latest/), which is a python library for parsing HTML and then extracting the needed information. The HTTP API endpoint serving images is built using [FastAPI](https://fastapi.tiangolo.com/).

## How does it work ? ⚙️

### Workflow

The following is a simplified flow that the scrapers take to get articles:

1. Iterate over the list of scrapers (one scraper for each newspaper), for each one:
	1. Download the main page for each category (politics, economy, woman..etc) following the newspaper’s configuration.
	2. For each of those pages, extract every article’s link.
  	3. Send those lists to our server, the server compares the list of links with the database and keeps only links that don’t already exist (meaning that it is indeed a new article), then sends back the cleaned links to scraper.
  	4. Scraper then proceeds to actually download the new articles, following these steps:
    	1. Download article’s HTML page.
    	2. Extract article’s title, content, date, and image link.
    	3. Parse article’s date (translation, reordering...etc) to a machine-readable format.
    	4. Download article’s image, assign a unique name to it and save it to local file system (more on this later).
    	5. Append article content to new articles list, and then send that list to our server to save on our database and serve to clients.
2. Iterate to next newspaper.


# FAQ ✅

## Why there is a step _b_ and _c_ ?

The scrapers and the database server work together, cooperating and communicating to each other to complete their tasks. Steps b and c were added as a means of optimization, we do that to make the scrapers download the least possible amount of data, we aim to download only data we are in need of, therefore, there is no need to scrape every main page article and only then store the new ones. Instead, we get only their links, send it to database server to clean and then download only the new articles.

## Why don’t we scrape only the last 2 articles of each category?

Indeed, scraping for example only the last 2 articles of each category will allow us to remove steps b and c, and that’s what we were actually doing in an earlier version. But, the problem with this approach is that we don’t know beforehand the newspaper’s frequency of publishing new articles, so that if we run the scraper every 5min and the newspaper manages to publish more than 2 articles for whatever reason (believe me, some newspapers do ! 🤨🥴), then we will lose a fair amount of articles and never get to download them. It then became clear that we have to make a trade-off, and we handled it the way described earlier (getting all links on main page, clean it, and then scrape the remaining). The fact that we are getting only every link first allows us to not miss articles while adding a minimal communication between our servers.

## How do we name images?

Each image gets a unique name assigned to it, and based on that name we store it to a specific order. we follow this pattern or three blocks in naming images:

{**_newspaper}-{YYYYMMDD}-{uuid4}.{ext}_**

where newspaper is the newspaper name, YYYYMMDD is the date of download, and uuid4 is a hexadecimal auto generated unique sequence of charachters, and ext is the image file extension. For example, the following is an image from al3omk newspaper, downloaded on November 29th, 2021.

**_al3omk-20211129-0bf2ac94324d477dbabf83a5b715d087.jpeg_**

A couple of questions could be raised here questioning this naming convention, allow us to explain why those decisions have been made:

- the newspaper name and the date of download are used as a path of directories where to store each image, for example the al3omk image above will be stored in this path: **al3omk/2021/11/29/al3omk-20211129-0bf2ac94324d477dbabf83a5b715d087.jpeg**, notice the nested tree of directories **al3omk > 2021 > 11 > 29.** You may be asking yourself now why don’t we just store images in one single directory since the image name is already guaranteed to be unique, that’s a valid question, but here we are taking into consideration that a file-system will under perform if there is a huge number of files in a single directory, hence we create a directory for each day of the year for each newspaper.
- the uuid4 block is an almost guaranteed sequence of characters to be unique, in fact even if you generate 1 billion UUID every second for 100 years, your chance of getting a duplicate is only 50%. Check this wikipedia [link](https://en.wikipedia.org/w/index.php?title=Universally_unique_identifier&oldid=755882275#Random_UUID_probability_of_duplicates) for more details.

## How do we schedule next scrapers run?

Spoiler: We use Systemd

> systemd is a suite of basic building blocks for a Linux system. It provides a system and service manager that runs as PID 1 and starts the rest of the system.

> systemd provides aggressive parallelization capabilities, uses socket and D-Bus activation for starting services, offers on-demand starting of daemons, keeps track of processes using Linux control groups, maintains mount and automount points, and implements an elaborate transactional dependency-based service control logic. systemd supports SysV and LSB init scripts and works as a replacement for sysvinit.

> Other parts include a logging daemon, utilities to control basic system configuration like the hostname, date, locale, maintain a list of logged-in users and running containers and virtual machines, system accounts, runtime directories and settings, and daemons to manage simple network configuration, network time synchronization, log forwarding, and name resolution.

there is a time gap of between 15min and 30min between each scraper run, the exact amount of time is chosen randomly by systemd on each reschedule, we do that to mimic a human being browsing internet. The idea behind this is that if we run scrapers every 15min for example (a fixed amount of time), then newspapers could easily detect bot behaviour and block our IP, by randomizing rescheduling we make it harder for servers to distinguish between us and genuine humans.

# Current flaws

Following are flaws to be improved:

- date parsing is very limited, it should be centralized and dynamic as much as possible, right now we are not getting the accurate date for a significant number of newspapers (we instead store date of scraping)

# Ideas to implement

Following are ideas and reworks to be implemented in future

- Parallelism. Right now are scraping under 20 newspaper, it takes the scraper around 12min to complete one round. we do iterate over them sequentially, however, it would be much better to make these scrapers work in parallel, by implementing something like a thread pool...etc. This will make the scraper much quicker, hence allowing us to efficiently scrape more data and easily extend to more newspapers.
- Using Cloud Storage. instead of storing images on local disk in the same server, we may store them on cloud storage. this will reduce our storage cost and make our scraper have less responsibilities.
- Dockerize and use a PaaS: Instead of deploying on a VM instance, we can dockerize the repository, and use a cloud service to run the container only when needed. this will hugely reduce our costs. Right now the VM is under utilized, running 24/7 but actually working only a small percentage of time.
