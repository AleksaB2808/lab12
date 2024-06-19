# lab12
def __init__(self, rows, columns):
    self.rows = rows
    self.columns = columns
    self.data = [[0] * columns for _ in range(rows)]
Конструктор класу ініціалізує матрицю з вказаною кількістю рядків rows і стовпців columns. Всі елементи матриці початково ініціалізуються нулями.

Метод add_element

def add_element(self, row, column, value):
    if 0 <= row < self.rows and 0 <= column < self.columns:
        self.data[row][column] = value
Метод add_element дозволяє додавати значення value до позиції (row, column) у матриці, за умови, що координати (row, column) знаходяться в межах розмірів матриці.

Метод sum_of_rows

def sum_of_rows(self):
    return [sum(row) for row in self.data]
Метод sum_of_rows обчислює суму кожного рядка у матриці і повертає список сум.

Метод transpose

def transpose(self):
    transposed = Matrix(self.columns, self.rows)
    for i in range(self.rows):
        for j in range(self.columns):
            transposed.data[j][i] = self.data[i][j]
    return transposed
Метод transpose створює і повертає транспоновану матрицю, де елементи self.data[i][j] стають transposed.data[j][i].

Метод multiply_by

def multiply_by(self, other):
    if self.columns != other.rows:
        raise ValueError(
            "Number of columns in the first matrix must be equal to the number of rows in the second matrix.")

    result = Matrix(self.rows, other.columns)
    for i in range(self.rows):
        for j in range(other.columns):
            for k in range(self.columns):
                result.data[i][j] += self.data[i][k] * other.data[k][j]
    return result
Метод multiply_by множить поточну матрицю на іншу матрицю other, якщо кількість стовпців у поточній матриці (self.columns) дорівнює кількості рядків у матриці other. Результат зберігається у новій матриці result.

Метод is_symmetric

def is_symmetric(self):
    if self.rows != self.columns:
        return False
    for i in range(self.rows):
        for j in range(i + 1, self.columns):
            if self.data[i][j] != self.data[j][i]:
                return False
    return True
Метод is_symmetric перевіряє, чи є матриця симетричною (дорівнює транспонованій матриці).

Метод rotate_right

def rotate_right(self):
    self.data = [[self.data[j][i] for j in range(self.rows - 1, -1, -1)] for i in range(self.columns)]
Метод rotate_right обертає матрицю на 90 градусів вправо, замінюючи поточні дані self.data на нові значення, що відповідають оберненому порядку.

Метод flatten

def flatten(self):
    return [element for row in self.data for element in row]
Метод flatten повертає матрицю у вигляді одновимірного масиву (списку всіх елементів матриці).

Метод diagonal

def diagonal(self):
    if self.rows != self.columns:
        raise ValueError("Matrix must be square to extract diagonal.")
    return [self.data[i][i] for i in range(self.rows)]
Метод diagonal виділяє діагональні елементи з квадратної матриці і повертає список їх значень.

Статичний метод from_list

@staticmethod
def from_list(list_of_lists):
    rows = len(list_of_lists)
    columns = len(list_of_lists[0])
    matrix = Matrix(rows, columns)
    for i in range(rows):
        for j in range(columns):
            matrix.add_element(i, j, list_of_lists[i][j])
    return matrix
Статичний метод from_list створює новий об'єкт Matrix зі списку списків list_of_lists, де кожен внутрішній список відповідає рядку в матриці.






