# NewtonVerfahren
````csharp
using System;

namespace NewtonVerfahren
{
    internal class Program
    {
        static void Main(string[] args)
        {
            double startwert = 2;
            Console.WriteLine("Funktion: f(x)=x³-x-2");

            double funktionswert = ContinousFunction(startwert);
            Console.WriteLine($"Funktionswert bei x = {startwert} ist {funktionswert}");

            double ableitung1 = DerivativeOfContinousFunction(startwert);
            Console.WriteLine($"Erste ABleitung = {ableitung1}");

            double nullstelle = CalculateRootOfPolynomial(startwert);
            if (double.IsNaN(nullstelle))
            {
                Console.WriteLine("Keine Konvergenz erreicht");
            }
            else
            {
                Console.WriteLine($"Die Nullstelle ist: {nullstelle}");
            }
        }

        public static double ContinousFunction(double x)
        {
            return Math.Pow(x, 3)-x - 2;
        }

        public static double DerivativeOfContinousFunction(double x)
        {
            return 3* Math.Pow(x, 2) - 1;
        }
        public static double CalculateRootOfPolynomial(double x0)
        {
            double tol = 1e-6; // wert wird als ausreichend genau betrachtet wenn 0,000001
            int maxIter = 1000; // Maximale Anzahl an Iterationen
            int iter = 0;
            double x = x0;

            while (iter < maxIter) //abbruch nach maximal 1000Iterationen
            {
                double fx = ContinousFunction(x); //wert der Funktionswert bei 2 = 4
                double fpx = DerivativeOfContinousFunction(x); //wert der ableitung

                if (Math.Abs(fx) < tol) //prüft ob fx kleiner als die toleranz ist
                {
                    return x;
                }

                x = x - fx / fpx; // Aktualisiert x


                iter++; //+1 Iteration
            }
            return double.NaN;
        }
    }
}
