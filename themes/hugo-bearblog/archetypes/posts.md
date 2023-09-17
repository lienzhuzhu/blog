+++
title = "{{ replace .Name "-" " " | title }}"
date = "{{ .Date }}"
draft = true
# description = ""

tags = [{{ range $plural, $terms := .Site.Taxonomies }}{{ range $term, $val := $terms }}"{{ printf "%s" $term }}",{{ end }}{{ end }}]
+++

