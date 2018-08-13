# OOPL6
Składowe statyczne klasy

## Zadanie 0 - Krótkie wprowadzenie
Składowe klasy mogą być statyczne i niestatyczne. Niestatyczne zawsze wiążą się z istnieniem jakiegoś obiektu (pola - odpowiadają elementom obiektu, metody muszą być wywoływane na rzecz obiektu, są komunikatami do obiektu).
Składowe statyczne (pola i metody) są wspólne dla wszystkich obiektów i:
* są deklarowane przy użyciu specyfikatora static,
* mogą być używane nawet wtedy, gdy nie istnieje żaden obiekt klasy

**Uwaga:** ze statycznych metod nie wolno odwoływać się do niestatycznych składowych klasy (obiekt może nie istnieć). Możliwe są natomiast odwołania do innych statycznych składowych.
Spoza klasy do jej statycznych składowych możemy odwoływać się na dwa sposoby:
* `NazwaKlasy.NazwaSkładowej`
* gdy istnieje jakiś obiekt: tak samo jak do niestatycznych składowych (uwaga: jest to
mylące i nie polecane).

## Zadanie 1
Utwórz klasę `Figures`. Umieść w niej poniższy kod i przetestuj działania. Zauważ, że metody statyczne `FieldOfCircle`a i `PerimeterOfCircle` korzystają z innych metod statycznych zawartych w bibliotece `Math`, która również jest klasą. Dodaj wewnątrz klasy kolejne metody statyczne umożliwiające obliczanie (pole i obwód dla figór płaskich, objętość i pole powierzchni całkowitej dla figór przestrzennych) następujących figur: `Square`, `Rectangle`, `Cone`, `Cylinder`. 

```java
package pl.edu.ur.oopl6.zad1;

public class Figures {
    
    /**
     * Inicjalizator statyczny
     */
    static {
        System.out.println("Biblioteka obliczająca wielkość figur geometrycznych!!!");
    }
    
    /**
     * Metoda statyczna obliczająca pole koła
     */
    public static double FieldOfCircle(double r){
        return Math.PI*Math.pow(r,2);
    }
    
    /**
     * Metoda statyczna obliczająca obwód koła
     */
    public static double PerimeterOfCircle(double r){
        return 2*Math.PI*r;
    }
    
}
```

```java
package pl.edu.ur.oopl6.zad1;

public class StaticComponents {

    public static void main(String[] args) {
        // TODO zad 3
        
        System.out.println(Figures.FieldOfCircle(0.5));
        System.out.println(Figures.PerimeterOfCircle(0.5));
    }
    
}
```

## Zadanie 2
Przetestuj i opisz działanie poniższego kodu źródłowego.

```java
package pl.edu.ur.oopl6.zad2;

public class Point {

    private int x;
    private int y;
    private int z;

    // Pole statyczne przechowujące w pamięci ilość obiektów klasy Punkt
    // Pole jest współdzielone dla wszystkich obiektów
    private static int counter;
    public static Punkt last_point;

    public Point(int x, int y, int z) {
        this.x = x;
        this.y = y;
        this.z = z;
        counter++;
        last_point = this;
    }

    public static void ShowLastPoint() {
        System.out.println("Klasa Punkt o współrzędnych (x = " + last_point.x
                + " y = " + last_point.y + ""
                + " z = " + last_point.z + "). Istnieje już"
                + " " + last_point.counter + " obiekt tej klasy.");
    }
    
    @Override
    public String toString(){
        String s = "Klasa Punkt o współrzędnych (x = " + last_point.x
                + " y = " + last_point.y + ""
                + " z = " + last_point.z + "). Istnieje już"
                + " " + last_point.counter + " obiekt tej klasy.";
        return s;
    }

}
```

```java
package pl.edu.ur.oopl6.zad2;

public class ObjectCounter {
    public static void main(String[] args){
        Point[] p = new Point[10];
        Random r = new Random();
        for (int i = 0; i<10; i++){
            p[i] = new Point(r.nextInt(1000), r.nextInt(1000), r.nextInt(1000));
            System.out.println(p[i].toString());
        }
        System.out.println();
        System.out.println("-------------------------------------------------");
        System.out.println(Point.last_point.toString());
        System.out.println("-------------------------------------------------");
        Point.ShowLastPoint();
    }
}
```

## Zadanie 3
Utwórz klasę `Complex` implementującą strukturę liczb zespolonych.

* klasa ma zawierać pola `re` - real oraz `im` - imaginary
* klasa ma zawierać konstruktor inicjalizujący powyższe pola

Do klasy dodaj metody dokonujące obliczeń na tych liczbach tj:
* `abs()` - obliczanie modułu liczby zespolonej
* `plus(Complex b)` - dodawanie (innej liczby zespolonej)
* `minus(Complex b)` - odejmowanie (innej liczby zespolonej)
* `times(Complex b)` - mnożenie (przez inną liczbę zespoloną)
* `scale(double alpha)` - mnożenie (przez skalar (typu `double`))
* `conjugate()` - sprzężenie
* `reciprocal()` - odwrotność
* `divides(Complex b)` - dzielenie (przez inną liczbę zespoloną)
* `exp()` - metoda zwracająca wartość liczby zespolonej w funkcji expotencjalnej
* `sin()` - metoda zwracająca wartość liczby zespolonej w postaci zapisu trygonometrycznego - sinus
* `cos()` - metoda zwracająca wartość liczby zespolonej w postaci zapisu trygonometrycznego - cosinus
* `tan()` - metoda zwracająca wartość liczby zespolonej w postaci zapisu trygonometrycznego - tangens

Dodaj do klasy statyczne odpowiedniki tych metod:

Przykład:

```java
    public Complex plus(Complex b) {
        Complex a = this;
        double real = a.re + b.re;
        double imag = a.im + b.im;
        return new Complex(real, imag);
    }

    public static Complex plus(Complex a, Complex b) {
        double real = a.re + b.re;
        double imag = a.im + b.im;
        Complex sum = new Complex(real, imag);
        return sum;
    }
```

##### W oparciu o opracowanie dr inż. Wojciecha Kozła
