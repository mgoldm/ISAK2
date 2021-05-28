# ISAK2
Смирнов Николай Сергеевич М3О-312Б-18. Лабораторная работа №2. 
"Управление процесcами"


Постановка задачи:
1. Выведите на экран листинг характеристик (в длинном и коротком форматах) процессов, инициализированных с Вашего терминала. Проанализируйте и объясните содержание каждого поля сообщения.
2. Выведите на экран листинг характеристик всех процессов. Используйте при необходимости конвейер с more для постраничного просмотра листинга. Какой процесс является родительским для большинства процессов? Что означает символ ? в поле управляющий терминал процесса?
3. Выведите на экран листинг процессов, запущенных конкретным пользователем. Какой ключ пришлось использовать? Что говорит значение ? в поле управляющий терминал процесса?
4. Разработайте и запустите простейшую процедуру в фоновом режиме с бесконечным циклом выполнения, предусматривающую, например, перенаправление вывода каких-то сообщений в файл или в фиктивный файл, и использующую команду 
для сокращения частоты циклов процедуры.
5. Выполните п. 1. Объясните изменения в листинге характеристик процессов.
6. Понизьте значение приоритета процедуры. На что и как повлияет эта операция при управлении вычислительным процессом системы? Как отразятся ее результаты в описателях процессов?
7. Проанализируйте листинг процессов. Какой процесс является родительским для процедуры.
8. Выйдите из системы и войдите заново. Проанализируйте листинг процессов. Объясните изменения в системе.
9. Запустите процедуру в фоновом режиме, но предусмотрите ее защиту от прерывания при выходе из системы.
10. Выполните п.6. Объясните изменения PPID процедуры.
11. Завершите выполнение процесса процедуры.
12. Запустите процедуру в интерактивном режиме с перенаправлением вывода в соответствующий файл.
13. Переведите задание с процедурой в фоновый режим и проанализируйте сообщение на экране. Что пришлось дополнительно сделать? Как выглядят приостановленные процессы в листинге команды ps?
14. Переведите задание с процедурой в интерактивный режим и проанализируйте сообщение на экране.
15. Завершите выполнение процедуры и проанализируйте сообщение на экране

Практическая часть:
1. Выведем в окно терминала листинг характеристик процессов в коротком формате:
![image](https://user-images.githubusercontent.com/57058926/118308953-4571b880-b4f5-11eb-8555-8c9805201f05.png)


Поле PID означает идентификатор процесса.
Поле TTY означает имя иерминала с которого запущен процесс.
Поле TIME означает процессорное время, затраченное на выполнение данного процесса.
Поле CMD означает команду которая вызвала выполнение процесса

Выведем на окно терминала листинг характеристик процессов в длинном формате:

![image](https://user-images.githubusercontent.com/57058926/118309269-ae593080-b4f5-11eb-80e2-a6963b34fc86.png)


Вывод дополнился новыми полями.
Поле UID означает идентификатор пользователя, который запустил процесс.
Поле PPID означает идентификатор родительского процесса.
Поле STIME означает время старта процесса.
Вывод дополнился новыми полями.
Поле UID означает идентификатор пользователя, который запустил процесс.
Поле PPID означает идентификатор родительского процесса.
Поле STIME означает время старта процесса.

2. Выведем листинг характеристик всех процессов:
![image](https://user-images.githubusercontent.com/57058926/118309302-c03ad380-b4f5-11eb-842e-2f227b52716d.png)

скриншот вставляю частично, слишком большйо список команд

3. Чтобы вывести листинг процессов для определенного пользователя, выйдем из пользователя "root"
![image](https://user-images.githubusercontent.com/57058926/118309495-03954200-b4f6-11eb-9dd8-63cd426adb27.png)
Скриншот также частичный

4. Воспользуемся редактором "vi" и создадим программу с помощью команды "vi s.py":
   Перейдем в режив ввода нажатием клавиши "i" и введем текст программы:
   
		import time
		while True:
			with open('text.txt', 'w') as file:
				file.write("Hello! ")
			time.sleep(1)
		~
		~
		~
		...
		~

    Сохраним и выйдем из редактора двойным нажатием "ZZ".


    Запустим программу из терминала в фоновом режиме:
	[gold@gold-VirtualBox:] python sl.py &
		[1] 9555
5. Выведем листинг характеристик процессов
	[root@gold-VirtualBox ~]# ps -f 
  
		UID	PID	PPID	C	STIME	TTY	TIME		CMD
		root	1199	668	0	10:55	tty1	00:00:00	-bash
		root	1236	1199	0	11:55	tty1	00:00:00	ps -f
		...
		root	3342	9339	0	12:47	tty1	00:00:00	python sl.py
6. Понизим приоритет процесса 9555 до значения 5 и выведем характеристику процессов с ключом "l":
        
	[root@gold0VirtualBox ~]# renice 5 3342
  
		9555 (process ID) old priority 0, new priority 5

	[root@gold0VirtualBox ~]# ps -fl
  
		...
		0	S	root	3342	3327	0	85	5	-	31383	12:47	poll_s	tty1	00:00:00	python slp.py
		...
7. Родительским процессом для процесса 3342 является процесс с идентификатором 3327 - bash.

8. Выйдем из системы командой "exit" и зайдем заново. Выведем листинг характеристик процессов
![image](https://user-images.githubusercontent.com/57058926/118311259-540d9f00-b4f8-11eb-8970-912776e9c746.png)

9.Запустим процедуру в фоновом режиме и предусмотрим ее защиту от прерывания.
	  [gold@gold0VirtualBox ~]# nohup python sl.py &
    
		  [1]	3346
	  [gold@gold0VirtualBox ~ ]# nohup: ignoring input and appending output to 'nohup.out'
 
 10. Выведим листинг характеристик процессов
 
   [root@gold0VirtualBox ~]# ps -fl
   
   
    F	S	UID	PID	PPID	C	PRI	NI	ADDR	SZ	STIME	WCHAN	TTY	TIME 		CMD
    4	S	root	3352	3241	0	80	0	-	28886	13:06	do_wai	tty1	00:00:00	-bash
	  4	S	root	3367	3346  0	80	0	-	31383	13:08	poll_s	tty1	00:00:00	python slp.py
	  0	R	root	3389	3373	0	80	0	-	38863	13:10	-	tty1	tty1	00:00:00	ps -fl
  
  11. Завершим выполнение процесса процедуры сигналом "-9":

[gold0VirtualBox ~]# kill -9 3367

[gold0VirtualBox  ~]# ps -fl

		F	S	UID	PID	PPID	C	PRI	NI	ADDR	SZ	STIME	WCHAN	TTY	TIME 		CMD
		4	S	root	3352	3241	0	80	0	-	28886	13:06	do_wai	tty1	00:00:00	-bash
		0	R	root	3389	3373	0	80	0	-	38863	13:10	-	tty1	00:00:00	ps -fl
		[1]+ Killed		nohup python sl.py
    
12. Запустим процедуру в фоновом режиме а затем переведем ее в интерактивный режим.

    [gold0VirtualBox  ~]# python sl.py &
    
		[1] 3392
    
	[gold0VirtualBox ~]#	fg
  
		python slp.py
13. Приостановим выполнение процесса сочетанием клавиш Ctrl + z.
	[gold0VirtualBox ~]# python slp.py
  
	[1]+ Stopped
  

	[gold0VirtualBox ~]# ps -fl
  
  F	S	UID	PID	PPID	C	PRI	NI	ADDR	SZ	STIME	WCHAN	TTY	TIME 		CMD 
  4	S	root	3352	3241	0	80	0	-	28886	13:06	do_wai	tty1	00:00:00	-bash
	0	T	root	3392	3521	0	80	0	-	31383	13:08	do_sig	tty1	00:00:00	python slp.py
	0	R	root	3421	3513	0	80	0	-	38863	13:10	-	tty1	00:00:00	ps -fl

14. Переведем процедуру в интерактивный режим
	[gold0VirtualBox ~]#	fg 
  
		python slp.py
    
15. Завершим выполнение процесса с помощью команды kill.
	[gold0VirtualBox ~]# kill -9 3392
  

Вывод:
В ходе лабораторной работы были изучены команды для работы с процессами в операционной системе Linux.
