## crear server 
git init --bare random.git

# iniciar repositorio en carpeta
git init

## estado
git status

## clonar
git clone https://...
git clone https://odtorres@bitbucket.org/odtorres/tutorial.git

## añadir todo
git add .

## commit
git commit -m "comentario del commit"
git commit -am "comentario del commit" archivo

## Mover para rama o Crear rama en caso de no estar
git checkout -b extended_unstable

## listar ramas
git branch

## sobrescribir rama existente y iniciar desde la revision
git branch -f rama rev

## When starting work on a new feature, branch off from the develop branch
git checkout -b myfeature develop

## guardar los cambios desde la rama
git merge rama

## para deshacer merge
git reset --hard @{1}

## mezclar un commit de otra rama
git merge rama commit

## mezclar 2 ramas
git merge destino origen

## quitar rama en el repo
git branch --unset-upstream

## poner rama nueva en el repo
git push --set-upstream origin ramaRepo

#Push
git push origin NombreRama

## descarga y guarda los cambios desde el repositorio
git pull

## actualizar origin del repo borrando ramas 
 git remote update origin --prune

## traer los cambios desde el repo sin mesclar
git fetch (luego hacer git merge)

## eliminar
git rm archivo
git rm -f archivo  (forzando)
git rm --cache archivo (del repo pero dejar local)

## mover
git mv origen destino
git mv origen destino -f (sobre-escribe)

## diferencias
git diff
git diff --staged
git diff --stat
git diff branch1 branch2

git diff file1 file2 > dif.patch
git apply dif.patch

## log
git log
git log desde hasta
git show commit

## hacer patch
git format-patch -1 -o new-commits -s

## aplicar patch
git am /dir/fichero.patch

## mostrar los commits
git log - - oneline

## Deshacer cambios a un fichero 
git checkout -- src/rand.c

## No incluir este en el proximo commit
git reset HEAD archivo

## Deshacr commit y conservar los cambios locales
git reset --soft HEAD^

## Deshacr el commit y los cambios locales
git reset --hard HEAD^

git reset --hard # removes staged and working directory changes

## eliminar archivos desconocidos del area de trabajo local
git clean

## configurando el perfil de usuario
git config --global user.name "Oscar Daniel Torres Hernández"
git config --global user.email oscardanieltorres@zoho.com odtorres@uci.cu

## configurando alias además
git config --global alias.st status

## confirmar ssl certificados
git config http.sslVerify false

## listar repositorios remotos
git remote

## añadir a la lista de repos
git remote add url

## pedir padre
HEAD^

## pedir abuelo
HEAD^^
HEAD~2

## pedir segundo padre
HEAD^2

## nesimo valor
@{n}

## ayer
 master@{yesterday}

## Banderas
M:Modified
C:Copi-edit
R:Rename-edit
A:Added
D:Deleted
U:Unmerged


## Referencias
HEAD
FETCH_HEAD
ORIG_HEAD
MERGE_HEAD
CHERRY_PICK_HEAD

## Generar keyssh
ssh-keygen
### Las llaves estan en C:\Users\Oscar\.ssh

## proxy

git config --global http.proxy http://odtorres:proxypwd@10.0.0.1:8080
git config --global https.proxy https://odtorres:proxypwd@10.0.0.1:8080

Commands to use:

git config --global --unset http.proxy
git config --global --unset https.proxy

Finally, to check the currently set proxy;

git config --global --get http.proxy
git config --global --get https.proxy

## expotar cambios con la estructura
git diff-tree -r --no-commit-id --name-only --diff-filter=ACMRT id_del_cambio | tar -czf cambios.tgz -T - 

## use to discard changes in working directory
git checkout -- <file>

## index error
rm -f .git/index
git reset

## add Existing Git Repo
cd existing_git_repo
git remote add origin http://ip/user/project.git
git push -u origin master

## cantidad de ficheros
git log --pretty="%H" --author="authorname" | while read commit_hash; do git show --oneline --name-only $commit_hash | tail -n+2; done | sort | uniq

## cantidad de commit
git shortlog -s -n

## nombre de los miembros
git log --pretty="format:%an %ae" \
| sed -e 's/^cfchris6 /Christian Franke /g' \
| sort | uniq -c | sort -n -r | sed -e 's/^ *[0-9]* //g'

## The log just outputs the names of the files that have been changed in each commit
git log --pretty=format: --name-only | sort | uniq -c | sort -rg > /d/resumen.txt

## The log just outputs the names of the files that have been changed in each commit
git log --pretty=format: --name-only --author="Oscar" | sort | uniq -c | sort -rg > /d/resumen2.txt

## The log just outputs the names of the files that have been changed in each commit
git log --pretty=format: --name-only --author="Oscar" --since="last year" | sort | uniq -c | sort -rg > /d/resumen3.txt

##
git log --shortstat --author="Oscar" | grep -E "fil(e|es) changed" | awk '{files+=$1; inserted+=$4; deleted+=$6} END {print "files changed: ", files, "lines inserted: ", inserted, "lines deleted: ", deleted }'

git log  --shortstat --author="Oscar" --since="1 Jan, 2013" | grep -E "fil(e|es) changed" | awk '{files+=$1; inserted+=$4; deleted+=$6} END {print "files changed: ", files, "lines inserted: ", inserted, "lines deleted: ", deleted }'

## change date of repository
git log --oneline
git format-patch -o folder -NumberOfCommitToPatch
//change date in the files
git reset --hard idCommitBeforeToRemove
git am .\folder\nameOfThePatch.patch
git log --oneline