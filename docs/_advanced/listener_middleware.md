---
title: Listener middleware
lang: en
slug: listener-middleware
order: 5
---

<div class="section-content">
Listener middleware is only run for the listener in which it's passed. You can pass any number of middleware functions to the listener using the `middleware` parameter, which must be a list that contains one to many middleware functions.
</div>

```python
# Listener middleware which filters out messages with "bot_message" subtype
def no_bot_messages(message, next):
    subtype = message.get("subtype")
    if subtype != "bot_message":
       next()

# This listener only receives messages from humans
@app.event(event="message", middleware=[no_bot_messages])
def log_message(logger, event):
    logger.info(f"(MSG) User: {event['user']}\nMessage: {event['text']}")
```
