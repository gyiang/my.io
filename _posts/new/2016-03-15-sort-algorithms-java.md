---
layout: post
title: 排序算法实现（java）
category: 技术
tags: 算法
keywords: 算法,排序,Sort,Algorithm
---

排序算法是非常常见也非常基础的算法，以至于大部分情况下它们都被集成到了语言的辅助库中。排序算法虽然已经可以很方便的使用，但是理解排序算法可以帮助我们找到解题的方向。

## 1. 冒泡排序 (Bubble Sort)

{% highlight java %}
public void bubbleSort(int[] numbers) {
    boolean numbersSwitched;
    do {
        numbersSwitched=false;
        for(int i=0;i<numbers.length-1;i++) {
            if (numbers[i + 1] < numbers[i]) {
                int tmp=numbers[i+1];
                numbers[i + 1] = numbers[i];
                numbers[i] = tmp;
                numbersSwitched=true;
            }
        }
    }while(numbersSwitched);
}
{% endhighlight %}


## 2. 插入排序（Insertion Sort）

{% highlight java %}
public static List<Integer> insertSort(final List<Integer> numbers) {
    final List<Integer> sortedList = new LinkedList<Integer>();
    originaList:
    for (Integer number : numbers) {
        for(int i=0;i<sortedList.size();i++) {
            if (number < sortedList.get(i)){
                sortedList.add(i, number);
                continue originaList;
            }
        }
        sortedList.add(sortedList.size(),number);
    }
    return  sortedList;
}
{% endhighlight %}


## 3. 快速排序（Quick Sort）


{% highlight java %}
public static List<Integer> quickSort(List<Integer> numbers) {
    if (numbers.size() < 2) {
        return numbers;
    }
    final Integer pivot = numbers.get(0);
    final List<Integer> lower = new ArrayList<Integer>();
    final List<Integer> higher = new ArrayList<Integer>();

    for (int i = 0; i < numbers.size(); i++) {
        if (numbers.get(i) < pivot) {
            lower.add(numbers.get(i));
        } else {
            higher.add(numbers.get(i));
        }
    }
    final List<Integer> sorted=quickSort(lower);
    sorted.add(pivot);
    sorted.addAll(quickSort(higher));
    return sorted;
}
{% endhighlight %}


## 4. 归并排序（Merge Sort）

{% highlight java %}
public static List<Integer> mergesort(final List<Integer> values) {
    if (values.size() < 2) {
        return values;
    }

    final List<Integer> leftHalf=values.subList(0,values.size()/2);
    final List<Integer> rightHalf = values.subList(values.size() / 2, values.size());

    return merge(mergesort(leftHalf), mergesort(rightHalf));
}

private static List<Integer> merge(final List<Integer> left, final List<Integer> right) {
    int leftPtr=0;
    int rightPtr=0;

    final List<Integer> merged=new ArrayList<Integer>(left.size()+right.size());

    while (leftPtr < left.size() && rightPtr < right.size()) {
        if (left.get(leftPtr) < right.get(rightPtr)) {
            merged.add(left.get(leftPtr));
            leftPtr++;
        } else {
            merged.add(right.get(rightPtr));
            rightPtr++;
        }
    }

    while (leftPtr < left.size()) {
        merged.add(left.get(leftPtr));
        leftPtr++;
    }
    while (rightPtr < right.size()) {
        merged.add(right.get(rightPtr));
        rightPtr++;
    }

    return merged;
}
{% endhighlight %}