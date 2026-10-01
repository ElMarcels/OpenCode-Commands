---
description: Commit y push completo de todos los cambios al branch main de GitHub
---

Realiza un push completo de los cambios del proyecto al branch `main` del repositorio remoto de GitHub.

## Contexto actual del repositorio

Rama actual:
!`git branch --show-current`

Remotos configurados:
!`git remote -v`

Estado del repositorio:
!`git status --short`

Resumen de cambios:
!`git diff HEAD --stat`

Últimos commits:
!`git log --oneline -5`

## Mensaje de commit

Mensaje proporcionado por el usuario (puede estar vacío): `$ARGUMENTS`

## Instrucciones

Sigue estos pasos en orden y detente si alguno falla:

1. **Verificaciones previas**
   - Confirma que estás dentro de un repositorio git y que existe el remoto `origin`.
   - Si no hay ningún cambio (working tree limpio) y no hay commits locales pendientes de push, informa al usuario y termina.

2. **Revisión de seguridad antes de añadir archivos**
   - Revisa la lista de archivos modificados/nuevos.
   - NO añadas archivos que parezcan secretos o credenciales (`.env`, `*.pem`, `*.key`, `credentials.json`, tokens, etc.). Si detectas alguno que no esté en `.gitignore`, avisa al usuario y pídele confirmación antes de continuar.
   - Evita también artefactos pesados o generados (`node_modules/`, `dist/`, `build/`, `*.log`) si no están ignorados.

3. **Staging**
   - Ejecuta `git add -A` para incluir todos los cambios (nuevos, modificados y eliminados).

4. **Commit**
   - Si el usuario proporcionó un mensaje en `$ARGUMENTS`, úsalo tal cual.
   - Si está vacío, analiza el diff (`git diff --cached`) y redacta un mensaje claro siguiendo Conventional Commits (`feat:`, `fix:`, `docs:`, `refactor:`, `chore:`, etc.), con una primera línea de máximo 72 caracteres y, si hace falta, un cuerpo breve explicando el porqué.
   - Ejecuta `git commit -m "<mensaje>"`.

5. **Sincronizar con el remoto**
   - Ejecuta `git fetch origin`.
   - Si la rama actual no es `main`, avisa al usuario de que los cambios se enviarán a `main` desde la rama actual y pide confirmación antes de continuar.
   - Ejecuta `git pull --rebase origin main` para integrar posibles cambios remotos.
   - Si hay conflictos, NO los resuelvas automáticamente: detente, lista los archivos en conflicto y explica al usuario cómo proceder.

6. **Push**
   - Ejecuta `git push origin HEAD:main`.
   - NUNCA uses `--force` ni `--force-with-lease`. Si el push es rechazado, explica el motivo y detente.

7. **Confirmación final**
   - Muestra el hash y mensaje del commit enviado (`git log -1 --oneline`).
   - Confirma que el push se completó correctamente con el resultado de `git status -sb`.

## Reglas

- Responde siempre en español.
- Sé conciso: muestra solo los comandos ejecutados y un resumen final.
- No modifiques la configuración de git (`git config`) ni reescribas el historial.
