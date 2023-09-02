![Логотип git](LogoGit.png)

# Работа с Git и GitHub (с помощью VSCode)

## 1. Проверка наличия установленного Git

В терминале выполнить команду **git --version**.
Если Git установлен появится сообщение с информацией о версии программы. Иначе будет сообщение об ошибке.

## 2. Установка Git

Загружаем последнюю версию Git с [сайта](https://git-scm.com/downloads)

Устанавливаем с настройками по умолчанию.

## 3. Настройка Git

При первом использовании Git необходимо представиться.

Для этого нужно ввести в терминале 2 команды:

``` 
git config --global user.name «Ваше имя английскими буквами»
git config --global user.email ваша почта@example.com 
```
💡 Записанное имя и почта - ваша подпись к коммитам. Они пригодятся в командной работе, коллеги будут видеть кто внёс изменения и как с ним можно связаться.

## 4. Инициализация репозитория

Обычно вы получаете репозиторий Git одним из двух способов:

1. Вы можете взять локальный каталог, который в настоящее время не находится под версионным контролем, и превратить его в репозиторий Git, либо

2. Вы можете клонировать существующий репозиторий Git из любого места.

В обоих случаях вы получите готовый к работе Git репозиторий на вашем компьютере.

### Создание репозитория в существующем каталоге
Если у вас уже есть проект в каталоге, который не находится под версионным контролем Git, то для начала нужно перейти в него. (Открыть нужную папку в VScode)

для Windows в терминале нахождение в папке будет выглядеть так:
``````
$ cd C:/Users/user/my_project
``````
затем для создания/инициализации репозитория следует выполнить команду:
``````
git innit
``````

Эта команда создаёт в текущем каталоге (папке) новый, скрытый подкаталог (папку) с именем **.git**, содержащий все необходимые файлы репозитория — структуру Git репозитория. Теперь Git отслеживает все файлы в папке, но ваш проект ещё не находится под версионным контролем.

Проверить статус Git можно с помощью команды:
``````
git status
``````
Терминал покажет текущее состояние гита, есть ли изменения, которые нужно закоммитить (сохранить). Например так:
``````
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean
``````
Это означает, что в вашей папке нет отслеживаемых файлов и Git не обнаружил неотслеживаемые файлы в папке.
***
💡 ***Совет*** 💡

*Ранее введённые команды можно вызывать с помощью стрелок клавиатуры. Ранее введённые команды перебираются нажатием стрелки "вверх"*
***
## 5. Запись изменений в репозиторий

### Добавление файла в репозиторий

Предположим, что вы добавили в свой проект новый файл, простой файл **README**. Если этого файла раньше не было, и вы выполните **git status**, вы увидите свой неотслеживаемый файл вот так:

``````
$ echo 'My Project' > README
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README

nothing added to commit but untracked files present (use "git add" to track)
``````
Статус Untracked означает, что Git видит файл, которого не было в предыдущем снимке состояния (коммите); Git не станет добавлять его в ваши коммиты, пока вы его явно об этом не попросите. 

### Отслеживание нового файла

Для того чтобы начать отслеживать (добавить под версионный контроль) новый файл, используется команда **git add**. Чтобы начать отслеживание файла **README**, вы можете выполнить следующее:
``````
$ git add README
``````
💡 *Писать название файла целиком не обязательно: терминал дозаполнит данные автоматически.*

Если вы снова выполните команду status, то увидите, что файл README теперь отслеживаемый и добавлен в индекс:
``````
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)

    new file:   README
``````
Если вы выполните коммит в этот момент, то версия файла, существовавшая на момент выполнения вами команды git add, будет добавлена в историю снимков состояния.

💡 *Команда git add принимает параметром путь к файлу или каталогу, если это каталог, команда рекурсивно добавляет все файлы из указанного каталога в индекс.*

❗❗❗ *Git отслеживает файлы по имени! 
Если изменить имя файла, необходимо добавить файл с новый именем + git commit*

### Коммит изменений

 Простейший способ зафиксировать изменения:
``````
git commit
``````
При чем при вводе команды к коммиту можно добавить комментарий:
``````
git commit -m "Текст комментария"
``````
Пример результата:
```
$ git commit -m "Story 182: fix benchmarks for speed"
[master 463dc4f] Story 182: fix benchmarks for speed
 2 files changed, 2 insertions(+)
 create mode 100644 README
```

✨ Итак, вы создали свой первый коммит! ✨

Вы можете видеть, что коммит вывел вам немного информации о себе: на какую ветку вы выполнили коммит (master), какая контрольная сумма SHA-1 у этого коммита (463dc4f), сколько файлов было изменено, а также статистику по добавленным/удалённым строкам в этом коммите.

💡 *Запомните, что коммит сохраняет снимок состояния вашего индекса. Всё, что вы не проиндексировали, так и висит в рабочем каталоге как изменённое; вы можете сделать ещё один коммит, чтобы добавить эти изменения в репозиторий. Каждый раз, когда вы делаете коммит, вы сохраняете снимок состояния вашего проекта, который позже вы можете восстановить или с которым можно сравнить текущее состояние.*

## 6. Просмотр истории коммитов

После того, как вы создали несколько коммитов или же клонировали репозиторий с уже существующей историей коммитов, вероятно вам понадобится возможность посмотреть что было сделано — историю коммитов. Одним из основных и наиболее мощных инструментов для этого является команда:
```
git log
```
По умолчанию (без аргументов) git log перечисляет коммиты, сделанные в репозитории в обратном к хронологическому порядке — последние коммиты находятся вверху. 

💡 *Нажатие клавиши ‘q’ возвращает 
в исходное окно терминала из комнд git log, git diff и других*

Наиболее распространённые опции для команды git log отражены далее:

| Опция | Описание |
|:------|:---------|
|-p     | Показывает патч для каждого коммита. |
|--stat     | Показывает статистику изменённых файлов для каждого коммита. |
|--shortstat    | Отображает только строку с количеством изменений/вставок/удалений для команды --stat. |
|--name-only    | Показывает список изменённых файлов после информации о коммите. |
|--name-status     | Показывает список файлов, которые добавлены/изменены/удалены. |
|--abbrev-commit     | Показывает только несколько символов SHA-1 чек-суммы вместо всех 40. |
|--relative-date     | Отображает дату в относительном формате (например, «2 weeks ago») вместо стандартного формата даты. |
|--graph    | Отображает ASCII граф с ветвлениями и историей слияний. |
|--pretty    | Показывает коммиты в альтернативном формате. Возможные варианты опций: oneline, short, full, fuller и format (с помощью последней можно указать свой формат).|
|--oneline    | Сокращение для одновременного использования опций --pretty=oneline --abbrev-commit. |
|||

## 7. Перемещение между сохранениями

💡 *Перед переключением версии файла в Git 
используйте команду git log, чтобы увидеть 
количество сохранений*

Для переключения между версиями используйте команду:
```
git checkout
```
**Эта команда также позволяет переключаться между ветками.**

Для работы нужно указать не только 
интересующий вас коммит, но и вернуться в тот, где работаем, при помощи команды git checkout master.

Для отслеживания разницы между текущим файлом и сохранённым можно использовать команду:
```
git diff
```
## 8. Игнорирование файлов

Для того чтобы исключить из отслеживания репозитории определенные файлы или папки необходимо создать там файл ***.gitignore*** и записать в него их название или шаблоны, соответствующие файлам или папкам.

## 9. Создание веток

Создать ветку можно командой

 ```
 git branch
 ```

Список веток в репозитории можно посмотреть с помощью команды

```
git branch
```

Текущая ветка будет отмечена звёздочкой и цветом: **\*master**
 
 ## 10. Слияние веток и разрешение конфликтов

 Для слияния выбранной ветки с текущей нужно выполнить команду:
 ```
 git merge <название ветки>
 ```

Если была изменена одна и та же часть файла в обеих ветках, то может возникнуть конфликт, который потребует участия пользователя.

VSCode предлагает варианты разрешения.

После решения конфликта изменения необходимо закоммитить. Ветка, данные из которой слиты и дальнейшая работа в ней не планируется, должна быть удалена.

## 11. Удаление веток

Ветку можно, находясь в другой ветке, удалить с помощью команды:

```
git branch -d <название ветки>
```

При попытки удалить ветку, в которой вы находитесь Git выдаст ошибку:

```
error: Cannot delete branch
```

При попытке удаления ветки с не слитыми изменениями Git выдаст ошибку:

```
error: The branch 'resolvingIssues' is not fully merged.
If you are sure you want to delete it, run 'git branch -D resolvingIssues'
```
❗❗❗ Обратите внимание, что все команды начинающиеся с большой буквы - принудительные. При использовании команды: 

```
git branch -D <название ветки>
```
Выбранная ветка удалится, а данные из неё не попадут в другие ветки.

## 12. Работа с удалёнными репозиториями

💡*Слово "Удалённый" означает, что репозиторий находится на расстоянии (от слова "даль"), а не "удалённый" от слова "удалить".*

# Спасибо за внимание!

![Спасибо за внимание!](smile.jpg)
