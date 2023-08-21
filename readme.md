#git #yandex
# Git
### Понятия

- Git — это консольный инструмент для работы с локальными и удалёнными репозиториями. Он не связан напрямую ни с одной из платформ и развивается отдельно от них.
- GitHub — платформа, которая работает с Git и упрощает командное взаимодействие.

### Источники

[Git](https://git-scm.com/)  
[GitHub](https://github.com/)

### Командная строка

Наиболее распространенные команды:
- mkdir -p folder/folder 	 *создание вложенных папок*
- ls -a 	*скрытые файлы*
- touch 	*создание файла, через пробел можно несколько файлов*
- cat 		*просмотр текстового файла*
- &&		*объединение команд*
- pwd 	*текущая директория*
- cd ~	*переход в домашнюю директорию / переход в корневую*

### Работа с Git

1. Глобальные настойки  
	git config --global user.name "name"
	git config --global user.email "email"  
	все настройки ~/.gitconfig или git config --list    

2. Инициализация репозитория   
	git init  	*в папке с проектом*  
	git status	 *статус репозитория*  
	удалив папку .git будет удален и репозитарий (rm -rf .git)  

3. Сохранение изменений  
	git add . *или* git add --all *или перечислить нужные файлы*  
	*untracked файл до add*  
	*modified файл между add*  

4. Записываем состояние  
	git commit -m "message" *запись состояния*   
	git log *все "коммиты" в обратном хронологическом порядке*  

### Работа с GitHub

1. GitHub  
	Регистрируемся на GitHub.com  
	Привязываем [[SSH]] ключи. *Не обязательно*   
	Генерируем два ключа и закидываем публичный на GitHub/настройки *Не обязательно*  
	Создаём репозиторий с аналогичным именем проекта на github  

2. Связывание репозиториев  
	*git remote add origin https://github.com/%пользователь%/%репозиторий%.git* связываем репозитории  
	
3. Синхронизация репозиториев  
	*git push -u origin main* (or master) залить на github в первый раз  
	после можно просто *git push*  
 
4. Создание readme  
	Readme.md кладется в папку с проектом  
	Readme составляется посредством языка [[Markdown]]  
	Создание readme - это хороший тон.  

### Хеш коммита

Хеш — основной идентификатор коммита
Все [хеши](Хеш.md) и таблицу `хеш → информация о коммите` Git сохраняет в служебные файлы в *.git*.

Команда *git log* выдаст следующую информацию о каждом коммите:
- хеш коммита - строка из цифр и латинских букв после слова **commit**;
- **Author** — имя автора и его электронная почта;
- **Date** — дата и время создания коммита;
- в конце находится сообщение коммита.

команда *git log --oneline* выдаст только укороченный хеш и сообщение коммита(72 символа)

Последний коммит обозначается словом *HEAD*, при вызове последнего коммита можно указать слово *HEAD* вместо хеша.

### Статусы файлов Git
`untracked`/`tracked`, `staged` и `modified`

Одна из ключевых задач Git — отслеживать изменения файлов  *git status* в репозитории. Для этого каждый файл помечается каким-либо статусом. Рассмотрим основные.

- **`untracked`** (англ. «неотслеживаемый»)  
    Мы говорили, что новые файлы в Git-репозитории помечаются как `untracked`, то есть неотслеживаемые. Git «видит», что такой файл существует, но не следит за изменениями в нём. У `untracked`-файла нет предыдущих версий, зафиксированных в коммитах или через команду `git add`.
- **`staged`** (англ. «подготовленный»)
    После выполнения команды `git add` файл попадает в **staging area** (от англ. _stage_ — «сцена», «этап `процесса`» и _area_ — «область»), то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии `staged`.
- **`tracked`** (англ. «отслеживаемый»)  
    Состояние `tracked` — это противоположность `untracked`. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью `git commit`, а также файлы, которые были добавлены в staging area командой `git add`. То есть все файлы, в которых Git так или иначе отслеживает изменения.
- **`modified`** (англ. «изменённый»)  
    Состояние `modified` означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён.
Для файлов в состояниях `staged` и `modified` обычно не указывают, что они также `tracked`, потому что это состояние подразумевается.
**!!! Обратите внимание:** `staged` и `modified` может быть у одного файла, но у разных его версий, в случае если файл изменили после коммита.

#### Цикл жизни файлов в Git

```mermaid  
flowchart TD; 
classDef class1 fill:#99FFCC, stroke:#000, stroke-width:4px, color:black;
classDef class2 fill:#FF6666, stroke:#000, stroke-width:4px, color:black;

A[/Untracked/]:::class2;
B[staged +tracked]:::class1;
C((tracked)):::class1;
D[modified]:::class2;

A-->|git add|B;  
B-->|git commit|C;  
B-.изменения.->D;  
C-.изменения.->D;
D-->|git add|B;
```


