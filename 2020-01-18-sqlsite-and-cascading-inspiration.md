# SQLSite and cascading inspiration

It’s been a long time since I’ve had an out-of-work open source side project, but over the last couple of weeks or so I’ve been working on [SQLSite](https://github.com/j4mie/sqlsite).

SQLSite is a simple web framework that serves data from an [SQLite](https://sqlite.org/index.html) database. The URL structure and routing is configured in a table in the SQLite database. Even the templates and static files are stored inside the SQLite database using the [SQLite Archive container format](https://sqlite.org/sqlar.html). The only language you need to know to build your website is SQL (along with HTML and CSS of course), and the website is entirely self-contained in a single database file.

Where this gets really interesting is that any other data stored in the SQLite database can be queried in any way you like and pulled in to the website or application you’re building.

For example, this blog is powered by SQLSite, and is running on a Raspberry Pi Zero W in my house. I’ve set up a crontab entry which looks something like this:

```
*/15 * * * * sqlite3 /path/to/loadavg.sqlite "INSERT INTO loadavg (load) VALUES ($(cat /proc/loadavg  | cut -d ' ' -f 3))"
```

I can then use that data to generate a graph:

*Graph removed*

In case it’s not clear: this is real, live data (the maximum 15-minute load average in each day over the last 7 days), generated when this page was rendered by running a database query:

```sql
ATTACH DATABASE 'loadavg.sqlite' AS loadavg;

SELECT
  strftime('%Y-%m-%d', timestamp) AS day,
  max(load) AS max_load
FROM loadavg.loadavg
WHERE timestamp > DATETIME('now', '-7 days')
GROUP BY day
ORDER BY timestamp;
```

I can imagine SQLSite being handy for people who like the idea of a static website generator, but find themselves wanting more flexibility. It would be useful for people who write about and publish data, or want to throw together very quick public-facing JSON APIs for datasets which are a bit too complex to publish as static JSON.

## Inspiration

The idea for SQLSite has been bouncing around in my brain since I stumbled across [Datasette](https://datasette.readthedocs.io/en/stable/) a few months ago. [Simon](https://simonwillison.net/)’s interest in data journalism has pushed him in the direction of building infrastructure for exploring and publishing data. SQLite is the perfect format for this: the data is contained in a single file and so is easy to manage and share, but unlike JSON or CSV, it's real relational data backed by a very powerful database engine.

SQLSite is really a stripped-back Datasette, with the “exploring” bit taken out. The `sql` Jinja template function in SQLSite is ~~stolen from~~ closely based on [datasette-template-sql](https://github.com/simonw/datasette-template-sql). I see SQLSite slotting into the Datasette ecosystem nicely, as it can benefit from all the [excellent tooling](https://github.com/simonw?utf8=%E2%9C%93&tab=repositories&q=sqlite&) that Simon and others are building for getting [data from disparate sources](https://github.com/dogsheep) into SQLite.

Discovering Datasette led me down a path of remembering just how mind-bogglingly brilliant SQLite itself is. It’s rekindled my love for the  idea of public-domain software (SQLSite is published under the [unlicense](https://unlicense.org/), which is based on SQLite's public domain license). I've started using SQLite at work for all sorts of things (manipulating and parsing log data, analysing dependencies for all of our GitHub repositories, etc) and at home (for querying nearly five years of Facebook Messenger conversations with my wife). I feel like I’ve rediscovered the power of SQL after years of only really thinking about databases through ORMs and query builders. Ideas for in-work and out-of-work projects are piling up. It’s even inspired me to start writing again (along with [this article](http://gregorygundersen.com/blog/2020/01/12/why-research-blog/) about keeping a research blog).

For me, inspiration is one of those things that’s unpredictable and uncontrollable. Next week my brain might entirely lose interest and spend all its free cycles thinking about something else. But when the rabbit hole of inspiration opens up, you’ve just got to see how deep it goes.

**Update October 2021**: "*next week my brain might entirely lose interest*" - this didn't quite come true in a week, but it did eventually. I've archived the SQLSite project on GitHub.
