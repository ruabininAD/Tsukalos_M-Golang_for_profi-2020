# Числовые типы данных
  ## Целые числа
  Бывают со знаком и без знака

   Со знаком называются int8, int16, int32, int64

   Без знака — uint8, uint16, uint32 и uint64.

  Типы int и uint являются наиболее эффективным представлением целых чисел со знаком и без знака соответственно для текущей платформы.

  ## Числа с плавающей точкой
  float32 и float64
  float32  обеспечивает точность примерно до шестого знака после запятой
  float64 - до 15-го знака.
    
    При преобразовании числа с плавающей запятой в целое число дробь отбрасывается путем усечения числа с плавающей запятой до нуля знаков после запятой. Это означает, что в процессе такой операции некоторые данные могут быть потеряны.

  ## Комплексные числа
  complex64 и complex128
  В первом из них используется два типа float32: один для вещественной части комплексного числа, а второй — для мнимой, тогда как в complex128 используется два типа float64

  Комплексные числа выражаются в форме a + bi, где a и b — действительные числа, а i — решение уравнения x^2 = –1
# Циклы в Go
 Цикл for позволяет осуществлять иттерации по различным типам данных.

`for i := 0; i < 100; i++ {}`

Вообще, цикл for состоит из трех частей: первая называется инициализацией, вторая — условием, а последняя — изменением счетчика. Ни одна из этих частей не является обязательной.

Ключевое слово `break` также позволяет создать цикл for без условия выхода.

Можно пропустить одну итерацию цикла for, используя ключевое слово continue.

Замена while

`for {}`

 следующий код Go эквивалентен циклу do ... while (anExpression):

`for ok := true; ok; ok = anExpression {}`

Как только переменная ok примет значение false, цикл for прекратит работу.

## Ключевое слово range
 range - перебирает любой тип данных.
# Массивы в Go
`anArray := [4]int{1, 2, 4, -4}`

`twoD := [4][4]int{{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}, {13, 14, 15, 16}}`

массивы Go не являются динамическими

# Срезы Go, и почему они намного лучше, чем массивы
    Срезы в Go реализованы на основе массивов, следовательно, внутри каждого среза Go лежит массив.
 Срезы передаются в функции по ссылке — это означает, что фактически в функцию передается адрес памяти переменной среза, и любые изменения, внесенные в срез внутри функции, не будут потеряны после выхода из нее

 ## Выполнение основных операций со срезами
 Для того чтобы создать литерал среза, нужно сделать следующее:

`aSliceLiteral := []int{1, 2, 3, 4, 5}`  

Однако, кроме этого, еще есть функция make(), которая позволяет создавать пустые срезы желаемой длины и емкости

`integer := make([]int, 20)`  
 Go автоматически инициализирует все элементы нового среза нулевыми значениями заданного типа.

 добавить элемент к срезу  
 `integer = append(integer, 12345)`

 с помощью нотации [:] можно получить доступ к нескольким последовательным элементам среза. Кроме того, нотация [:] позволяет создать новый срез из уже существующего среза или массива:  
`integer[1:3]`

Для некоторого массива a1 можно создать срез s1, который бы ссылался
на этот массив, с помощью оператора s1 := a1[:].

Это означает, что при изменении элементов вторичного среза изменяются и элементы исходного среза, поскольку оба они указывают на один и тот же базовый массив. Проще говоря, при создании вторичного среза не создается копия исходного среза.

## Автоматическое расширение срезов
 Срезы характеризуются двумя основными свойствами: емкостью (capacity) и длиной (length).
 

## Байтовые срезы
Байтовый срез — это срез, типом которого является byte. Чтобы создать байтовый срез с именем s, нужно выполнить следующий код:  
`s := make([]byte, 5)`

В большинстве случаев байтовые срезы используются для хранения строк, и поэтому позволяет легко переключаться между этим типом и типом string.

## copy()
     При использовании функции copy() для срезов следует быть очень осторожным, поскольку количество элементов, копируемых встроенной функцией copy(dst, src), составляет минимум из len(dst) и len(src).

С помощью функции copy() можно создать срез из элементов существующего массива или как копию существующего среза.

## Многомерные срезы
`s1 := make([][]int, 4)`

## Сортировка срезов с помощью sort.Slice()

```go
sort.Slice(mySlice, func(i, j int) bool {
 return mySlice[i].height < mySlice[j].height
 })
```
    Обратите внимание, что sort.Slice() изменяет последовательность элементов в срезе в соответствии с функцией сортировки.

## Добавление массива к срезу

```go 
s := []int{1, 2, 3}
a := [3]int{4, 5, 6}
ref := a[:]
n := append(s, ref...) // "New slice:[1 2 3 4 5 6]
```
многоточие (...) разбивает массив на элементы, которые добавляются к существующему срезу.

# Хеш-таблицы Go
Хеш-таблицы, или карты (map) Go — то же, что известные хеш-таблицы, существующие во многих других языках программирования.
Основным их преимуществом является способность использовать любой тип данных в качестве индекса, который в этом случае называется ключом карты или просто ключом.

**ключи хеш-таблицы должны поддерживать оператор ==**

Следующий код с использованием функции make() позволяет создать пустую 
хеш-таблицу с ключами типа string и значениями типа int:
`iMap = make(map[string]int)`

Чтобы получить доступ к объектам anotherMap, к ним нужно обратиться как 
к `anotherMap["k1"]` и `anotherMap["k2"]`.

 Чтобы удалить объект хеш-таблицы, следует воспользоваться функцией delete():  
`delete(anotherMap, "k1")`

Перебор:   
```go
for key, value := range iMap {
 fmt.Println(key, value)
}
```

# Константы в Go
 константы — переменные, значения которых нельзя изменять.
`const HEIGHT = 200`

Значение констант определяется не во время выполнения программы, а на этапе 
компиляции.

Обратите внимание, что результаты всех операций между константами компилятор Go также считает константами.


# Указатели в Go
указатели — адреса памяти, что обеспечивает повышение скорости в обмен на сложный для отладки код и неприятные ошибки.

Чтобы функция принимала указатель в качестве параметра, нужно написать 
следующий код:  
`func getPointer(n *int) {}`  
Аналогичным образом функция может возвращать указатель:  
`func returnPointer(n int) *int {}`  
# Работа с временем
Константы Go для работы с датами — это Jan для анализа трехбуквенной аббревиатуры, используемой для описания месяца, 2006 для анализа года и 02 — для 
анализа дня месяца. Если вместо Jan использовать January, то, как и следовало ожидать, вместо трехбуквенного сокращения получим полное название месяца.

## Измерение времени выполнения программы

```go
package main
import (
 "fmt"
 "time"
)
func main() {
 start := time.Now()
 time.Sleep(time.Second)
 duration := time.Since(start)
 fmt.Println("It took time.Sleep(1)", duration, "to finish.")
 start = time.Now()
 time.Sleep(2 * time.Second)
 duration = time.Since(start)
 fmt.Println("It took time.Sleep(2)", duration, "to finish.")
 start = time.Now()
 for i := 0; i < 200000000; i++ {
 _ = i
 }
 duration = time.Since(start)
 fmt.Println("It took the for loop", duration, "to finish.")
 sum := 0
 start = time.Now()
 for i := 0; i < 200000000; i++ {
 sum += i
 }
 duration = time.Since(start)
 fmt.Println("It took the for loop", duration, "to finish.")
}
```
 Вся работа выполняется функцией time.Since(). Эта функция принимает один аргумент, который должен означать момент времени в прошлом. В данном случае будет измерено время, необходимое Go для выполнения time.Sleep(time.Second), поскольку это единственный оператор, стоящий между time.Now() и time.Since().
# Измерение времени выполнения команд и функций
# Работа с датами
