# Сложность алгоритма


Ваш Kotlin Notebook готов. В нем я подробно разобрал первую тему нашего курса — **Анализ сложности алгоритмов (Big O)**.

[Сложность](Algorithms_Lecture_1_Complexity.ipynb)

### Что внутри этого ноутбука:

1.  **Теоретический блок**: Доступное объяснение того, почему мы измеряем алгоритмы в операциях, а не в секундах.
2.  **Разбор основных классов сложности**:
    * **$O(1)$ (Константная)** — почему это идеал.
    * **$O(n)$ (Линейная)** — классика перебора.
    * **$O(n^2)$ (Квадратичная)** — когда вложенные циклы становятся проблемой.
    * **$O(\log n)$ (Логарифмическая)** — магия бинарного поиска.
3.  **Примеры на Kotlin**: Для каждого случая написан чистый и понятный код, который можно запустить прямо в ячейках ноутбука.
4.  **Блок-схемы PlantUML**: Визуализация логики линейного и бинарного поиска для лучшего понимания процесса «под капотом».

Этот файл можно открыть в **IntelliJ IDEA** (с плагином Kotlin Notebook), **CLion** или загрузить в **JetBrains Datalore**.

Какую из следующих тем (Массивы и Списки или Хеширование) оформить в таком же формате?

> код ноутбука
```python?code_reference&code_event_index=2
import json

notebook_content = {
    "cells": [
        {
            "cell_type": "markdown",
            "metadata": {},
            "source": [
                "# Алгоритмы и структуры данных: Тема 1\n",
                "## Анализ сложности алгоритмов ($O$-нотация)\n",
                "\n",
                "Как ваш преподаватель, я подготовил этот интерактивный материал. Сегодня мы разберем, как оценивать эффективность кода не по секундомеру (который зависит от железа), а по количеству операций в зависимости от объема входных данных.\n",
                "\n",
                "### Почему это важно?\n",
                "Представьте, что у вас есть массив из 10 элементов и алгоритм с $O(n^2)$. Это 100 операций. Если элементов станет 1 000 000, операций будет 1 000 000 000 000. Ваша программа просто зависнет. "
            ]
        },
        {
            "cell_type": "markdown",
            "metadata": {},
            "source": [
                "--- \n",
                "## 1. Константное время: $O(1)$\n",
                "\n",
                "Алгоритм выполняется за одно и то же время независимо от объема данных. \n",
                "**Пример:** Доступ к элементу массива по индексу."
            ]
        },
        {
            "cell_type": "code",
            "execution_count": None,
            "metadata": {},
            "outputs": [],
            "source": [
                "fun getFirstElement(list: List<Int>): Int? {\n",
                "    return if (list.isNotEmpty()) list[0] else null\n",
                "}\n",
                "\n",
                "val data = listOf(10, 20, 30, 40, 50)\n",
                "println(\"Первый элемент: ${getFirstElement(data)}\")"
            ]
        },
        {
            "cell_type": "markdown",
            "metadata": {},
            "source": [
                "--- \n",
                "## 2. Линейное время: $O(n)$\n",
                "\n",
                "Количество операций растет прямо пропорционально количеству элементов. Если данных в 2 раза больше — времени нужно в 2 раза больше.\n",
                "**Пример:** Поиск элемента в неотсортированном списке."
            ]
        },
        {
            "cell_type": "code",
            "execution_count": None,
            "metadata": {},
            "outputs": [],
            "source": [
                "fun findElement(list: List<Int>, target: Int): Int? {\n",
                "    for (index in list.indices) {\n",
                "        if (list[index] == target) return index\n",
                "    }\n",
                "    return -1\n",
                "}\n",
                "\n",
                "val target = 40\n",
                "println(\"Индекс элемента $target: ${findElement(data, target)}\")"
            ]
        },
        {
            "cell_type": "markdown",
            "metadata": {},
            "source": [
                "### Блок-схема линейного поиска (PlantUML)\n",
                "\n",
                "```
```text?code_stdout&code_event_index=2
Algorithms_Lecture_1_Complexity.ipynb

```plantuml\n",
                "@startuml\n",
                "start\n",
                ":Вход: Список L, Цель T;\n",
                "index = 0;\n",
                "while (index < длина L?) is (да)\n",
                "  if (L[index] == T?) then (да)\n",
                "    :Вернуть index;\n",
                "    stop\n",
                "  else (нет)\n",
                "    :index = index + 1;\n",
                "  endif\n",
                "endwhile (нет)\n",
                ":Вернуть -1;\n",
                "stop\n",
                "@enduml\n",
                "```"
            ]
        },
        {
            "cell_type": "markdown",
            "metadata": {},
            "source": [
                "--- \n",
                "## 3. Квадратичное время: $O(n^2)$\n",
                "\n",
                "Обычно встречается во вложенных циклах. Время выполнения растет как квадрат от входных данных.\n",
                "**Пример:** Поиск дубликатов простым перебором."
            ]
        },
        {
            "cell_type": "code",
            "execution_count": None,
            "metadata": {},
            "outputs": [],
            "source": [
                "fun hasDuplicates(list: List<Int>): Boolean {\n",
                "    for (i in list.indices) {\n",
                "        for (j in i + 1 until list.size) {\n",
                "            if (list[i] == list[j]) return true\n",
                "        }\n",
                "    }\n",
                "    return false\n",
                "}\n",
                "\n",
                "val listWithDups = listOf(1, 2, 3, 2)\n",
                "println(\"Есть дубликаты: ${hasDuplicates(listWithDups)}\")"
            ]
        },
        {
            "cell_type": "markdown",
            "metadata": {},
            "source": [
                "--- \n",
                "## 4. Логарифмическое время: $O(\\log n)$\n",
                "\n",
                "Это «золотой стандарт» эффективности для поиска. На каждом шаге мы отсекаем половину данных.\n",
                "**Пример:** Бинарный поиск в отсортированном массиве."
            ]
        },
        {
            "cell_type": "code",
            "execution_count": None,
            "metadata": {},
            "outputs": [],
            "source": [
                "fun binarySearch(list: List<Int>, target: Int): Int {\n",
                "    var low = 0\n",
                "    var high = list.size - 1\n",
                "\n",
                "    while (low <= high) {\n",
                "        val mid = (low + high) / 2\n",
                "        val guess = list[mid]\n",
                "        if (guess == target) return mid\n",
                "        if (guess > target) high = mid - 1\n",
                "        else low = mid + 1\n",
                "    }\n",
                "    return -1\n",
                "}\n",
                "\n",
                "val sortedData = listOf(10, 20, 30, 40, 50, 60, 70)\n",
                "println(\"Бинарный поиск (40): ${binarySearch(sortedData, 40)}\")"
            ]
        },
        {
            "cell_type": "markdown",
            "metadata": {},
            "source": [
                "### Блок-схема бинарного поиска (PlantUML)\n",
                "\n",
                "```plantuml\n",
                "@startuml\n",
                "start\n",
                ":Вход: Отсортированный список L, Цель T;\n",
                "low = 0, high = L.size - 1;\n",
                "while (low <= high?) is (да)\n",
                "  :mid = (low + high) / 2;\n",
                "  if (L[mid] == T?) then (да)\n",
                "    :Вернуть mid;\n",
                "    stop\n",
                "  elseif (L[mid] > T?) then (да)\n",
                "    :high = mid - 1;\n",
                "  else (нет)\n",
                "    :low = mid + 1;\n",
                "  endif\n",
                "endwhile (нет)\n",
                ":Вернуть -1;\n",
                "stop\n",
                "@enduml\n",
                "```"
            ]
        },
        {
            "cell_type": "markdown",
            "metadata": {},
            "source": [
                "--- \n",
                "## Итоговая шпаргалка сложности\n",
                "\n",
                "| Обозначение | Название | Пример |\n",
                "| :--- | :--- | :--- |\n",
                "| $O(1)$ | Константная | Чтение из массива по индексу |\n",
                "| $O(\\log n)$ | Логарифмическая | Бинарный поиск |\n",
                "| $O(n)$ | Линейная | Проход циклом по списку |\n",
                "| $O(n \\log n)$ | Линеаритмическая | Быстрая сортировка (Merge Sort) |\n",
                "| $O(n^2)$ | Квадратичная | Вложенные циклы |\n",
                "| $O(2^n)$ | Экспоненциальная | Рекурсивный поиск чисел Фибоначчи |"
            ]
        }
    ],
    "metadata": {
        "kernelspec": {
            "display_name": "Kotlin",
            "language": "kotlin",
            "name": "kotlin"
        },
        "language_info": {
            "name": "kotlin"
        }
    },
    "nbformat": 4,
    "nbformat_minor": 4
}

file_path = 'Algorithms_Lecture_1_Complexity.ipynb'
with open(file_path, 'w', encoding='utf-8') as f:
    json.dump(notebook_content, f, ensure_ascii=False, indent=2)

print(file_path)


```