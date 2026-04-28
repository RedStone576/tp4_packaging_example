# Pengantar Package Java

## Cara Mengorganisasikan Proyek Java Dengan Directory (a.k.a. Folder)

Sebenarnya, bila sebuah file tidak memiliki deklarasi "package," file tersebut dianggap hidup di "default package", tidak mempedulikan di folder mana file itu berada. 

Artinya, struktur directory dari sebuah proyek Java tidak akan mempengaruhi namaspace jika tidak menggunakan package.

Misal kita buat:
```
tp4/
    Main.java  
    entity/
        User.java
        monster/
            Monster.java
```

```java
/* ~/tp4/Main.java */

public class Main
{
    public static void main(String[] args)
    {
        User alpha = new User();
        alpha.greet_a_monster();
    }
}
```

```java
/* ~/tp4/entity/User.java */

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
/* ~/tp4/entity/monster/Monster.java */

public class Monster
{
    public void say()
    {
        System.out.println("Sebenarnya saya adalah orang Jawa Timur");
    }
}
```

Kita bisa menggunakan flag `-cp` (cp: classpath) untuk memberi tahu lokasi file `.class` kita.

Linux/Mac:
```bash
javac -cp ".:entity:entity/monster" Main.java
```

Windows:
```bash
javac -cp ".;entity;entity\monster" Main.java
```

Maka, akan menghasilkan:
```bash
tp4/
    Main.class
    Main.java
    entity/
        User.class
        User.java
        monster/
            Monster.class
            Monster.java
```

Dan bisa dijalankan dengan:

Linux/Mac:
```bash
java -cp ".:entity:entity/monster" Main
```

Windows:
```bash
java -cp ".;entity;entity\monster" Main
```



## Cara Mengorganisasikan Proyek Java Dengan Namespace

Misal kita memiliki:
```
tp4/
    Main.java
    Monster.java
```
(perhatikan bahwa struktur directory masih flat, tidak terdapat directory lain di dalamnya)

Kita bisa mendeklarasikan namespace pada file `Monster.java` seperti berikut:
```java
package entity.monster;
```

Public class pada file tersebut akan memili "fully qualified name" berupa `entity.monster.Monster`, dan bisa kita import dengan:
```
import entity.monster.Monster
```
https://docs.oracle.com/javase/specs/jls/se11/html/jls-6.html#jls-6.7

Contoh penggunaan:
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

Lalu bisa kita compile dengan:
```bash
javac -d . Monster.java Main.java
```
`-d` (d: destination) di maka hasil `*.class` akan disimpan relatif di directory saat ini

Maka akan menghasilkan:
```
tp4/
    Main.class
    Main.java
    Monster.java
    entity/
        monster/
            Monster.class
```
Perhatikan bahwa compiler akan secara otomatis membuat directory baru `entity/monster/` dan meletakkan `Monster.class` di sana.

Dan dapat dijalankan hanya dengan:
```bash
java Main
```

### Mengapa tidak perlu memberi tahu classpath (-d)???

- Karena secara default, classpath = .
- dan, struktur `.class` sudah sesuai dengan deklarasi package

Java pertama akan mencari class sesuai dengan fully qualified name yang diberikan, `entity.monster.Monster` akan ditemukan `entity/monster/Monster.class`.




## Cara Mengorganisasikan Proyek Java Dengan Package (Directory + Namaspace)

Kita gabungkan kedua pendekatan sebelumnya, andaikan dengan struktur seperti berikut:
```bash
tp4/
    Main.java
    entity/
        User.java
        monster/
            Monster.java
```

---
**Perlu diingat: layaknya nama file dan nama public class, struktur dari directory, harus sama dengan deklarasi package-nya.**

Contoh:
```
entity/monster/Monster.java
```
```java
package entity.monster;
```
---

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

```java
/* ~/tp4/entity/User.java */

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
/* ~/tp4/Main.java */

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

Bisa langsung kita compile dengan:
```bash
javac -d . Main.java entity/User.java entity/monster/Monster.java
```

Maka akan menghasilkan:
```
tp4/
    Main.class
    Main.java
    entity/
        User.class
        User.java
        monster/
            Monster.class
            Monster.java
```

Lalu bisa dijalankan hanya dengan:
```bash
java Main
```

## Konvensi penaamaan
- nama package ditulis dengan lowercase untuk menghindari konflik dengan nama kelas dan interface
- biasanya, proyek enterprise menggunakan domain name mereka yang dibalik untuk prefiks nama package mereka. (contoh yang mungkin pernah dilihat: `com.mojang.minecraft`)
- package yang berada di Java itu sendiri, dimulai dengan `java.` atau `javax.`

https://docs.oracle.com/javase/tutorial/java/package/namingpkgs.html
 
