using System;

class Program
{
    // Функція створення матриці з випадковими значеннями
    static void Create(int[,] matrix, int min, int max)
    {
        Random r = new Random();
        for (int i = 0; i < matrix.GetLength(0); i++)
        {
            for (int j = 0; j < matrix.GetLength(1); j++)
            {
                matrix[i, j] = r.Next(min, max + 1); // включно з max
            }
        }
    }

    // Вивід матриці на екран
    static void Print(int[,] matrix)
    {
        for (int i = 0; i < matrix.GetLength(0); i++)
        {
            for (int j = 0; j < matrix.GetLength(1); j++)
            {
                Console.Write($"{matrix[i, j],5}");
            }
            Console.WriteLine();
        }
    }

    // Пошук усіх входжень елемента
    static void FindElement(int[,] matrix, int target)
    {
        bool found = false;
        Console.WriteLine($"\nПошук значення {target}:");
        for (int i = 0; i < matrix.GetLength(0); i++)
        {
            for (int j = 0; j < matrix.GetLength(1); j++)
            {
                if (matrix[i, j] == target)
                {
                    Console.WriteLine($"Знайдено на позиції: рядок {i}, стовпець {j}");
                    found = true;
                }
            }
        }
        if (!found)
        {
            Console.WriteLine("Елемент не знайдено.");
        }
    }

    // Сортування рядків матриці за зростанням
    static void SortRows(int[,] matrix)
    {
        int cols = matrix.GetLength(1);
        for (int i = 0; i < matrix.GetLength(0); i++)
        {
            // Сортування кожного рядка (методом бульбашки)
            for (int j = 0; j < cols - 1; j++)
            {
                for (int k = 0; k < cols - j - 1; k++)
                {
                    if (matrix[i, k] > matrix[i, k + 1])
                    {
                        int temp = matrix[i, k];
                        matrix[i, k] = matrix[i, k + 1];
                        matrix[i, k + 1] = temp;
                    }
                }
            }
        }
    }

    static void Main(string[] args)
    {
        const int ROWS = 5;
        const int COLS = 6;
        int[,] matrix = new int[ROWS, COLS];

        Create(matrix, -10, 10);

        Console.WriteLine("Початкова матриця:");
        Print(matrix);

        Console.Write("\nВведіть значення для пошуку: ");
        int target = int.Parse(Console.ReadLine());

        FindElement(matrix, target);

        Console.WriteLine("\nМатриця після сортування рядків:");
        SortRows(matrix);
        Print(matrix);
    }
}
