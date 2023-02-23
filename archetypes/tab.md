---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
activeTab: "{{ lower .Name }}"
layout: "single"
---
