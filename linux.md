# Гайд по Linux Shell

## Работа с папками и директориями
* pwd - print working directory
* ls - list (показать все папки в директории)
  * ls route - показать содержимое папки по пути
  * -l - узнать полную информацию о папке и правах доступа
* cd nameFolder - перейти в папку
* clear - очистить терминал
    
* touch nameFile.txt - создать файл с именем nameFile с расширением txt
* nano nameFile.txt - открыть файл для редактирования, если файла с таким именем нет, то создать его
* mkdir - создать папку
* cp test.txt folder/test.txt - скопировать файл test.txt в папку folder и вставить файл с именем test.txt
* mv test.txt folder/newFolder - переместить файл test.txt в папку folder
* rm test.txt - удалить файл test.txt
  * rm folder/* - удалить все файлы (но не папки!)
  * rm folder/*.txt - удалить все файлы с расширением txt
  * rm -rf folder - удалить папку
  * 
## Права пользователей

Чтобы выполнить команду с правами администратора, перед командой необходимо прописать ***sudo*** (super user do)  
* sudo su - зайти в режим администратора в косноли (su - switch user)  
* sudo chown root:root file.txt - поменять владелецев файла (chown - change owner)
* sudo chmod 664 - 4-r, 6-wr, 7-полный доступ (chmod - change mode)
    
* sudo chown -R root:root folder - поменять владельцев папки
* sudo chmod -R 764 - 4-r, 6-wr, 7-полный доступ (chmod - change mode)
