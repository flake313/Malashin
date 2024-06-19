import math

# Функция для вычисления косинуса через ряд Тейлора с использованием периодичности
def taylor_cos(x, k):
    x = x % (2 * math.pi)  # Приводим x к диапазону от 0 до 2*pi
    q, s, n = 1, 0, 0
    while abs(q) > k:
        s += q
        n += 1
        q *= (-1) * (x * x) / ((2 * n - 1) * (2 * n))
    return s

# Функция для вычисления экспоненты через ряд Тейлора
def taylor_exp(x, k):
    q, s, n = 1, 0, 0
    while abs(q) > k:
        s += q
        n += 1
        q *= x / n
    return s

# Функция для вычисления 5 * e^(0.5 / (cos(x) + 14)) через ряды Тейлора
def complex_function_taylor(x_rad, k):
    try:
        # Вычисление косинуса от значения x с использованием ряда Тейлора
        cos_x = taylor_cos(x_rad, k)
        
        # Вычисление значения экспоненты
        exponent = 0.5 / (cos_x + 14)
        exp_value = taylor_exp(exponent, k)
        
        # Умножение на 5
        result = 5 * exp_value
        
        return result
    except ZeroDivisionError:
        return "Ошибочка."

# Ввод значения x в радианах и точности k
x_rad = float(input("Введите значение x в радианах: "))
k = float(input("Введите желаемую точность (погрешность), например, 0.000000001: "))

# Вычисление результата
result = complex_function_taylor(x_rad, k)

# Вывод результата с точностью до 16 знаков после запятой
print(f"Результат вычисления функции 5 * e^(0.5 / (cos({x_rad}) + 14)) с использованием рядов Тейлора: {result:.16f}")

