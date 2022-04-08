using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace kursova_1
{
    internal class Program
    {

        private static void Swap(int[] arr, int i, int j)
        {
            var tmp = arr[i];
            arr[i] = arr[j];
            arr[j] = tmp;
        }

        private static int Partition(int[] arr, int low, int high)
        {
            var pivotPos = (high + low) / 2;
            var pivot = arr[pivotPos];

            Swap(arr, low, pivotPos);

            var left = low;
            for (var i = low + 1; i <= high; i++)
            {
                if (arr[i].CompareTo(pivot) >= 0) continue;

                left++;

                Swap(arr, i, left);
            }
            Swap(arr, low, left);

            return left;
        }

        private static void QuicksortSequential(int[] arr, int left, int right)
        {
            if (right <= left) return;

            var pivot = Partition(arr, left, right);

            QuicksortSequential(arr, left, pivot - 1);

            QuicksortSequential(arr, pivot + 1, right);
        }


        private static async void QuicksortParallel(int[] arr, int left, int right)
        {
            if (right <= left) return;

            else
            {
                var pivot = Partition(arr, left, right);

                Parallel.Invoke(
                () => QuicksortParallel(arr, left, pivot - 1),
                () => QuicksortParallel(arr, pivot + 1, right));

                //Console.WriteLine($"Виконується задача {Task.CurrentId}");
            }
        }

        static void Main(string[] args)
        {
            while (true)
            {
                Stopwatch timer = new Stopwatch();

                Console.Write("Введiть к-ть елементiв масиву: ");

                int elements = Convert.ToInt32(Console.ReadLine());

                int[] test = new int[elements];

                var random = new Random();

                //Console.Write("\nПочатковий масив: ");

                for (int i = 0; i < elements; i++)
                {
                    test[i] = random.Next(0, 1000);

                    //Console.Write( test[i] + " ");
                }

                //Console.WriteLine();
                timer.Start();

                //QuicksortSequential(test, 0, test.Length - 1);

                QuicksortParallel(test, 0, test.Length - 1);

                timer.Stop();

                //Console.Write("Вiдсортований масив: ");
                //foreach (var v in test)
                //Console.Write(v + " ");

                Console.WriteLine($"Витрачений час: {timer.ElapsedMilliseconds} \n");
                //Console.WriteLine("\n");
            }
        }
    }
}
