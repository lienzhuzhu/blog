+++
title = "{{ replace .Name "-" " " | title }}"
date = "{{ .Date }}"
# description = ""

tags = [{{ range $plural, $terms := .Site.Taxonomies }}{{ range $term, $val := $terms }}"{{ printf "%s" $term }}",{{ end }}{{ end }}]
+++

