# Pengantar Package Java

## Cara Mengorganisasikan Proyek Java Dengan Directory (a.k.a. Folder)

Sebenarnya, bila sebuah file tidak memiliki deklarasi package, file tersebut dianggap hidup di default package.
Walaupun file tersebut hidup di sebuah directory dalam directory.

Kita bisa menggunakan flag `-cp` untuk memberi tahu java, di mana classpath dari sebuah file berada.

```bash
javac -cp . Main.java entity/User.java entity/monster/Monster.java
java -cp . Main```

## Cara Mengorganisasikan Proyek Java Dengan Namespace

Misal:
```
tp4/
    Main.java
    Monster.java```
    
```java
/* ~/tp4/Monster.java */

package entity.monster;

public class Monster
{
    public void say()
    {
        System.out.println("Sebenarnya saya adalah orang Jawa Timur");
    }
}```

```java
import entity.monster.Monster;

public class Main
{
    public static void main(String[] args)
    {
        Monster jteam = new Monster();
        jteam.say();
    }
}```

Lalu bisa kita compile dengan
```bash
javac -d . Main.java entity/User.java entity/monster/Monster.java```

## Cara Mengorganisasikan Proyek Java Dengan Package (Directory + Namaspace)

Perlu diingat: layaknya nama file dan nama public class, struktur dari directory, harus sama dengan nama package.


