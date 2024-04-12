---
title: {{ replace .File.ContentBaseName "-" " " | title }}
date: {{ .Date }}
draft: true
type: posts
keywords:
tags:
categories:
{{- $path := split
(.File.Dir
| path.Clean
| strings.TrimSuffix .File.ContentBaseName
| path.Clean)
"/" -}}
{{ range after 1 $path }}
  - {{ . -}}
{{ end }}
resources:
  - name: featured-image
    src: images/featured-image.png
---

<!--more-->
