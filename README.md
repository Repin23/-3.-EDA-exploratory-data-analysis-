1. Даны значения зарплат из выборки выпускников: 100, 80, 75, 77, 89, 33, 45, 25, 65, 17, 30, 24, 57, 55, 70, 75, 65, 84, 90, 150. Посчитать (желательно без использования статистических методов наподобие std, var, mean) среднее арифметическое, среднее квадратичное отклонение, смещенную и несмещенную оценки дисперсий для данной выборки.
2. В первом ящике находится 8 мячей, из которых 5 - белые. Во втором ящике - 12 мячей, из которых 5 белых. Из первого ящика вытаскивают случайным образом два мяча, из второго - 4. Какова вероятность того, что 3 мяча белые?
3. На соревновании по биатлону один из трех спортсменов стреляет и попадает в мишень. Вероятность попадания для первого спортсмена равна 0.9, для второго — 0.8, для третьего — 0.6. Найти вероятность того, что выстрел произведен: a). первым спортсменом б). вторым спортсменом в). третьим спортсменом.
4. В университет на факультеты A и B поступило равное количество студентов, а на факультет C студентов поступило столько же, сколько на A и B вместе. Вероятность того, что студент факультета A сдаст первую сессию, равна 0.8. Для студента факультета B эта вероятность равна 0.7, а для студента факультета C - 0.9. Студент сдал первую сессию. Какова вероятность, что он учится: a). на факультете A б). на факультете B в). на факультете C?
5. Устройство состоит из трех деталей. Для первой детали вероятность выйти из строя в первый месяц равна 0.1, для второй - 0.2, для третьей - 0.25. Какова вероятность того, что в первый месяц выйдут из строя: а). все детали б). только две детали в). хотя бы одна деталь г). от одной до двух деталей?


1.
import numpy as np
import matplotlib.pyplot as plt
from math import factorial

arr=np.array([100, 80, 75, 77, 89, 33, 45, 25, 65, 17, 30, 24, 57, 55, 70, 75, 65, 84, 90, 150])

def mean_value(array):
return sum(array) / len(array)

print(f'Среднее арифметическое = {round(mean_value(arr),2)}')
a=round(mean_value(arr),2)

Среднее арифметическое = 65.3

np.mean(arr)
65.3

def mean_square_deviation(array):
    square_deviation = (array - mean_value(array)) ** 2
    return (sum(square_deviation) / (len(square_deviation) - 1)) ** (1/2)

    
print(f'Среднее квадратичное отклонение = {round(mean_square_deviation(arr),2)}')
cреднее квадратичное отклонение = 31.62

np.std(arr, ddof=1)

31.624607341019814

def dispersion(array, offset):
    square_deviation = (array - mean_value(array)) **2
    return sum(square_deviation) / (len(square_deviation) - 1) if offset else sum(square_deviation) / len(square_deviation)

    print(f'Смещенная оценка дисперсии = {round(dispersion(arr, False),2)}\n'
      f'Немещенная оценка дисперсии = {round(dispersion(arr, True),2)}')

Смещенная оценка дисперсии = 950.11
Немещенная оценка дисперсии = 1000.12

np.var(arr, ddof=0)
950.11
np.var(arr, ddof=1)
1000.1157894736842


2.
import numpy as np
import matplotlib.pyplot as plt
from math import factorial

def combinations(n,k):
    return factorial(n) / (factorial(k) * factorial(n - k))
   
P1 = (combinations(5,0) * combinations(3,2) / combinations(8,2)) * (combinations(5,3) * combinations(7,1) / combinations(12,4))
print(f'Из первого ящика вытащили 0 белых мячей И из второго вытащили 3 белых мяча = {round(P1, 4)}')

P2 = (combinations(5,1) * combinations(3,1) / combinations(8,2)) * (combinations(5,2) * combinations(7,2) / combinations(12,4))
print(f'из первого ящика вытащили 1 белый мяч И из второго вытащили 2 белых мяча = {round(P2, 4)}')

P3=(combinations(5,2) * combinations(3,0) / combinations(8,2)) * (combinations(5,1) * combinations(7,3) / combinations(12,4))
print(f'из первого ящика вытащили 2 белых мяча И из второго вытащили 1 белый мяч = {round(P3, 4)}')

P = P1 + P2 + P3
print(f'Вероятность того, что 3 мяча белые Р = {round(P, 4)} = {round(P * 100, 2)}%')

Вероятность того, что 3 мяча белые Р = 0.3687 = 36.87%


3.

PBA = 1/3
PB = PBA * 0.9 + PBA * 0.8 + PBA * 0.6
print(f'Вероятность того, что цель поражена P(A) = {round(PB, 4)}')
Вероятность того, что цель поражена P(A) = 0.7667

PAB1 = PBA * 0.9 / PB
PAB2 = PBA * 0.8 / PB
PAB3 = PBA * 0.6 / PB
print(f'Вероятность того, что выстрел произвёл первый спортсмен: PAB1 = {round(PAB1, 4)} = {round(PAB1 * 100, 2)}%;\n'
      f'Вероятность того, что выстрел произвёл второй спортсмен: PAB1 = {round(PAB2, 4)} = {round(PAB2 * 100, 2)}%;\n'
      f'Вероятность того, что выстрел произвёл третий спортсмен: PAB1 = {round(PAB3, 4)} = {round(PAB3 * 100, 2)}%.')

Вероятность того, что выстрел произвёл первый спортсмен: PAB1 = 0.3913 = 39.13%;
Вероятность того, что выстрел произвёл второй спортсмен: PAB1 = 0.3478 = 34.78%;
Вероятность того, что выстрел произвёл третий спортсмен: PAB1 = 0.2609 = 26.09%.


4.

PB = 0.25 * 0.8 + 0.25 * 0.7 + 0.5 * 0.9
print(f'Полная вероятность наступления события PA = {round(PB, 4)}.')

PAB1 = 0.25 * 0.8 / PB
PAB2 = 0.25 * 0.7 / PB
PAB3 = 0.5 * 0.9 / PB
print(f'Вероятность того, что студент учится на факультете А: {round(PAB1, 4)} = {round(PAB1 * 100, 2)}%;\n'
      f'Вероятность того, что студент учится на факультете B: {round(PAB1, 4)} = {round(PAB1 * 100, 2)}%;\n'
      f'Вероятность того, что студент учится на факультете C: {round(PAB3, 4)} = {round(PAB3 * 100, 2)}%.')

Вероятность того, что студент учится на факультете А: 0.2424 = 24.24%;
Вероятность того, что студент учится на факультете B: 0.2424 = 24.24%;
Вероятность того, что студент учится на факультете C: 0.5455 = 54.55%.



PA = 0.1 * 0.2 * 0.25
print(f'Вероятность того, что из строя выйдут все детали Р(A) = {round(PA, 4)} = {round(PA * 100, 2)}%')

Вероятность того, что из строя выйдут все детали Р(A) = 0.005 = 0.5%

PB = 0.1 * 0.2 * 0.75 + 0.1 * 0.25 * 0.8 + 0.2 * 0.25 * 0.9
print(f'Вероятность того, что из строя выйдут только 2 детали Р(B) = {round(PB, 4)} = {round(PB * 100, 2)}%')

Вероятность того, что из строя выйдут только 2 детали Р(B) = 0.08 = 8.0%

PC = 0.9 * 0.8 * 0.75
print(f'Вероятность того, что из строя не выйдет ни одной детали Р(C) = {round(PC, 4)} = {round(PC * 100, 2)}%')

Вероятность того, что из строя не выйдет ни одной детали Р(C) = 0.54 = 54.0%

PD = 1 - PC
print(f'Вероятность того, что вышли из строя хотя бы одна деталь PD = {round(PD, 4)} = {round(PD * 100, 2)}%')

Вероятность того, что вышли из строя хотя бы одна деталь PD = 0.46 = 46.0%

PE = 0.1 * 0.8 * 0.75 + 0.2 * 0.9 * 0.75 + 0.25 * 0.9 * 0.8
PF = PE + PB
print(f'Вероятность того, что выйдет из строя одна деталь Р(E) = {round(PF, 4)} = {round(PF * 100, 2)}%')

Вероятность того, что выйдет из строя одна деталь Р(E) = 0.455 = 45.5%


