# AGENTS.md

# OMG Serviteca, reglas permanentes para agentes

## Fuente de verdad
El repositorio Git y la rama `master` representan el estado compartido del proyecto entre Codex y Claude Code.

## Inicio obligatorio
Antes de modificar código:
1. Ejecutar `git status`.
2. Confirmar la rama con `git branch --show-current`.
3. Revisar `git remote -v`.
4. Ejecutar `git fetch origin`.
5. Confirmar que la rama de trabajo es `master`.
6. Si el árbol está limpio, ejecutar `git pull --ff-only origin master`.
7. Si existen cambios locales, divergencias o conflictos, analizarlos antes de sincronizar. No destruir trabajo existente.
8. Leer `docs/OMG_UX_REDESIGN.md`.
9. Leer `docs/BITACORA.md`.
10. Revisar las tareas abiertas antes de comenzar.

## Rama
Trabajar directamente sobre `master`, salvo instrucción expresa del usuario.

No crear ramas nuevas por iniciativa propia.

## Protección
No ejecutar de forma automática:
- `git reset --hard`
- `git clean -fd`
- `git push --force`

No eliminar archivos o cambios de otro agente sin investigar su función.

## Implementación
Reutilizar la arquitectura existente.
No rehacer el proyecto desde cero.
No inventar información comercial.
Mantener responsive, SEO, accesibilidad y rendimiento.
La dirección oficial de OMG Serviteca es: Cra. 1 N.º 17-47, Variante, Chía.

## Bitácora obligatoria
`docs/BITACORA.md` es el registro compartido de continuidad.

Antes de trabajar:
- revisar tareas pendientes;
- revisar decisiones recientes;
- identificar el último trabajo realizado.

Después de trabajar:
- registrar fecha;
- agente utilizado;
- tarea ejecutada;
- archivos principales modificados;
- pruebas realizadas;
- resultado;
- pendientes;
- commit generado.

No marcar una tarea como terminada si no fue validada.

## Finalización
Antes de terminar:
1. Revisar `git diff`.
2. Ejecutar pruebas disponibles.
3. Ejecutar lint si existe.
4. Ejecutar build si existe.
5. Actualizar `docs/BITACORA.md`.
6. Ejecutar `git status`.
7. Crear un commit descriptivo.
8. Ejecutar `git push origin master`.
9. Verificar que local y `origin/master` quedaron sincronizados.

Informar al usuario el hash corto, mensaje del commit, resultado del build, pruebas y push.
