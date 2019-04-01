---
title: "04 Configure_email_aliases"
date: 2019-04-01T10:14:19-03:00
draft: true
---

Email aliases can be the answer to a wide variety of questions. Do you want to send a copy of all email received by one address to an additional account? Email alias. Do you want to send all of "webmaster's" email to Bob instead? Email alias. In this lesson, we'll demonstrate how to configure email aliases using PostFix. After this lesson, you'll be able to send your own email to whomever you like. Alias responsibly.

`/etc/postfix/aliases`:

```
# emails enviados para webmaster
# serão entregues na caixa postar de user
webmaster: user

# emails enviados para chad
# serão enviados para chad e também para boss
chad: chad, boss
```

```bash
sudo postalias /etc/postfix/aliases
```