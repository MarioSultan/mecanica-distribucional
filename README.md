# Mecánica de Distribuciones

Libro en LaTeX: fundamentos matemáticos y formulación hamiltoniana.

## Estructura

```
main.tex                 ← monta el libro (casi nunca se toca)
preambulo.tex            ← paquetes, colores, comandos y cajas
referencias.bib          ← bibliografía
portada/                 ← cubierta, anteportada, portada, créditos,
                           dedicatoria, prefacio y notación
capitulos/               ← un archivo por tema
apendices/               ← un archivo por apéndice
plantilla-capitulo.tex   ← copia para empezar un tema nuevo
```

## Páginas de libro

Cubierta (fondo oscuro con gaussianas que se estrechan hasta una delta
de Dirac), anteportada, portada interior, créditos, dedicatoria, prefacio,
índice general, notación y convenciones, capítulos, apéndices,
bibliografía e índice alfabético. Todo se edita en `portada/`.

- Epígrafe al inicio de un capítulo: `\epigrafe{Texto}{Autor}`.
- Separador dentro de un capítulo: `\ornamento`.
- Entrada de índice alfabético: `\index{distribucion@distribución!espacial}`
  (la parte `distribucion@` hace que se ordene bien con tilde).
- Para imprimir con capítulos siempre en página impar, cambia `openany`
  por `openright` en `main.tex`.

## Escribir un tema nuevo

1. Copia `plantilla-capitulo.tex` a `capitulos/02-nombre.tex`.
2. Añade `\include{capitulos/02-nombre}` en `main.tex`.
3. Para compilar solo ese capítulo, descomenta `\includeonly{...}` en `main.tex`.

## Entornos disponibles

`definicion`, `teorema`, `proposicion`, `lema`, `corolario`, `ejemplo`
(numerados automáticamente, con etiqueta), `demostracion`, `resultado`
y `observacion` (sin número).

```latex
\begin{teorema}{Normalización}{normalizacion}
...
\end{teorema}
% citar: Teorema~\ref{thm:normalizacion}
```

Prefijos de etiqueta: `def:`, `thm:`, `prop:`, `lema:`, `cor:`, `ej:`.

## Compilar

```bash
latexmk -pdf main.tex     # compilar
latexmk -c                # limpiar auxiliares
```

Cada `push` a `main` compila el libro en GitHub Actions y deja el PDF
en la pestaña **Actions → último run → Artifacts**.

## Flujo con Git

```bash
git add capitulos/02-nombre.tex main.tex
git commit -m "Capítulo 2: borrador de la sección 2.1"
git push
```

Consejo: una rama por capítulo grande (`git switch -c cap-02`) y
`merge` a `main` cuando esté listo.
