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
bash> echo AA
AA
bash> echo -n AB
ABbash>
bash> echo -nnnnnnnnnnnn a1
a1bash> echo -n -n -n -n  a2
a2bash> echo -n -n a2 -n -n
a2 -n -nbash>
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
bash> export CHEK=/usr/bin
bash> cd $CHEK
bash> pwd
/usr/bin
```
#### pwd

#### Relative Path

#### Enviroment Path

#### Redirection

#### Go crazy and history

- heredoc, redirects, interactive mode
```
bash> cat -e << "" >> a
> first
> second
> // Ctrl + D 
> bash> cat a
first$
second$
```

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
bash> echo 1 && echo 2 || echo 3 && echo 4
1
2
4
bash> echo 1 && echo 2 || (echo 3 && echo 4)
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
