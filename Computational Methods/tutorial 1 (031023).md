
## algorithm 0
first run:

| conversion | temperature | multiplier | converted_temperature | output |
| ---------- | ----------- | ---------- | --------------------- | ------ |
| fahrenheit to celcius | 32 | | | |
| | 0 | 0.555556 | 0 | 0 |


second run:

| conversion | temperature | multiplier | converted_temperature | output |
| ---------- | ----------- | ---------- | --------------------- | ------ |
| celcius to fahrenheit | 10 | 1.8 | | |
| | 18 | | 50 | 50 |

## algorithm 1

| width | height | result1 | edges | lengths | result2 | output |
| ----- | ------ | ------ | ----- | ------- | ------ | ------ |
| 10 | 5 | 50 | | | | 50 |
| | | | 20 | 10 | 30 | 30 |

| width | height | result1 | edges | lengths | result2 | output |
| ----- | ------ | ------ | ----- | ------- | ------ | ------ |
| 12.5 | 17 | 212.5 | | | | 212.5 |
| | | | 25 | 34 | 59 | 59 |

## algorithm 2

| year_born | current_year | year_difference | result | output |
| --------- | ------------ | --------------- | ------ | ------ |
| 2003 | 2023 | 20 | 240 | |
| | | | 7200 | |
| | | | 172800 | 172800 |


| year_born | current_year | year_difference | result | output |
| --------- | ------------ | --------------- | ------ | ------ |
| 1998 | 2023 | 25 | 300 | |
| | | | 9000 | |
| | | | 216000 | 216000 |


## algorithm 3

| random_number | number | output |
| ------------- | ------ | ------ |
| 483 | 10 | too low, guess again! |


| random_number | number | output |
| ------------- | ------ | ------ |
| 16 | 54 | too high, guess again! |


| random_number | number | output |
| ------------- | ------ | ------ |
| 32 | 32 | correct! |

## algorithm 4

| number | counter | result | output |
| ------ | ------- | ------ | ------ |
| 8 | 1 | 8 | 8 |
| | 2 | 16 | 16 |
| | 3 | 24 | 24 |
| | 4 | 32 | 32 |
| | 5 | 40 | 40 |
| | 6 | 48 | 48 |
| | 7 | 56 | 56 |
| | 8 | 64 | 64 |
| | 9 | 72 | 72 |
| | 10 | | |


| number | counter | result | output |
| ------ | ------- | ------ | ------ |
| 2 | 1 | 2 | 2 |
| | 2 | 4 | 4 |
| | 3 | 6 | 6 |
| | 4 | 8 | 8 |
| | 5 | 10 | 10 |
| | 6 | 12 | 12 |
| | 7 | 14 | 14 |
| | 8 | 16 | 16 |
| | 9 | 18 | 18 |
| | 10 | | |

## algorithm 5

| a | b | c | counter | output |
| - | - | - | ------- | ------ |
| 0 | 1 | | 1 | 0 |
| | | 1 | | |
| 1 | 1 | | | 1 |
| | | | 2 | |
| | | 2 | | |
| 1 | 2 | | | 1 |
| | | | 3 | |
| | | 3 | | |
| 2 | 3 | | | 2 |
| | | | 4 | |
| | | 5 | | |
| 3 | 5 | | | 3 |
| | | | 5 | |
| | | 8 | | |
| 5 | 8 | | | 5 |
| | | | 6 | |
| | | 13 | |
| 8 | 13 | | | 8
| | | | 7 | | 
| | | 21 | | |
| 13 | 21 | | | 13 |
| | | | 8 | |
| | | 34 | |
| 21 | 34 | | | 21 |
| | | | 9 | |
| | | 55 | |
| 34 | 55 | | | 34 |
| | | | 10 | |

## algorithm creating
### algo 1

```
Let a = input from user
Let b = input from user
Let sum = a+b
Output sum
Let difference = b-a
Output difference
If b = 0:
	Output "division by zero error"
Else:
	Let ratio = a/b
	Output ratio
End If
Let product = a*b
Output product
```

### algo 2
```
Let diameter = input from user
Get pi
Let radius = diameter/2
Let area = 4*pi*radius*radius
Let volume = (area*radius)/3
Output area
Output volume
```

### algo 3
```
Let weight_grams = input from user
If weight_grams <= 53:
	Output "small"
Elif weight_grams <= 63:
	Output "medium"
Elif weight_grams <= 73:
	Output "large"
Else:
	Output "very large"
End If
```

### algo 4
```
Let counter = 1
While counter <= 15:
	If counter divisible by 3 and counter divisible by 5:
		Output "FizzBuzz"
	Elif counter divisible by 3:
		Output "Fizz"
	Elif counter divisible by 5:
		Output "Buzz"
	Else:
		Output counter
	End If
	Increment counter
End While
```

### algo 5
```
Let largest = 0
Let counter = 0
While counter < 10:
	Let input = input from user
	If counter = 0 or input > largest:
		largest = input
	End If
	Increment counter
End While
Output largest
```
