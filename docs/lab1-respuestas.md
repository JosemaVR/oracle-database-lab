Apartado 4
4.G
¿a dónde apunta el HEAD? ¿En qué orden aparecen los commits? Responde:
HEAD apunta al commit mas reciente de la rama feature/customer-search.
HEAD   feature/customer-search   3add21e

Los commits aparecen desde el más reciente hasta el más antiguo:
•	3add21e  docs: draft customer search notes
•	e26592c  docs: fix typo in schema notes
•	3dd7c91  docs: add customer schema notes
•	be6d55a  docs: add initial project documentation

4.H
El primer “git status” mostró README.md como modificado en el Working Directory. Después de ejecutar “git add README.md”, el segundo “git status” lo mostró dentro de “Changes to be committed”, es decir, en el Staging Area.
El último comando, “git status -c”, produjo un error porque -c no es una orden válida de “git status”.


Apartado 7
7.1	¿Cuál es la diferencia entre Working Directory, Staging Area y Local Repository? Da un ejemplo de un archivo pasando por las tres.
El Working Directory es la carpeta del proyecto en la que vemos y modificamos los archivos. El Staging Area contiene los cambios seleccionados para el próximo commit. El Local Repository es el historial de commits guardado dentro de .git.
Por ejemplo, al crear o modificar database/schema/clientes.sql, el cambio está en el Working Directory. Con:
•	git add database/schema/clientes.sql
pasa al Staging Area. Finalmente, con:
•	git commit -m "feat: add customers table"
queda registrado en el Local Repository.

7.2	Si modificas un archivo pero no haces git add, ¿aparece ese cambio en tu próximo commit? Explica por qué.
No. “git commit” registra el contenido que se encuentra en el Staging Area, no todos los cambios del Working Directory.
Si añadimos un archivo con “git add” y después volvemos a modificarlo, el commit incluirá la versión que añadimos inicialmente, pero no la modificación posterior.

7.3	¿Por qué git status no mostraba las carpetas vacías que creaste en la Parte C? ¿Qué truco usamos para solucionarlo?
Porque Git controla archivos, no carpetas vacías. Para solucionarlo introdujimos archivos “.gitkeep” dentro de las carpetas “touch docs/.gitkeep”. “.gitkeep” no es una palabra reservada de Git, sino una convención para conservar una carpeta mediante un archivo rastreable.

7.4	Explica con tus palabras qué es HEAD.
HEAD es el puntero que indica dónde estamos trabajando dentro del historial. Normalmente apunta a la rama activa y, mediante esta, al último commit de dicha rama.
Por ejemplo:
HEAD   feature/customer-search   3add21e


7.5	¿Qué diferencia hay entre crear una branch con git switch -c y crear una carpeta nueva con mkdir? ¿Cómo lo comprobamos en la Parte G?
“git switch -c” crea una rama, es decir, un nuevo puntero dentro del historial, y cambia a ella. “mkdir” crea una carpeta física en el disco.
Lo comprobamos ejecutando “ls -la” después de crear la rama. La estructura de carpetas seguía siendo la misma y no apareció ninguna carpeta llamada feature. También comprobamos la rama activa con “git branch".

7.6	Durante el conflicto de la Parte H, ¿qué representaba el contenido entre <<<<<<< HEAD y =======? ¿Y entre ======= y >>>>>>>?
Entre <<<<<<< HEAD y ======= aparecía la versión existente en la rama actual, que en el ejercicio era main.
Entre ======= y >>>>>>> fix/readme-subtitle aparecía la versión procedente de la rama que se estaba intentando fusionar.
Para resolver el conflicto había que escoger o combinar el contenido y eliminar todos los marcadores.

7.7	¿Por qué NO se debe hacer git commit --amend sobre un commit que ya se subió con git push?
Porque “—amend” sustituye el commit por otro con un hash diferente. Si el commit original ya se ha compartido, el historial local deja de coincidir con el remoto.
Para subir el historial reescrito sería necesario forzar el push, lo que puede sobrescribir trabajo ajeno. En ese caso es preferible crear un nuevo commit correctivo.

7.8	Si borras por accidente la carpeta .git de tu proyecto, ¿qué se pierde exactamente? ¿Se pierde también el código fuente que está en el disco?
Se pierde la información interna del repositorio: commits, ramas, etiquetas, Staging Area, configuración local, remotos y seguimiento de archivos.
El código fuente del Working Directory no se borra. Los archivos continúan en el disco, pero la carpeta deja de ser un repositorio Git. Si existe una copia completa en GitHub, se puede recuperar clonando nuevamente el repositorio.


7.9	Explica con tus propias palabras la diferencia entre Git y GitHub, sin usar la palabra "nube".
Git es un programa de control de versiones que permite registrar cambios, crear commits, manejar ramas y fusionar historiales en nuestro equipo.
GitHub es una plataforma web que aloja repositorios Git y añade herramientas de colaboración como Pull Requests, revisiones, Issues y automatizaciones. Git puede utilizarse sin GitHub.

7.10	¿Por qué no se debe subir un archivo .env con contraseñas reales a un repositorio, aunque el repositorio sea privado?
Porque puede contener contraseñas, tokens y claves que podrían quedar expuestos a colaboradores, a una cuenta comprometida o si el repositorio se hace público accidentalmente.
Además, aunque posteriormente se borre el archivo, los secretos pueden permanecer en el historial. El “.env” debe incluirse en “.gitignore” y debe utilizarse un “.env.example” con valores ficticios para documentar las variables necesarias.

7.11	Un compañero te dice: "hice push y ahora GitHub me rechaza el segundo push con 'non-fast-forward'". ¿Qué ha ocurrido probablemente y qué comando ejecutarías primero?
La rama remota contiene commits que no existen en la copia local, posiblemente porque otro compañero hizo push o porque se modificó el archivo desde GitHub.
Según el procedimiento del laboratorio, primero ejecutaría “git pull” y después resolvería posibles conflictos y volvería a ejecutar “git push”.
En un entorno profesional también puede utilizarse primero git fetch origin para inspeccionar los cambios remotos antes de integrarlos.

7.12	¿Qué tipo de Conventional Commit (feat, fix, docs, test…) usarías para: añadir un índice de rendimiento a una tabla, corregir una restricción mal definida, y actualizar el README?
•	Para añadir un índice de rendimiento: “perf: add performance index to customers table”
•	Para corregir una restricción mal definida: “fix: correct customers table constraint”
•	Para actualizar el README: “docs: update README”