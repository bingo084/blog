---
title: {{ replace .File.ContentBaseName "-" " " | title }}
date: {{ .Date }}
draft: true
keywords:
  - draft
tags:
  - draft
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
---

<!--more-->
