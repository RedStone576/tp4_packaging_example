# Pengantar Package Java

## Cara Mengorganisasikan Proyek Java Dengan Directory (a.k.a. Folder)

Sebenarnya, bila sebuah file tidak memiliki deklarasi package, file tersebut dianggap hidup di default package.
Walaupun file tersebut hidup di sebuah directory dalam directory.

Kita bisa menggunakan flag `-cp` untuk memberi tahu java, di mana classpath dari sebuah file berada.

```bash
javac -cp . Main.java entity/User.java entity/monster/Monster.java
java -cp . Main
```

## Cara Mengorganisasikan Proyek Java Dengan Namespace

Misal kita memiliki:
```
tp4/
    Main.java
    Monster.java
```

Kita bisa mendeklarasikan bahwa sebuah file hidup di dalam sebuah package dengan `package <kategori>.<nama file>;`
    
```java
/* ~/tp4/Monster.java */

package entity.monster;

public class Monster
{
    public void say()
    {
        System.out.println("Sebenarnya saya adalah orang Jawa Timur");
    }
}
```

Lalu bisa kita import dengan `import <kategori>.<nama file>.<nama class>`

```java
/* ~/tp4/Main.java */

import entity.monster.Monster;

public class Main
{
    public static void main(String[] args)
    {
        Monster jteam = new Monster();
        jteam.say();
    }
}
```

Lalu bisa kita compile dengan
```bash
javac -d . Monster.java Main.java
```

Maka akan menghasilkan
```bash
entity/monster/Monster.class
Main.class
```

Semua file masih berada di dalam sebuah directory yang berstruktur flat, tetapi Java kengorganisasikannya dengan otomatis.

Tidak lupa, tentunya bisa di-run dengan
```bash
java Main
```

## Cara Mengorganisasikan Proyek Java Dengan Package (Directory + Namaspace)

Kita gabungkan kedua pendekatan sebelumnya, andaikan dengan struktur seperti berikut
```bash
tp4/
    Main.java
    entity/
        User.java
        monster/
            Monster.java
```

Dengan files berikut:
```java
/* ~/tp4/entity/monster/Monster.java */

package entity.monster;

public class Monster
{
    public void say()
    {
        System.out.println("Sebenarnya saya adalah orang Jawa Timur");
    }
}
```

**Perlu diingat: layaknya nama file dan nama public class, struktur dari directory, harus sama dengan nama package.**

```java
package entity;

import entity.monster.Monster;

public class User
{
    public void greet_a_monster()
    {
        System.out.println("halo bang");
        
        Monster jteam = new Monster();
        jteam.say();
    }
}
```

```java
import entity.User;

public class Main
{
    public static void main(String[] args)
    {
        User alpha = new User();
        alpha.greet_a_monster();
    }
}
```


