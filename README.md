# Determining next number in a sequence

**Explanation on how it works:**

  First let me start by saying this isn't 100% exact by any means. There are many cases it cannot make determinations of, but it can generally find the sequence if the relationship between the numbers is via multiplication/division or subtraction/additive. If the relationship is a special case like pi for example, it cannot figure that out.

  It starts in the findSequence function and then goes through a loop to find something I called the divisibility score. If the divisibility score is greater than or equal to 1, we can safely assume that things are divisible across the board. This allows for a quick calculation. I then send the series of numbers to findGreatestDivisor to assume that we are multiplying by the largest divisor found in the series of numbers. [1,2,4,8,16,32] will have a greatest divisor of 2, for example. If everything goes well there, we take the divisor and send it back to findSequence, and then slice the last element in the series of numbers, grab it from the end via pop(), and multiply it by the divisor.

  If the divisibility score is not ideal, it will then head over to tryMultiplicative which uses *y = kx* to determine if there is a directly proportional number found to work off of (being *k*). We then check to see if the *k* is consistent across the board at the bottom (from y / x). If *k* is consistent across the board, we can take *k* and apply it to the next term in the series *(x)*. *f(x) = y* where x is the position in the array, and y is the value at the position. *k* is the function. If this does not work out, we use trackK to determine whether *k* isNaN OR if it evaluates to false via (k % 1 === 0). If it evaluates to false, we can assume that the likelihood of the pattern isn't found via divisibility or multiplication.

  If it is not found, we can then try to use a difference table to find if there is an additive relationship between the numbers. tryDifference is called and passed the series. Here we initialize a new array and set difference to seq.slice(0) which is the "rest" of the series. We enter a second loop to set out to find the next series of numbers that we can subtract from. The difference variable is then set to the difference between the first two integers in our series of numbers. Finally, to keep track of our next sequence, we push difference[j] to the bottomLevel array. Using .slice(0), eventually the sequence will be empty and the for loops will stop the subtraction. Using .reduce, I then take the result of my subtraction for each series, and add the last set in the series to make the determination. This assumes it is consistent across the board. Then you are returned your result.
