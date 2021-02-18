# *Задание 1*
  Доброго времени суток, дорогой проверяющий. Сразу начну с извинения за то, что будет описано ниже. Дело в том, что условие первого задания было изначально истолковано мной неверно из-за чего предложенная задача, на мой взгляд, многократно усложнилась. Однако, колоссальное время, потраченное на решение именно этой версии задачи, не прошло даром - мне-таки удалось найти алгоритм, который чертовски похож на правильный. Не могу отказать себе в удовольствии предствить его на ваш суд. Что касается оригинальной задачи, то её решение будет приведено в конце, как следствие из более сложной.
  Всё, что будет представлено ниже, ни в коем случае не является формальным доказательством правильности работы алгоритма, а является лишь доводами и рассуждениями в пользу его правильности.
# Постановка задачи
  Чём же отличается задача из моей фантазии от оригинальной? Стаканом! В задаче, которую мы будем решать ниже, стакан может быть произвольным. Да, там всё ещё в отсортированном виде лежат заявки на покупку и продажу, но он может быть произвольного размера. Так же, в случае если стакан исчерпается, никаких дополнительных заявок не предоставляется. Чтобы сэмулировать бесконечный стакан, можно добавить позицию объёма +INF. Это алгоритму не вредит.
# Основная (на мой взгляд) проблема
  Не секрет, что один из алгоритмов для решения задачи в её изначальном виде завязан на обработке локальных минимумов и максимумов. Рассмотрим пример. Пусть в момент 0 доступен только один аск 9$ объёмом 1, в момент 1 есть только один бид 10$ объёмом 1, в момент 2 только есть один аск 9$ объёмом X и в момент 3 есть только один бид 20$ объёмом 2. Изначальное количество денег - 18. Заметим, что в момент 1 и 3 выгодно покупать. А вот стоит ли продовать в момент 2 зависит от X. При X = 2 - стоит, а при X = 1 - нет. При достаточно долгой цепочке колебаний, перебор вариантов экспоненциально вырастет и исполнение программы займёт очень долго.
# Алгоритм 
  Пусть изначально у нас А$. В каждый момент времени храним отсортированный список доступных к этому моменту асков. Сверху список обрезается по границе заявок, которые можно исполнить на A$. Изначально список пуст. Идём по таймстемпам слева-напрано. Если самый дешёвый аск из нашего списка стоит дешевле, чем самый дорогой бид в этот момент времени, то совершаем сделку, но с небольшой хитростью. Вся прибыль от сделки добавляеься в переменную А. Использованые аски исключаются из нашего списка. **В наш список добавляются исполненные бид заявки**. В наш список добавляются аски из текущего таймстепа. Наш список асков, сортируется и обрезается. Переходим к следующему таймстемпу. Ответ - число, которое в конце будет в A$ (Это верно, если считать, что в конце алгоритма у него должны быть только доллары. Если измерение проходит по pnl, то нужно купить обём из нашего списка, цена которого ниже средней).
# Пояснение
  Добавление бид заявок к нам в список асков, обёясняется необходимостью иногда отменять сделки. Ведь продать по какой-то цене, а потом купить по ней и есть отмена сделки. Также прошу заметить, что биды, попадая в список асков, не имеют каких-либо отличий от асков и обрабатываются как аски автоматически.
# Рассуждения
  Что может пойти не так? Так как стек всегда обрезан, больше текущих денег мы не купим. Может показаться, что мы могли бы заработать на сделке, потратить куда-то вырученные деньги, а потом отменить первую сделку. Вроде, если подумать и порисовать видно, что так, вроде, тоже не бывает. Забавный факт, что алгоритм не может отменить сделку, которая вылетела из списка асков. Получается, что если алгритм верен, то эта сделка в момент выхода из стека точно утверждается. Доказывать этот факт я не умею.
# Task1
  Чтобы решить task1, нужно в представленном алгоритме всем нулевым бидам и аскам выставить количество +INF
  
  
# *Задание 2*
  В качестве лучшего решения задачи 2, я представляю улучшенный алгритм из примера. Отличия следующие:
* Храним все обещанные future_mid_price. При решении используем не только значение через 2 секунды, но и через 1 секунду (+-eps)
* При решении вместо mid_price используем update.order_book.bid_price[0] и update.order_book.ask_price[0] соответственно
* При большом спреде не торгуем
