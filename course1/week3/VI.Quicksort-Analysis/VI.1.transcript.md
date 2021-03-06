## Quick Sort - Analysis I: A Decomposition Principle


>So this is the first video of three in which we'll mathematically analyze the running time of the randomized implementation of quick sort. So in particular we're going to prove that the average running time of quick sort is big O of n log n. Now this is the first randomized algorithm that we've seen in the course and therefore in its analysis will be the first time that we're going to need any kind of probability theory. 

1. 通过三个视频用数学方法分析quicksort的随机实现的运行时间。
2. 将证明quicksort的平均运行时间是 $O(nlogn)$ , 
3. randomized algorithm（随机算法）需要probability theory（概率论）。

> So let me just explain upfront what I'm going to expect you to know. In the following analysis. Basically, I need you to know the first few ingredients of discrete probability theory. So I need you to know about sample spaces, that is how to model all of the different things that could happen, all of the ways that random choices could resolve themselves. I need you to know about random variables, functions on sample spaces, which take on real values.  I need you to know about expectations that is average values of random variables and very simple but very key propriety we're going to need in the analysis of quick sort is linearity of expectation. 


1. 需要 discrete probability theory 知识。

2. **Sample Spaces**： 样本空间

3. **Random Variable:** 随机变量

4. **Expection:** 期望值， 即 随机变量的平均值

5. 分析quicksort很重要的方法是linearity of expection (线性期望值)

   ​


> So if you haven't seen this before or if you're too rusty definitely you should review this stuff before you watch this video. Some places you can go to get that necessary review you can look at the probability review part one video.  That's up on the course's website. If you'd prefer to read something, like I said at the beginning of the course, I recommend the free online lecture notes by Eric Lehman and Tom Leighton, Mathematics for Computer Science.  That covers everything we'll need to know, plus much, much more. There's also a Wikibook on Discrete Probability, which is a perfectly fine, obviously, free source in which you can learn the necessary material. Okay?

参考书：
[Mathematics for Computer Science - Mit](https://www.google.com.sg/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=2ahUKEwix-6HE667aAhUN2o8KHZbpB8cQFjAAegQIARAs&url=https%3A%2F%2Fcourses.csail.mit.edu%2F6.042%2Fspring17%2Fmcs.pdf&usg=AOvVaw1RiTrJyH7GVa35u6_R_bjo)  该书在不断更新(2017/06/05, PDF, 12.8MB)
[High School Mathematics Extensions/Discrete Probability](https://en.wikibooks.org/wiki/High_School_Mathematics_Extensions/Discrete_Probability)
_Introduction to Algorithms, 3rd Appendix C, Couning and Probability_  (heefan推荐)



> So after you've got that sort of fresh in your mind, then you're ready to watch the rest of this video. And in particular, we're ready to prove the following theorems stated in the previous video.
>
> So the quick sort algorithm with a randomized implementation, that is we're in every single recursive subcall, you pick a pivot uniformly at random. We stated the following assertion. But for every single input, so for a worst case input array of length n, the average running time of QuickSort with random pivots is $O(n log n)$. And again, to be clear where the randomness is, the randomness is not in the data. We make no assumptions about the data. 

1. 使用随机实现方法的quicksort，就是在每个单独的递归调用中，都随机的选择pivot.

2. 对于一个输入，最差情况下，$n$长度的数组使用随机选择的pivot的平均运行时间是$O nlogn$ 

3. 注意，随机指的是pivot，而不是输入的数据。 对输入的数据是没有要求的。

   ​

> As per our guiding principles. No matter what the input array is, averaging only over the randomness in our own code, the randomness internal to our algorithm. We get a running time of $n log n$. We saw in the past that the best case behavior of QuickSort is $n log n$. Its worst case behavior is $n^2$. So this theorem is asserting that no matter what the input array is, the typical behavior of QuickSort is far closer to the best case behavior than it is to the worst case behavior. Okay. So that's what we're going to prove in the next few videos. So let's go ahead and get started. 

1. 无论输入的array的size如何，平均复杂度是 $nlogn$, 最好情况是 $nlogn$, 最坏情况是 $n^2$

   ​
>So first I'm going to set up the necessary notation and be clear about what exactly is the sample space, what is the random variable that we care about, and so on. So we're going to fix an arbitrary array of length N. That's going to be the input to the quick sort algorithm. [SOUND]. And we'll be working with this fixed but arbitrary input array for the remainder of the analysis. Okay.

* remainder : 余数

  ​

> So just fix a single input in your mind. Now, what's the relevant sample space? Well, recall what a sample space is. It's just all the possible outcomes of the randomness in the world. So it's all the distinct things that could happen. Now here, the randomness is of our own devising. It's just the random pivot sequences, the random pivots chosen by QuickSort. So $\Omega$ （Omega）is just the set of all possible random pivots the QuickSort could choose. Now the whole point of this theorem proving that the average running time of quick sort is small boils down to computing the expectation of a single random variable. 

1. **sample space:** 所有可能的结果，且给个结果都是不同的。
2. 本例中，pivot的选择是随机的。所以 $\Omega$ 是所有可能的随机的pivot的集合。 
3. 问题转化为证明一份随机变量的期望值。



> So here's the random variable we're going to care about. For a given pivot sequence remember that random variables are real value functions. Defined on the sample space. So for a given point in the sample space or pivot sequence $\Sigma$ (Sigma), we're going to define C of sigma as the number of comparisons that quick sort makes. Where by comparison, I don't mean something like with an array index in a for-loop. That's not what I mean by comparison. I mean a comparison between two different entries of the input array, by comparing the third entry in the array against the seventh entry in the array, to see whether the third entry or the seventh entry is smaller. Notice that this is indeed a random variable that is given knowledge of the pivot sequence $\Sigma$ (Sigma), the choices of all pivots. 

1. 随机变量：给定的pivot序列是实数函数，定义在样本空间。
2. 定义quicksort比较的次数
3. “比较”：在输入的array中项的两两比较。
4. "random varialbes"： pivot sequence的 $\sigma$, 也就是所有pivots的选择。
5. $(\sigma)$ = quicksort的两个输入的元素 



> You can think of quick sort at that point as just a deterministic algorithm with all of the pivot choices pre-determined, and so a deterministic version of QuickSort make some deterministic member of comparisons so for giving pivot sequence $\Sigma$, we're just calling C of sigma to be however many comparisons it makes given those choices of pivots. Now with the theorem I stated is not about the number of comparisons of QuickSort but rather about the running time of QuickSort, but really to think about it kind of the only real work that the QuickSort algorithm does, is make comparisons between pairs of elements in the input array.

1. 由于pivot是预先决定的，你可以认为quicksort是一个确定性的算法。
2. 确定性的quicksort使得？？
3. ​




> The axis is a little bit of other book keeping but that's all noise that second over stuff. All QuickSort really does is compare between pairs of elements in the input array. And if you want to know what I mean by that a little more formally, dominated by comparisons, I mean that there exists a constant C so that the total number of operations of any type that QuickSort executes is at most a constant factor larger than the number of comparisons. So lets say that by RT, I mean the number of primitive operations of any form, that QuickSort uses. And for every previd sequence, sigma, the total number of operations, is no more than a constant times the total number of comparisons. And if you want a proof of this it's not that interesting so I'm not going to talk about it here. But in the notes posted on the website there is a sketch of why this is true. How you can formally argue

that there isn't much work beyond just the comparisons. But I hope most of you find that to be pretty intuitive. So given this, given that the running time that QuickSort boils down just to the number of comparisons. We want to prove the running time is n log n. All we gotta do, quote unquote, all we
have to do this proves that the average number of comparisons the QuickSort mix is all nlogn. And that's what we're going to do. That's what the rest of
these lecture is all about. So that's what we got to prove. 



We got to prove the expectation of
this random variable C which counts up the number of comparisons QuickSort mix is
for arbitrary input array of link n bound by big O of nlogn So the high order bit of this lecture
is a decomposition principle. We've identified this random variable,
C, the number of comparisons and it's exactly what we care about. It governs the average
running time of QuickSort. The problem is, it's quite complicated. It's very hard to understand
what this capital C is, it's fluctuating between nlogn and
then squared. And it's hard to know how
to get a handle on it. So how are we going to go about proving
this assertion, that the expectant number of comparisons that QuickSort makes,
is on average just O of nlogn. At this point we've actually have a fair
amount of experience with divide and conquer algorithms. You've seen a number of examples. And whenever we had to do a running
time analysis of such an algorithm we'd write out a recurrence we applied the
master method or in the worst case we'd run our recursion tree to figure out
the solution at our recurrence so you'd be very right to expect
something similar to happen here. But as we probe deeper and
we think about QuickSort we quickly realized that the master
method just doesn't apply, or at least not in the form that we're
used to, the problem is two fold. So first of all the size of the two
sub-problems is random, right? As we discuss in the last video,
the quality of the pivot is what determines how balanced the split
we get into the two sub-problems. It could be as bad as a sub-problem
of size 0 and one of size N minus 1. Or it could be as good as a perfectly
balanced split into two sub problems of equal sizes but we don't know. It's going to depend on
the random choice of the pivot. Moreover the master method at
least as we discussed it required solved subproblems to
have the same size and unless you're extremely lucky
that's not going to happen. In the QuickSort algorithm. It is possible to develop a theory
of recurrence relations for randomized algorithms and
apply that to QuickSort in particular. But I'm not going to go that route for
two reasons. The first one is't really quite messy. It get's pretty technical to talk
about solutions to recurrences for randomized algorithms. Or to thing about random recursion trees,
both of those get pretty complicated. The second reason is, I really want to introduce you to what
I call a decomposition principle. By which you take a random
variable that's complicated, but that you care about a lot. You decompose it into
simple random variables, which you don't really care about in their
own right, though it's easy analyze. And then you stitch those two things
together using linearity and expectation. So that's going to be the workhorse for
our analysis of the QuickSort algorithm. And it's going to come up again a couple
times in the rest of the course, for example, when we study hashing. So to explain how this decomposition
principle applies to QuickSort in particular. I'm going to need to introduce to you the
building blocks, simple random variables. Which will make up the complicated
random variable that we care about, the number of comparisons. Here's some notation. Recall that we fixed in the background
an arbitrary array of length n and that's denoted by capital A. And some notation which is simple but
also quite important. By z sub i,
what I mean is the ith smallest element in the input array capital A,
also know as the ith order statistic. So let me tell you what zi is not. What zi is not, in general, is the element in the ith position
of the input unsorted array. What zi is, is it's the element
which is going to wind up in the ith element of the array, once we sort it. Okay, so if you fast forward to the end
of a sorting algorithm and position i, you're going to find zi. So, let me give you an example. So suppose we had just
a simple array here, unsorted with the numbers 6, 8, 10 and 2. Then z1, well that's the first smallest,
the one smallest, or just the minimum. So z1 would be the 2, z2 would be the 6,
z3 would the the 8 and z4 would be the 10, for
this particular input array. Okay, so
zi is just the ith smallest number. Whatever it may lie on the original
unsorted array, that's what zi refers to. So we already defined the sample space. That's just all possible choices of
pivots the QuickSort might make. I already described one random variable, the number of comparisons that QuickSort
makes on a particular choice of pivots. Now I'm going to introduce a family
of much simpler random variables. Which count merely the comparisons
involving a given pair of elements in the input array,
not all elements, just a given pair. So for a given a choice of pivots,
a given sigma, and for given choices of inj,
both of which are between 1 and n. And so we only count things once, so I'm going to insist the i
is less than j always. And now here's a definition, my xij and
this is a random variable, so it's a function of the pivots chosen. This is going to be the number
of times that zi and zj are compared in
the execution of QuickSort. Okay, so this is going to be
an important definition in our analysis. It's important you understand it. So, for something like the third smallest
element and the seventh smallest element. xij is asking, that's when i equals 3 and
j equals 7, x37 is asking how many times those two elements
get compared as QuickSort proceeds. And this is a random variable in
the sense that if the pivot choices are all predetermined, if we think
of those being chosen in advance. Then there's just some fixed
deterministic number of times that zi and zj get compared. So it's important you understand
these random variables xij, so the next quiz is going to ask a basic
question about the range of values that a given xij can take on. So for this quiz we're considering
as usual some fixed input array. And now furthermore fixed to specific
elements of the input array. For example, the third smallest element, wherever it may lie, and the seventh
smallest element, wherever it may lie. Think about just these
pair of two elements. What is the range of values that
the corresponding random variable xij can take on? That is what are the different number of
times that a given pair of elements might be conceivably get compared in
the execution of the QuickSort algorithm? All right, so the correct answer
to this quiz is the second option. This is not a trivial quiz. This is a little tricky to see. So the assertion is that
a given pair of elements, they might not be compared at all. They might be compared once and they're
not going to get compared more than once. So here what I'm going to discuss
is why it's not possible for a given pair of elements to be compared
twice during the execution of QuickSort. It'll be clear later on, if it's not
already clear now, that both 0 and 1 are legitimate possibilities. A pair of elements might never get
compared and they might get compared once. And again, we'll go into more
detail on that in the next video. But why is it impossible
to be compared twice? Well think about two elements, say
the third element and the seventh element. And let's recall how
the partition subroutine works. Observe that in QuickSort,
the only place in the code where comparisons between pairs
of input array elements happens. It only happens in
the partition subroutine, so that's where we have to drill down. So what are the comparisons that get
made in the partition subroutine? Well, go back and look at that code. The pivot element is compared
to each other element in the input array exactly once. So the pivot just hangs up in
the first entry of the array. We have this for loop, this index j which
marches over the rest of the array. And for each value of j, the jth element of the input
array gets compared to the pivot. So summarizing,
in an invocation of partition, every single comparison
involves the pivot element. So two elements get compared if and
only if one is the pivot. All right so
let's go back to the question. Why can't a given pair of elements of
the input array get compared two or more times? Well, think about the first time
they ever get compared in QuickSort. It must be the case, that at that
moment we're in a recursive call where either one of those
two is the pivot element. So if it's the third smallest element or
the seventh smallest element. The first time those two elements
are compared to each other, either the third smallest or the seventh
smallest is currently the pivot. Because all comparisons
involve a pivot element. Therefore, what's going to
happen in the recursion, well the pivot is excluded
from both recursive calls. So, for example, if the seventh smallest
element is currently the pivot, that's not going to be passed on the recursive call
which contains the third smallest element. Therefore if you're compared once,
one of the elements is the pivot and they'll never be compared again, because the pivot will not even show
up in any future recursive calls. So let me just remind
you of some terminology. So a random variable which can
only take on the values 0 or 1 is often called
an indicator random variable, because it's just indicating whether or
not a certain things happens. So, in that terminology, each xij is indicating whether or not the ith
smallest element in the array and the jth smallest element in
the array ever get compared. It can't happen more than once,
it may or may not happen, and xij is 1 precisely when it happens. So that's the event that it's indicating. Having defined the building blocks I need,
these indicator random variables, these xij's. Now I can introduce you to
the decomposition principle as applied to QuickSort. So there's a random variable
that we really care about, which is denoted capital C, the number
of comparisons the QuickSort makes. That's really hard to get a handle on,
in and of itself, but we can express C as the sum of indicator
random variables, of these xijs. And those we don't care about
in their own right, but they're going to be much
easier to understand. So let me just rewrite the definitions of
C in the xij, so we're all clear on them. So c, recall, counts all of
the comparisons between pairs of input elements that QuickSort makes,
whereas an xij only counts the number. And it's going to be 0 or 1, comparisons
that involve the ith smallest and the jth smallest elements in particular. Now, since every comparison involves
precisely one pair of elements, some i and some j with i less than j,
we can write c as the sum of the xijs. So don't get intimidated
by this fancy double sum. All this is doing is it's iterating
over all of the ordered pairs, so all of the pairs ij, where i and
j are both between 1 and n and where i is strictly less than n. This double sum is just a convenient
way to do that iteration. And of course, no matter what the pivots
chosen are, we have this equality, okay? The comparisons are somehow split up
amongst the various pairs of elements, the various is and js. Why is it useful to express a complicated
random variable as a sum of simple random variables? Well, because an equation like this
is now right in the wheelhouse of linearity of expectation, so
let's just go ahead and apply that. Remember, and this is super, super
important, linearity of expectation says that the expectation of a sum
equals the sum of the expectations. And moreover, this is true whether or not the random variables are independent,
okay? And I'm not going to prove it here, but
you might want to think about the fact that the xijs are not,
in fact, independent. So we're using the fact that
linear expectation works even for non-independent random variables. Again, why is this interesting? Well, the left hand side,
This is complicated, right? This is some crazy number of comparisons
by some algorithm on some arbitrarily long array. And it fluctuates between two pretty far
apart numbers n log n and n squared. On the other hand,
this does not seem as intimidating. Given xij, it's just 0 or 1, whether or
not these two guys get compared or not. So that is the power of this
decomposition approach, okay? So, it reduces understanding
a complicated random variable to understanding simple random variables. In fact, because these
are indicator random variables, we can even clean up this
expression some more. So for any given xij being a 0, 1 random
variable, if we expand the definition of expectation, just as an average
over the various values, what is it? Well, it's some probability it takes
on the value 0, that's possible, and then some possibility it
takes on the value 1. And of course, this 0 part,
we can very satisfyingly delete, cancel. And so, the expected value of a given xij is just the probability that xij = 1. And remember,
it's an indicator random variable. It's 1 precisely when the ith smallest and
the jth smallest elements get compared. So putting it all together,
we find that what we care about. The average value of the number of
comparisons made by QuickSort on this input array is this double sum,
which literates over all ordered pairs, where each sum and is the probability
that the corresponding xij = 1. That is the probability that zi and zj get compared. And this is essentially the stopping
point for this video for the first part of the analysis, so let's call this
star and put a nice circle around it. So what's going to happen next is that
in the second video for the analysis, we're going to drill
down on this probability, probability that a given pair of elements
gets compared, and we're going to nail it. We're going to give an exact
expression as a function of i and j for exactly what this probability is. Then in the third video,
we're going to take that exact expression, plug it into the sum, and
then evaluate this sum. And it turns out the sum will
evaluate to O of n log n. So that's the plan. That's how you'll apply
decomposition in terms of 0, 1 or indicator random variables,
apply linearity of expectation. In the next video, we'll understand
these simple random variables, and then we'll wrap up in the third video. Before we move on to the next part of
the analysis, I do just want to emphasize that this decomposition principle is
relevant not only for QuickSort, but it's relevant for the analysis of
lots of randomized algorithms. And we will see more applications, at least one more application,
later in the course. So just to kind of really
hammer the point home, let me spell out the key steps for
the general decomposition principle. So first you need to figure
out what is it you care about. So in QuickSort,
we cared about the number of comparisons. We had this lemma that said the running
time is dominated by comparisons. So we understood what we wanted to know,
the average value for the number of comparisons. The second step is to express this random
variable y as a sum of simple random variables, ideally indicator or
0, 1 random variables. Now you're in the wheel house
of linearity of expectation, you just apply it, and
you find that what it is you care about, the average value of
the random variable y is just the sum of the probabilities
of various events. That given xl,
random variable is equal to 1. And so the upshot is to understand the
seemingly very complicated left-hand side, all you have to do is understand
something, which in many cases, is much simpler, which is understand
the probability of these various events. In the next video, I'll show you exactly
how that's done in the case of QuickSort, where we care about the xijs, the probability that two
elements gets compared. So let's move on and
get exact expression for that probability.