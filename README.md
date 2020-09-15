import java.util.Scanner;
import java.util.Arrays;
import java.lang.*;

public class LaborasPirmas {
    public static void main(String[] args){
        String name, surname;
        int n, m, b, a;
        Scanner sc = new Scanner(System.in);

        System.out.println("Enter your first name:");
        name = sc.next();
        System.out.println("Enter your second name:");
        surname = sc.next();
        System.out.println("Entered value: " + name + " " + surname);

        n = name.length();
        m = surname.length();

        System.out.println("Your name has: " + n + " letters ");
        System.out.println("Your second name has: " + m + " letters ");
        a = 2;
        b = n + m;

        int[][] array = new int[n][m];
        double[] rowAverage = new double[n];
        double[] columnAverage = new double[m];


        fillArray(n,m,a,b,array,rowAverage,columnAverage);
        countingAboveAverage(n,m,array,rowAverage);
        countingMaxButNoA(n,m,a,array);
        sortingAFromMinToMax(n,m,a,array);
        minColumnValue(columnAverage);
    }
    public static int generateRandomNumber(int a, int b)
    {
        // Metodas kuris sukuria ir gražina atsitiktinę reikšmę nuo a iki b
        return (int) (Math.random() * (b - a)) + a;
    }
    public static void fillArray(int n, int m, int a, int b, int[][] array, double[] rowAverage, double[] columnAverage)
    {
        double[] allRows = new double[n];
        double[] allColumns = new double[m];

        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < m; j++)
            {
                array[i][j] = generateRandomNumber(a,b);
                allRows[i] += array[i][j];
            }
            rowAverage[i] = allRows[i] / m; // eiluciu vidurkiai
        }
        for(int i = 1; i <= m; i++) //vykdomas spausdinimas dvimacio masyvo, su atsitiktinai sugeneruotomis reiksmemis
        {
            System.out.print("  " + i);
        }
        System.out.println();
        int temp = 1;
        for(int[] row : array)
        {
            System.out.println(temp + Arrays.toString(row));
            temp++;
        }
        for(int p = 0; p < m; p++)
        {
            for(int s = 0; s < n; s++)
            {
                allColumns[p] += array[s][p];
            }
            columnAverage[p] = allColumns[p] / n; // stulpeliu vidurkiai
        }
        for(int i=0;i<n;i++)
            System.out.println("Eiluciu vidurkiai: " + String.format("%.4f", rowAverage[i]));
        for(int i=0;i<m;i++)
            System.out.println("Stulpeliu vidurkiai: " + String.format("%.4f", columnAverage[i]));
    }
    public static void countingAboveAverage(int n, int m, int[][] array, double[] rowAverage)
    {
        int count = 0;
        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < m; j++)
            {
                if(array[i][j] > rowAverage[i])
                {
                    count++;
                }
            }
            System.out.println((i+1) + " eiluteje yra: " + count + " skaiciai, kurie yra didesni uz tos eilutes vidurki");
            count = 0;
        }
    }
    public static void countingMaxButNoA(int n, int m, int a, int[][] array)
    {
        int max = 0;

        for(int i = 0; i < n; i++)
        {
            for(int j = 0; j < m; j++)
            {
                if(array[i][j] > max && i != a - 1 && j != a - 1)
                {
                    max = array[i][j];
                }
            }
        }
        System.out.println("\n" + "Didziausia reiksme netikrinant a sulpelio ir eilutes yra: " + max);
    }
    public static void sortingAFromMinToMax(int n, int m, int a, int[][] array)
    {
        int[] array1 = new int[m];

        for(int i = a - 1; i < a; i++)
        {
            for(int j = 0; j < m; j++)
            {
                array1[j] = array[i][j];
            }
            Arrays.sort(array1);
            System.out.println("\n" + a + " eilutes reiksmes surikiuotos nuo maziausios iki didziausios " + Arrays.toString(array1));
        }
    }
    public static void minColumnValue(double[] columnAverage)
    {
        double minimalColumn = columnAverage[0];
        int length = columnAverage.length;
        int index = 0;
        for(int i = 0; i < length; i++)
        {
            if(columnAverage[i] < minimalColumn)
            {
                minimalColumn = columnAverage[i];
                index = i + 1;
            }
        }
        System.out.println("\n" + "Maziausia stulpelio vidurkio reiksme yra: " + index + " stulpelyje, jo reiksme: " + minimalColumn);
    }
}
