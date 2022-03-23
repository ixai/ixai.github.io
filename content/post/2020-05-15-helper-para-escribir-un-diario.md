---
title: Helper para escribir un diario
date: 2020-05-15
slug: helper-para-escribir-un-diario
draft: true
---

Hice una función para ayudarme a llevar un diario en mi computadora. Es simple, yo solo ejecuto `blog` y se crea un archivo para el día de hoy a partir de un template. Si hoy ya existe, solamente lo abre.

```sh
function blog {
	blog_path="${HOME}/Documents/blog"
	today="${blog_path}/$(date +%Y-%m-%d).md"
	if test ! -f $today; then
		cp "${blog_path}/template.md" $today
	fi
	subl $today
}
```

Apenas llevo una semana probandolo, pero me ha servido como acompañante de mi diario físico. Sobretodo para apuntar notas rápidas mientras estoy en la computadora.
