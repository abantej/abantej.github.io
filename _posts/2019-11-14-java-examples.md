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