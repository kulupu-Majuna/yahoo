# tokipona@yahoogroups.com archive
This repo is a readable archive of the yahoo groups toki pona mailing list.

The data comes from the archive hosted on the [now-defunct toki pona forums](http://forums.tokipona.org/), which was both broken (all threads 404) and hard to read (the posts have been stripped of any line breaks and the quotation format is inconsistent), as well as posts from after [2007-11-19] coming from [GMane](https://gmane.io/) (gmane.culture.language.tokipona) via [narkive](https://tokipona.yahoogroups.narkive.com/).

These files need to be manually edited to add linebreaks and tag their content, hence the need for the repo. 
Currently only a very small portion of threads have been analysed.

## Building
This repo is structured as a jekyll website, you'll be able to view it on github pages.

To host the site locally, make sure you have ruby installed then run `bundle install` and `bundle exec jekyll serve` from the folder containing this README.

## File Structure

Each email thread has a corresponding file `threads/<hash>.md` where hash is some unique identifier for it. The actual emails in each thread are found in `_posts/_<hash>/0.md`, `_posts/_<hash>/1.md`, etc.

A thread file is in this format
```yml
---
title: 'Email subject line'
posts: 1 # the number of emails in the thread
hash: 'unique identifier, matching the file name'
author: 'Email address or display name' # same as first email's author
date: 2008-11-29T02:05:00+00:00 # same as first email's date
sources: # at least one URL to where the content was sourced from
  - http://forums.tokipona.org/viewtopic.php?t=id
tags: # List of tags (defined in _data/tags.yml). If not present, this indicates the thread has not been analysed.
  - english
  - tokipona
  - languagechange
  - poll
---
```
The hash field is a meaningless identifier that associates the thread with the folder `_posts/_<hash>`. The 'posts' field is an integer corresponding to the number of post files in this folder, which will be titled `0.md`, `1.md`, `2.md`, etc. The order of these is important for interpreting 'nestinglevel' (which posts are in reply to which)

A post file is in this format
```md
---
author: "Email address or display name of sender"
date: 2009-09-06 01:03:51 UTC # date the email was sent
nestinglevel: 0 # if zero, this is the head of an thread, if non-zero N then this is in reply to the most recent email with nestinglevel N-1 (in the current thread with maximum filename id less than the current)
---
Basic markdown representation of email. If a post has been proofread it will be in the following format, otherwise it could be anything.

Plain linebreaks as used in this paragraph represent automatic line wrapping inserted by the original archive's source.
These are represented in forums.tokipona.org sources as two words without a space between (likethis) which occur in a 
consistent position range (eg every 70-80 characters) and often in the middle of sentences. These should probably be
shown as one continuous paragraph

Slash-prefixed line breaks like as used in this paragraph indicate a line break intended by the author.\
These are represented in forums.tokipona.org sources as two words without a space between that occur outside of the normal word wrap wrange, \
or as a full stop immediately followed by the next sentence.Like this.

Empty lines as above act as seperators between distinct paragraphs. 
These are either directly in the source or are representend in the same way as slash-prefixed line breaks but where a paragraph break makes more sense (ie when introducing a new topic, when doing anything but comparing lines side by side).

When links have known archives, they will be represented like this: [https://web.archive.org/](https://web.archive.org/web/20020124143456/http://web.archive.org/index.html) or wikipedia ?oldid= urls prefered. When they don't, they will just be represented as plaintext urls like https://tokipona.org/.

Ocassionally you will see internal links, if this is a link to an email on the same page it will be of the form [original url](#postN) where N is a number. If it's a link to a different page it'll be of the form [original url]({% link path/to/file.md %}#postN) (the #postN might not be present).

Other formatting includes:
- Bullet point lists, indicated with lines starting with '- ' like so (it's okay to just show these in plaintext)

> Quotations, which are shown as lines prefixed with a '> '.
> When a quotation is just the entire previous email, it will be ommitted.
>> Multiple layers of quotations are written with repeated '>'.
>
> Quotation blocks always end with an empty line

Email signatures are indicated by inserting three asterisks before them.
These indicate text that is repeated at the all an author's emails, that is generally irrelevant to the topic at hand. 

***

Text in a signature could be safely ignored. Their urls don't need to be archived.

forums.tokipona.org auto-inserted smilies such as `![:)](images/smilies/icon_e_smile.gif "Smile")`, which should be restored to their original text form (eg `:)`).
```

## Contributing
PRs welcome! Pick some thread, add newlines to all the files in the `_posts/_XXX` folder, then change the `/threads/XXX.md` file to have the relevant tags (defined in `_data/tags.yml`). Repeat this as many times as you want then open a pull request with your changes. :D