---
layout: post
title:  "Java Examples"
date:   2019-11-14 10:28:00 +0800
categories: java
---

### Printing Elements

{% highlight java %}

// Old
for (Hero hero: heroes) {
    System.out.println(hero.getName());
}

// Java 8
heroes.forEach(hero -> System.out.println(hero.getName()));

{% endhighlight %}

### Sorting Elements

{% highlight java %}

// Old
Collections.sort(heroes, new Comparator<Hero>() {
   public int compare(Hero hero1, Hero hero2) {
       return hero1.getName().compareToIgnoreCase(hero2.getName());
   }
});

// Java 8
heroes.sort(Comparator.comparing(Hero::getName));

{% endhighlight %}

### Listing hidden files

{% highlight java %}

// Old
File[] hiddenFiles = new File(".").listFiles(new FileFilter() {
    @Override
    public boolean accept(File file) {
        return file.isHidden();
    }
});

// Java 8
hiddenFiles = new File(".").listFiles(File::isHidden);

{% endhighlight %}

### Passing Methods

{% highlight java %}
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


// Using lambda

List<Hero> strengthHeroes = filterHeroes(heroes, (Hero h) -> Attribute.STRENGTH.equals(h.getAttribute()));

List<Hero> agilityHeroes = filterHeroes(heroes, (Hero h) -> Attribute.AGILITY.equals(h.getAttribute()));

List<Hero> intHeroes = filterHeroes(heroes, (Hero h) -> Attribute.INTELLIGENCE.equals(h.getAttribute()));
...

{% endhighlight %}

### Grouping and filtering

{% highlight java %}

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

{% endhighlight v%}