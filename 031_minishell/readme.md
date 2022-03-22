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

#### env

#### export

#### unset

#### cd

#### pwd

#### Relative Path

#### Enviroment Path

#### Redirection

#### Go crazy and history

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
