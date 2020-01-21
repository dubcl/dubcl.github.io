---
layout: post
title: Problem sending e-mail on Storwize v3700
date: '2015-10-16 18:51:08'
---

I administrate some IBM Storwize v3700, since some days ago one of them report problem with e-mail notifications, looking in the event log, this show something like "Unable to connect to remote smtp server", and yes, before some connectivity test, the server don't connect with our SMTP server.

When you try to (re)configure the e-mail notification, verifying all inputs and when test you config the task details show:

```language-bash
CMMVC6280E Sendmail error EX_TEMPFAIL. The sendmail command could not create a connection to a remote system.
```

Well, looking on the net and the IBM documentation, the solution is simple, we need change the management IP address, yes, sound weird, but work.

Once time you change the IP, if you go to e-mail setup and test the connection this work again.

![](https://lh3.googleusercontent.com/OUQAGggpuzu2QXsW_lpMKivkGDWnUoLyhLaRI8VahMho0MQ6DF2bvyY9jkej296M3DcIBTUXr8hlWbpz_FnS26GciDwlJDMTd-sGLMcpkldeyT9CrJwX7AZA0-3idoNLUO9_KOTlBWPjEcJI4fU5JD7-skgECGSx7jpws12cSRq3StGsWdwu47ffSlFUbws1YaUuraFVxj0JTSymYHFQE0W7toMnRd7Ae_QHi_Nq3kFZxNO0fuUjgNQUjaTjwWCqAKhndZf5RhDW-xg8tji8DBgZxfeH97BqG6Vb0_KBvb_cFyk020Lxf7t2l8SLdJ-nj7lMfdhEphT6hG6zyY2ZB-upSFAgRCZVIPOee2NoDRifEOPn6kMa2weMkVOLGSUmxPkimEyDwoX85FX4JBm6wgWvlxKhBoKVmf3Z9pkAtbAX_RgBoNXWsIvaCQuHHBM3MDbP_QCbYvVZM8jWzpiEKfypQGPTOjXxrQ8jrVGYagaFX1biRMKasqR-KLRTqjkABXiFTCCC9Qj8NAdF10P10uWWAIcEsn07R1ktWihNXZo=w1905-h957-no)

