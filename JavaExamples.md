## Java Codewars Kata Solutions

- [x] **6 Kyu - Your order, please** 

### *Details: * 

Your task is to sort a given string. Each word in the string will contain a single number. This number is the position the word should have in the result.

Note: Numbers can be from 1 to 9. So 1 will be the first word (not 0).

If the input string is empty, return an empty string. The words in the input String will only contain valid consecutive numbers.

### *Solution: *

```
  import java.util.*;

  public class Order {


    public static String order(String words) {

      if(words == "") return "";

      String[] wordList = words.split(" ");
      String[] result = new String[wordList.length];

      Arrays.stream(wordList).forEach(s -> {

        int position;

        for(String c : s.split("")) {

         if (c.matches("[0-9]")) {

           position = Integer.parseInt(c);
           result[position - 1] = s;
           break;

         }

        }

      });

      return String.join(" ",result);
    }
  }
  
```

- [x] **7 Kyu - Alternate capitalization** 

### *Details: * 

Given a string, capitalize the letters that occupy even indexes and odd indexes separately, and return as shown below. Index 0 will be considered even.

For example, capitalize("abcdef") = ['AbCdEf', 'aBcDeF']. See test cases for more examples.

The input will be a lowercase string with no spaces.

Good luck!

### *Solution: *

```
  class Solution{
    public static String[] capitalize(String s){
        
      String[] sList = s.split("");
      
      String[] result = new String[] {"",""};
      
      for(int i = 0; i < sList.length; i++) {
        
        if(i % 2 == 0) {
          
          result[0] = result[0] + sList[i].toUpperCase();
          result[1] = result[1] + sList[i];
          
        } else {
          
          result[0] = result[0] + sList[i];
          result[1] = result[1] + sList[i].toUpperCase();
          
        }
        
      }
      
      return result;
    }
}
  
```

- [x] **6 Kyu - Sort the odd** 

### *Details: * 

You will be given an array of numbers. You have to sort the odd numbers in ascending order while leaving the even numbers at their original positions.

### *Solution: *

```
  import java.util.*;
  import java.util.stream.*;

  public class Kata {
    public static int[] sortArray(int[] array) {

      int[] oddListSorted = IntStream.of(array)
        .filter(e -> e % 2 != 0)
        .sorted()
        .toArray();

      int oddPosition = 0;

      for(int i = 0; i < array.length; i++) {

        if(array[i] % 2 == 0 ) continue;

        array[i] = oddListSorted[oddPosition];
        oddPosition++;

      }
      
      return array;
      
    }
  }

```

- [x] **7 Kyu - Money, Money, Money** 

### *Details: * 

Mr. Scrooge has a sum of money 'P' that he wants to invest. Before he does, he wants to know how many years 'Y' this sum 'P' has to be kept in the bank in order for it to amount to a desired sum of money 'D'.

The sum is kept for 'Y' years in the bank where interest 'I' is paid yearly. After paying taxes 'T' for the year the new sum is re-invested.

Note to Tax: not the invested principal is taxed, but only the year's accrued interest

### *Solution: *

```
  public class Money {
  public static int calculateYears(double principal, double interest,  double tax, double desired) {
    
    if(desired <= principal) return 0;
    
    int years = 0;
      
    while(principal <= desired) {
      
      principal += (principal * interest) * (1 - tax);
      years++;
      
    }
    
    return years;
  }
}

```

- [x] **7 Kyu - Factorial** 

### *Details: * 

In mathematics, the factorial of a non-negative integer n, denoted by n!, is the product of all positive integers less than or equal to n. For example: 5! = 5 * 4 * 3 * 2 * 1 = 120. By convention the value of 0! is 1.

Write a function to calculate factorial for a given input. If input is below 0 or above 12 throw an exception of type ArgumentOutOfRangeException (C#) or IllegalArgumentException (Java) or RangeException (PHP) or throw a RangeError (JavaScript) or ValueError (Python) or return -1 (C).

### *Solution: *

```
  public class Factorial {

  public int factorial(int n) {
    
    if(n < 0 || n > 12) throw new IllegalArgumentException("n must be greater than 0 and less than 12");
      
    if(n == 0) return 1;
    
    return n * factorial(n - 1);
  }
}

```

**More...**

