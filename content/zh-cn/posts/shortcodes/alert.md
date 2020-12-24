---
categories:
- Shortcode
date: "2020-10-22"
description: 关于 Alert Shortcode 的详细描述
featured: false
images: []
series:
- 用户手册
tags:
- Alert
title: Alert Shortcode
---

本文展示了如果使用 `alert` shortcode。
<!--more-->

```markdown
{{</* alert "Message" [type] */>}}
```

> The parameter `type` is optional. Default to `info`.

## Info

```markdown
{{</* alert "Info" */>}}
```

{{< alert "Info" >}}

## Success

```markdown
{{</* alert "Success" success */>}}
```

{{< alert "Success" success >}}

## Warning

```markdown
{{</* alert "Warning" warning */>}}
```

{{< alert "Warning" warning >}}

## Danger

```markdown
{{</* alert "Danger" danger */>}}
```

{{< alert "Danger" danger >}}
