# Intergration

using System;

public class Trapezoidal
{
    private double f(double x)
    {
        return 1.0 / (1.0 + x);
    }

    public double Compute(double a, double b, int n)
    {
        double[] x = new double[n + 1];

        double h = (b - a) / n;

        x[0] = a;
        x[n] = b;
        for (int i = 1; i < n; i++)
        {
            x[i] = a + i * h;
        }

        double sum = f(x[0]);

        for (int j = 1; j < n; j++)
        {
            sum += 2 * f(x[j]);       
        }

        sum += f(x[n]);

        double integration = sum * h / 2;

        return integration;

    }
}

public class Simpson
{
    private double f(double x)
    {
        return 1.0 / (1.0 + x); 
    }

    public double Compute(double a, double b, int n)
    {
        double[] x = new double[n + 1];
        double h = (b - a) / n;

        x[0] = a;

        for (int i = 1; i <= n; i++)
        {
            x[i] = a + h * i;      
        }

        double sum = f(x[0]);        

        for (int j = 1; j < n; j++)
        {
            if (j % 2 != 0)
            {
                sum += 4 * f(x[j]);
            }
            else
            {
                sum += 2 * f(x[j]);
            }

            //Console.WriteLine("f[{0}] = {1}", j, f(x[j]));
        }

        //Console.WriteLine("f[10] = {0}", f(x[10]));
        sum += f(x[n]);

        double integration = sum * h / 3;

        return integration;
    }

    public double Error()
    {
        return 0;
    }

}

public class MainClass
    {
    public static void Main()
    {
        Simpson simpson = new Simpson();
        Trapezoidal trapezoidal = new Trapezoidal();
        double a = 0d;
        double b = 1d;
        int n = 8;

        if (n % 2 == 0)
        {
            Console.WriteLine("Function integration using the Simpson's Rule: " + simpson.Compute(a, b, n));
        }
        else
        {
            Console.WriteLine("n should be an even number");
        }

        Console.WriteLine("Function integration using the Trapezoidal's Rule: " + trapezoidal.Compute(a, b, n));

        Console.ReadLine();
}
}
