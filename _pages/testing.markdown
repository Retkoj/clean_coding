---
layout: page
title:  "Unit testing"
date:   2022-06-24 00:59:34 +0200
categories: jekyll update
---

Functie:

{% highlight python %}
def get_fibonacci_sequence(n_terms: int):
    """
    Returned de eerste [n_terms] getallen van de Fibonacci serie naar de terminal.

    :param n_terms: Het gewenste aantal getallen dat geprint moet worden
    """
    fibonacci_series = []
    current_number = 0
    next_number = 1
    count = 0
    while count < n_terms:
        fibonacci_series.append(current_number)
        next_sum = current_number + next_number
        current_number = next_number
        next_number = next_sum
        count += 1
    return fibonacci_series
{% endhighlight %}

Testcases:

{% highlight python %}
import unittest

from fibonacci import get_fibonacci_sequence


class TestFibonacci(unittest.TestCase):

    def test_fibonacci_length(self):
        """Assert the length of the output equals the number_of_terms input"""
        number_of_terms = 6
        self.assertEqual(len(get_fibonacci_sequence(number_of_terms)), number_of_terms,
                         f"Length should be {number_of_terms}")

    def test_fibonacci_output(self):
        """Assert that the correct sequence is outputted"""
        number_of_terms = 10
        expected_output = [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
        self.assertEqual(get_fibonacci_sequence(number_of_terms), expected_output,
                         f"{number_of_terms} terms should result in {expected_output}")

    def test_bad_type(self):
        """Assert a string input raises a TypeError"""
        number_of_terms = "banana"
        with self.assertRaises(TypeError):
            get_fibonacci_sequence(number_of_terms)


if __name__ == '__main__':
    unittest.main()

{% endhighlight %}