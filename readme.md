git config --global user.name ""
                    user.email ""
git log - вся информация о комитах
git checkout "хэш коммита" - вернуться к состоянию комита
git pull origin master - получить все комиты
git branch - показать все ветки
git branch name - создать ветку с именем name 
git checkout name - переключиться на ветку с именем name
git merge name - слить ветку name с веткой master (необходимо находиться в базовой ветке)
git rebase name - перенести все комиты с ветки name в ветку master (необходимо находиться в базовой ветке)

git cherry-pick "хэш коммита" - переносит коммит в конец ветки, где сейчас находимся


После каждого изменения master необходимо в feature ветку подгужать изменения
Изучить GIT Flow

Если после merge возникает конфликт необходимо исправить файл где до = ваша версия, а после версия из вливаемой ветки

git revert "hash" - создаёт новый коммит с отменёнными изменениями из прошлого коммита

git reset --soft "hash" - сотрёт из лога коммиты, но изменения в этих коммитах оставит и поместит в индекс гита

git reset --hard "hash" - сотрёт из лога коммиты и данные в них