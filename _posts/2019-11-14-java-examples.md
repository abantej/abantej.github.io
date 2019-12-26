---
layout: post
title:  "Java Examples"
date:   2019-11-14 10:28:00 +0800
categories: java
---

### Printing Elements
```java
// Old
for (Hero hero: heroes) {
    System.out.println(hero.getName());
}

// Java 8
heroes.forEach(hero -> System.out.println(hero.getName()));
```

### Sorting Elements
```java

// Old
Collections.sort(heroes, new Comparator<Hero>() {
   public int compare(Hero hero1, Hero hero2) {
       return hero1.getName().compareToIgnoreCase(hero2.getName());
   }
});

// Java 8
heroes.sort(Comparator.comparing(Hero::getName));

```

### Listing hidden files
```java
// Old
File[] hiddenFiles = new File(".").listFiles(new FileFilter() {
    @Override
    public boolean accept(File file) {
        return file.isHidden();
    }
});
// Java 8
hiddenFiles = new File(".").listFiles(File::isHidden);
```

### Passing Methods
```java
private static class Hero {
    private String name;
    private Attribute attribute;
    public Hero (String name, Attribute attribute) {
        this.name = name;
        this.attribute = attribute;
    }

    public String getName() {
        return this.name;
    }

    public Attribute getAttribute() {
        return this.attribute;
    }

    public static boolean isStrengthHero(Hero hero) {
        return Attribute.STRENGTH.equals(hero.getAttribute());
    }

    public static boolean isAgilityHero(Hero hero) {
        return Attribute.AGILITY.equals(hero.getAttribute());
    }

    public static boolean isIntelligenceHero(Hero hero) {
        return Attribute.INTELLIGENCE.equals(hero.getAttribute());
    }
}

public interface Predicate<T> {
    boolean test(T t);
}

...

static List<Hero> filterHeroes(List<Hero> heroes, Predicate<Hero> p) {
    List<Hero> result = new ArrayList<>();
    for (Hero hero: heroes) {
        if (p.test(hero)) {
            result.add(hero);
        }
    }
    return result;
}

// Using predicates

List<Hero> strengthHeroes = filterHeroes(heroes, Hero::isStrengthHero);

List<Hero> agilityHeroes = filterHeroes(heroes, Hero::isAgilityHero);

List<Hero> intHeroes = filterHeroes(heroes, Hero::isIntelligenceHero);


// Lambda

List<Hero> strengthHeroes = filterHeroes(heroes, (Hero h) -> Attribute.STRENGTH.equals(h.getAttribute()));

List<Hero> agilityHeroes = filterHeroes(heroes, (Hero h) -> Attribute.AGILITY.equals(h.getAttribute()));

List<Hero> intHeroes = filterHeroes(heroes, (Hero h) -> Attribute.INTELLIGENCE.equals(h.getAttribute()));
...

```

### Grouping and filtering
```java
// Old
Map<Currency, List<Transaction>> transactionsByCurrencies = new HashMap<>();
for (Transaction transaction: transactions) {
    if (transaction.getPrice() > 0) {
        Currency currency = transaction.getCurrency();
        List<Transaction> transactionsForCurrency = transactionsByCurrencies.get(currency);
        if (transactionsForCurrency == null) {
            transactionsForCurrency = new ArrayList<>();
            transactionsByCurrencies.put(currency, transactionsForCurrency);
        }
        transactionsForCurrency.add(transaction);
    }
}

for (Map.Entry<Currency, List<Transaction>> entry : transactionsByCurrencies.entrySet()) {
    List<Transaction> txns = transactionsByCurrencies.get(entry.getKey());
    for (Transaction txn: txns) {
        System.out.println(entry.getKey() + " " + txn.getPrice());
    }
}

// Java 8
import static java.util.stream.Collectors.groupingBy;

transactionsByCurrencies = transactions.stream()
        .filter((Transaction t) -> t.getPrice() > 0)
        .collect(groupingBy(Transaction::getCurrency));


transactionsByCurrencies.forEach((k, v) -> {
    v.forEach((Transaction t) -> System.out.println(t.getCurrency() + " " + t.getPrice()));
});

```

### Sorting
```java
List<Hero> heroes = HeroList.HEROES;
heroes.sort(Comparator.comparing(Hero::getName));
```

### Predicate
```java
import java.util.ArrayList;
import java.util.List;

public class PredicateExample {

    enum Color {
        RED,
        GREEN,
        BLUE,
        BLACK,
        WHITE,
        PURPLE
    }

    @FunctionalInterface
    interface Predicate<T> {
        boolean test(T t);
    }

    static boolean hasColor(List<Color> colors, Predicate<Color> p) {
        for (Color color: colors) {
            if (p.test(color)) {
                return true;
            }
        }
        return false;
    }

    public static void main(String[] args) {
        List<Color> colors = new ArrayList<>();
        colors.add(Color.RED);
        colors.add(Color.BLUE);
        colors.add(Color.WHITE);
        boolean hasBlue = hasColor(colors, c -> c.equals(Color.BLACK));
        System.out.println(hasBlue);
    }
}
```

### Consumer
```java
import java.util.ArrayList;
import java.util.List;

public class ConsumerExample {

    @FunctionalInterface
    interface Consumer<T> {
        void accept(T t);
    }

    static <T> void forEach(List<T> list, Consumer<T> c) {
        for (T i: list) {
            c.accept(i);
        }
    }

    public static void main(String[] args) {
        List<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Orange");
        fruits.add("Grapes");
        fruits.add("Watermelon");
        forEach(fruits, System.out::println);
    }
}
```

### Function

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

public class FunctionExample {
    private interface Function<T, R> {
        R apply(T t);
    }

    static <T, R> List<R> map(List<T> list, Function<T, R> f) {
        List<R> result = new ArrayList<>();
        for (T s : list) {
            result.add(f.apply(s));
        }
        return result;
    }

    public static void main(String[] args) {
        List<Integer> list = map(Arrays.asList("lambdas", "in", "action"), String::length);
        list.forEach(System.out::println);
    }
}
```

### Exceptions in Lambda
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.util.function.Function;

public class BufferedReaderExample {

    @FunctionalInterface
    interface BufferedReaderProcessor {
        String process(BufferedReader b) throws IOException;
    }

    public static void main(String[] args) {
        BufferedReaderProcessor p = (BufferedReader br) -> br.readLine();

        Function<BufferedReader, String> f = (BufferedReader b) -> {
            try {
                return b.readLine();
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        };
    }
}
```

### Lambda Type Checking Process

```java
List<Apple> heavierThan150g = filter(inventory, (Apple a) -> a.getWeight() > 150);
```

1. You look up the declaration of the filter method.
2. It expects as the second formal parameter an object of type Predicate<Apple> (the target type).
3. Predicate<Apple> is a functional interface defining a single abstract method called test.
4. The method test describes a function descriptor that accepts an Apple and returns a boolean.
5. Any actual argument to the filter method needs to match this requirement.

### Decrypt Base64 Encryption

```java
import java.security.GeneralSecurityException;
import javax.crypto.Cipher;
import javax.crypto.spec.IvParameterSpec;
import javax.crypto.spec.SecretKeySpec;
import javax.xml.bind.DatatypeConverter;
import java.util.Base64;

public class Base64Decryptor {
    private static byte[] des_cbc_decrypt(
            byte[] encrypted_password,
            byte[] decryption_key,
            byte[] iv)
            throws GeneralSecurityException {

        Cipher cipher = Cipher.getInstance("DES/CBC/PKCS5Padding");
        cipher.init(Cipher.DECRYPT_MODE, new SecretKeySpec(decryption_key, "DES"), new IvParameterSpec(iv));
        return cipher.doFinal(encrypted_password);
    }

    private static byte[] decrypt_v4(
            byte[] encrypted,
            byte[] db_system_id)
            throws GeneralSecurityException {
        byte[] encrypted_password = Base64.getDecoder().decode(encrypted);
        byte[] salt = DatatypeConverter.parseHexBinary("051399429372e8ad");

// key = db_system_id + salt
        byte[] key = new byte[db_system_id.length + salt.length];
        System.arraycopy(db_system_id, 0, key, 0, db_system_id.length);
        System.arraycopy(salt, 0, key, db_system_id.length, salt.length);

        java.security.MessageDigest md = java.security.MessageDigest.getInstance("MD5");
        for (int i = 0; i < 42; i++) {
            key = md.digest(key);
        }

// secret_key = key [0..7]
        byte[] secret_key = new byte[8];
        System.arraycopy(key, 0, secret_key, 0, 8);

// iv = key [8..]
        byte[] iv = new byte[key.length - 8];
        System.arraycopy(key, 8, iv, 0, key.length - 8);

        return des_cbc_decrypt(encrypted_password, secret_key, iv);
    }

    public static void main(String[] argv) {
        try {

            byte[] encrypted = argv[0].getBytes();
            byte[] db_system_id = argv[1].getBytes();

            byte[] x = decrypt_v4(encrypted, db_system_id);

            String password = new String(x);

            System.out.println(password);
        } catch (Exception e) {
            System.out.println(e.toString());
        }
    }
}
```