		Mandatory:
	Makefile:
Не забываем проверить -lpthread
	Input:
1. Без аргументов
2. С неправильным кол-во аргументов !=4 && != 5
3. C неправильным аргументом ( <0, =0, буквы, >MAX_INT)
4. С кол-вом number_must_eat = 0

	Workability:
Init
Проверяем все выделение памяти, все malloc должны быть защищены, иначе выйти

Если не создался mutex
if pthread_mutex_init(&mutex, 0)
выйти


Проверить кол-во приемов пищи
./philo 101 1000 200 200 4 | grep eating | wc -l


	Leaks:
General
1. Закрытие всех threads 
phread_join(thread, NULL);
2. Уничтожение всех используемых mutex
pthread_mutex_destroy(mutex);

-fsanitize=thread
1. Один философ -> умирает
2. Несколько философов, все поели
3. Несколько филисофов, кто-то умирает

Не должно быть data races.

valgring
1. Не должно быть dead lock'ов

P.S. Valgrind и fsanitize негативно влияют на работоспособность, время собятия может кардинально различаться.

		Bonus:
	Input:
Same as Mandatory

	Workability:

При завершении работы одного процесса(кто-то умер / все поели) нужно убить других философов(процессы)
kill(philos[i], SIGTERM);

	Leaks:
General
1. Закрыть все используемые семафоры
sem_close(sem);
2. Удалить именнованный семафор
sem_unlink("sem");

-fsanitize=thread
Может некорректно работать с семафорами, если показывает data race, не значит, что все плохо. Придется проверять самим, каждое использование переменной. Если защищенно, то ОК.
