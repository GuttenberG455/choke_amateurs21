# minishell
[Задание](https://cdn.intra.42.fr/pdf/pdf/43461/en.subject.pdf)

[Стандартный чеклист](https://github.com/mharriso/school21-checklists/blob/master/ng_3_minishell.pdf)

## Mandatory:
### Makefile:
1. Проверить make, make clean, make fclean, make re.
2. Проверить relink после изменения .c, .h, Makefile
3. Проверить наличие флагов -Wall -Wextra -Werror

Не забываем проверить наличие библиотеки readline. Например, -lreadline

### Input:

Запускаем программу через ./minishell. Должен отображаться *promt* и ожидать ввод команд.

### Workability:
#### Simple command & global

#### Arguments & history


#### echo
- execute the echo command `echo` with or without arguments or *-n*
Параметр *-n* должен не выводить символ новой строки
```
bash-3.2$ echo AA
AA
bash-3.2$ echo -n AB
ABbash-3.2$
bash-3.2$ echo -nnnnnnnnnnnn a1
a1bash-3.2$ echo -n -n -n -n  a2
a2bash-3.2$ echo -n -n a2 -n -n
a2 -n -nbash-3.2$
```

#### exit

#### Return value of a process

#### Signals

#### Double quotes

#### Simple quotes

#### env, export, unset
- check if the `env` shows you the current environment variables
- `export` environment variables, create new ones or replace old ones
- `unset` environment variables, remove them

`env` должен показать переменные среды, `export` экспортирует переменные, `unset` удаляет.

Экспортируем след. переменные, смотрим на вывод ошибки о неправильном идентификаторе. 
```
export X1 X2=22 _X3 _X4=44 5 X6=66 7=77 X7 X8=88 X##=99 =

bash: export: `5': not a valid identifier
bash: export: `7=77': not a valid identifier
bash: export: `X##=99': not a valid identifier
bash: export: `=': not a valid identifier
```
Проверяем *$?* должен быть *1*. После этого запускаем `export`. Должны появится новые переменные. Внимание на: сортировку по алфавиту, значения должны быть в *"*, пустые должны быть показаны. </br>
В `env` должны отображаться только переменные со значением. Порядок ???
```
export
...
declare -x X1
declare -x X2="22"
declare -x X6="66"
declare -x X7
declare -x X8="88"
declare -x _X3
declare -x _X4="44"

env
...
X8=88
X2=22
_X4=44
X6=66
```
Теперь удалим переменные командой `unset`

```
unset X1 X2 3=33 _X4 X7 X&& =
bash: unset: `3=33': not a valid identifier
```
Проверяем *$?* должен быть *1*. После этого запускаем `export`. Переменные должны быть удалены. Сообщение об ошибке должно быть одно, но удалиться должны все корректно написанные. 



#### cd


Команда | Что должно быть
--- | ---
cd  | перемещение в директорию *home*
cd ~ | перемещение в директорию *home* (воможно не по заданию)
cd .. | перемещение на директорию выше (назад)
cd . | остаемся в текущей директории
cd /usr/bin </br> cd <global_directory> | перемещение в директорию по глобальному пути
cd \<local_directory> | перемещение в директорию по относительному пути

Не забываем проверять при помощи переменных среды `$PWD`, `$OLDPWD` и `$?` (exit status):

`$PWD` - должно быть текущим путем, `$OLDPWD` - прошлым </br>
`$?` - 0 в случае успеха и 1 в случае ошибки (нет директории, нет доступа)

Можно проверить с переменной среды:
```
bash-3.2$ export CHEK=/usr/bin
bash-3.2$ cd $CHEK
bash-3.2$ pwd
/usr/bin
```
#### pwd

#### Relative Path

#### Enviroment Path

#### Redirection

#### Go crazy and history

- special redirects for file descriptors
```
bash-3.2$ cat <file_to_cat> <non-existent_file> 1>stdout.txt 2>stderr.txt
bash-3.2$ cat stdout.txt
file_content%                                                                                      
bash-3.2$ cat stderr.txt
cat: <non-existent_file>: No such file or directory
bash-3.2$ cat <file_to_cat> <non-existent_file> 8>3 2>4
file_content%
bash-3.2$ cat <file_to_cat> <non-existent_file> 1>3 9>4
cat: <non-existent_file>: No such file or directory
```
- heredoc, redirects, interactive mode
```
bash-3.2$ cat -e << "" >> a
> first
> second
> // Ctrl + D 
> bash-3.2$ cat a
first$
second$
```
- heredoc
```
bash-3.2$ cat <<$USER
> qq
> <user_name>
> $USER
qq
<user_name>
```
heredoc закроется только после написания слова после << несмотря на $


#### Enviroment Variables

#### Miscellaneous

### Leaks:
#### General
1. Очистка выделенной памяти (не забываем проверить все комманды)
2. Маллоки должны быть защищены. В случае невыделения памяти, нужно завершить программу.


#### valgrind

Библиотека readline может вызвать утечки. Это некритично.
___
## Bonus:
### Input:
Same as Mandatory

### Workability

#### And, Or
- Use &&, || and parenthesis() with commands and check if it works as bash.
```
bash-3.2$ echo 1 && echo 2 || echo 3 && echo 4
1
2
4
bash-3.2$ echo 1 && echo 2 || (echo 3 && echo 4)
1
2
```

#### WildCard
- Use wildcards in arguments for the local directory

Команда | Что должно быть
--- | ---
echo * | Печатает содержимое директории
cat * | Печатает содержимое всех файлов в директории
export * | Добавляет название файлов в *env*
unset * | Удаляет параметры с названием файлов в *env*
cd * | Если одна папка в директории, то перемещаемся туда
