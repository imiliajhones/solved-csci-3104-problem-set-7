Download Link: https://assignmentchef.com/product/solved-csci-3104-problem-set-7
<br>
<ol>

 <li>(45 pts) Recall that the <em>string alignment problem </em>takes as input two strings <em>x </em>and <em>y</em>, composed of symbols <em>x<sub>i</sub>,y<sub>j </sub></em>∈ Σ, for a fixed symbol set Σ, and returns a minimal-cost set of <em>edit </em>operations for transforming the string <em>x </em>into string <em>y</em>.</li>

</ol>

Let <em>x </em>contain <em>n<sub>x </sub></em>symbols, let <em>y </em>contain <em>n<sub>y </sub></em>symbols, and let the set of edit operations be those defined in the lecture notes (substitution, insertion, deletion, and transposition).

Let the cost of <em>indel </em>be 1, the cost of <em>swap </em>be 13 (plus the cost of the two <em>sub </em>ops), and the cost of <em>sub </em>be 12, except when <em>x<sub>i </sub></em>= <em>y<sub>j</sub></em>, which is a “no-op” and has cost 0.

In this problem, we will implement and apply three functions.

<ul>

 <li>alignStrings(x,y) takes as input two ASCII strings <em>x </em>and <em>y</em>, and runs a dynamic programming algorithm to return the cost matrix <em>S</em>, which contains the optimal costs for all the subproblems for aligning these two strings.</li>

</ul>

alignStrings(x,y) :                                                     // x,y are ASCII strings

S = table of length nx by ny                       // for memoizing the subproblem costs

initialize S        // fill in the basecases for i = 1 to nx for j = 1 to ny

S[i,j] = cost(i,j)                              // optimal cost for x[0..i] and y[0..j]

}} return S

<ul>

 <li>extractAlignment(S,x,y) takes as input an optimal cost matrix <em>S</em>, strings <em>x,y</em>, and returns a vector <em>a </em>that represents an optimal sequence of edit operations to convert <em>x </em>into <em>y</em>. This optimal sequence is recovered by finding a path on the implicit DAG of decisions made by alignStrings to obtain the value <em>S</em>[<em>n<sub>x</sub>,n<sub>y</sub></em>], starting from <em>S</em>[0<em>,</em>0].</li>

</ul>

extractAlignment(S,x,y) : // S is an optimal cost matrix from alignStrings initialize a               // empty vector of edit operations [i,j] = [nx,ny] // initialize the search for a path to S[0,0] while i &gt; 0 or j &gt; 0 a[i] = determineOptimalOp(S,i,j,x,y) // what was an optimal choice?

[i,j] = updateIndices(S,i,j,a)                                     // move to next position

} return a

When storing the sequence of edit operations in <em>a</em>, use a special symbol to denote no-ops.

1

(iii) commonSubstrings(x,L,a) which takes as input the ASCII string <em>x</em>, an integer 1 ≤ <em>L </em>≤ <em>n<sub>x</sub></em>, and an optimal sequence <em>a </em>of edits to <em>x</em>, which would transform <em>x </em>into <em>y</em>. This function returns each of the substrings of length at least <em>L </em>in <em>x </em>that aligns exactly, via a run of no-ops, to a substring in <em>y</em>.

<ul>

 <li>From scratch, implement the functions alignStrings, extractAlignment, and commonSubstrings. You may not use any library functions that make their implementation trivial. Within your implementation of extractAlignment, ties must be broken uniformly at random.</li>

</ul>

Submit (i) a paragraph for each function that explains how you implemented it (describe how it works and how it uses its data structures), and (ii) your code implementation, with code comments.

Hint: test your code by reproducing the APE / STEP and the EXPONENTIAL / POLYNOMIAL examples in the lecture notes (to do this exactly, you’ll need to use unit costs instead of the ones given above).

<ul>

 <li>Using asymptotic analysis, determine the running time of the callcommonSubstrings(x, L, extractAlignment( alignStrings(x,y), x,y ) ) Justify your answer.</li>

 <li>(15 pts extra credit) Describe an algorithm for counting the number of optimalalignments, given an optimal cost matrix <em>S</em>. Prove that your algorithm is correct, and give is asymptotic running time.</li>

</ul>

Hint: Convert this problem into a form that allows us to apply an algorithm we’ve already seen.

<ul>

 <li>String alignment algorithms can be used to detect changes between different versions of the same document (as in version control systems) or to detect verbatim copying between different documents (as in plagiarism detection systems).</li>

</ul>

The two data string files for PS7 (see class Moodle) contain actual documents recently released by two independent organizations. Use your functions from (1a) to align the text of these two documents. Present the results of your analysis, including a reporting of all the substrings in <em>x </em>of length <em>L </em>= 9 or more that could have been taken from <em>y</em>, and briefly comment on whether these documents could be reasonably considered original works, under CU’s academic honesty policy.

<ol start="2">

 <li>(20 pts) Ron and Hermione are having a competition to see who can compute the <em>n</em>th Pell number <em>P<sub>n </sub></em>more quickly, without resorting to magic. Recall that the <em>n</em>th Pell number is defined as <em>P<sub>n </sub></em>= 2<em>P<sub>n</sub></em><sub>−1 </sub>+<em>P<sub>n</sub></em><sub>−2 </sub>for <em>n &gt; </em>1 with base cases <em>P</em><sub>0 </sub>= 0 and <em>P</em><sub>1 </sub>= 1.</li>

</ol>

Ron opens with the classic recursive algorithm:

Pell(n) :

if n == 0 { return 0 } else if n == 1 { return 1 } else { return 2*Pell(n-1) + Pell(n-2) } which he claims takes <em>R</em>(<em>n</em>) = <em>R</em>(<em>n </em>− 1) + <em>R</em>(<em>n </em>− 2) + <em>c </em>= <em>O</em>(<em>φ<sup>n</sup></em>) time.

(a) Hermione counters with a dynamic programming approach that “memoizes” (a.k.a. memorizes) the intermediate Pell numbers by storing them in an array P[n]. She claims this allows an algorithm to compute larger Pell numbers more quickly, and writes down the following algorithm.<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>

MemPell(n) {

if n == 0 { return 0 } else if n == 1 { return 1 } else { if (P[n] == undefined) { P[n] = 2*MemPell(n-1) + MemPell(n-2) } return P[n]

}

}

<ol>

 <li>Describe the behavior of MemPell(n) in terms of a traversal of a computation tree. Describe how the array P is filled.</li>

 <li>Determine the asymptotic running time of MemPell. Prove your claim is correct by induction on the contents of the array.</li>

</ol>

<ul>

 <li>Ron then claims that he can beat Hermione’s dynamic programming algorithmin both time and space with another dynamic programming algorithm, which eliminates the recursion completely and instead builds up directly to the final solution by filling the <em>P </em>array in order. Ron’s new algorithm<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a> is</li>

</ul>

DynPell(n) :

P[0] = 0,                P[1] = 1 for i = 2 to n { P[i] = 2*P[i-1] + P[i-2] } return P[n]

Determine the time and space usage of DynPell(n). Justify your answers and compare them to the answers in part (2a).

<ul>

 <li>With a gleam in her eye, Hermione tells Ron that she can do everything he cando better: she can compute the <em>n</em>th Pell number even faster because intermediate results do not need to be stored. Over Ron’s pathetic cries, Hermione says</li>

</ul>

FasterPell(n) :

a = 0, b = 1 for i = 2 to n c = 2*a + b a = b b = c

end return a

Ron giggles and says that Hermione has a bug in her algorithm. Determine the error, give its correction, and then determine the time and space usage of FasterPell(n). Justify your claims.

<ul>

 <li>In a table, list each of the four algorithms as columns and for each give its asymptotic time and space requirements, along with the implied or explicit data structures that each requires. Briefly discuss how these different approaches compare, and where the improvements come from. (Hint: what data structure do all recursive algorithms implicitly use?)</li>

 <li>(5 pts extra credit) Implement FasterPell and then compute <em>P<sub>n </sub></em>where <em>n </em>is the four-digit number representing your MMDD birthday, and report the first five digits of <em>P<sub>n</sub></em>. Now, assuming that it takes one nanosecond per operation, estimate the number of years required to compute <em>P<sub>n </sub></em>using Ron’s classic recursive algorithm and compare that to the clock time required to compute <em>P<sub>n </sub></em>using FasterPell.</li>

</ul>

<a href="#_ftnref1" name="_ftn1">[1]</a> Ron briefly whines about Hermione’s P[n]=undefined trick (“an unallocated array!”), but she point out that MemPell(n) can simply be wrapped within a second function that first allocates an array of size <em>n</em>, initializes each entry to undefined, and then calls MemPell(n) as given.

<a href="#_ftnref2" name="_ftn2">[2]</a> Ron is now using Hermione’s undefined array trick; assume he also uses her solution of wrapping this function within another that correctly allocates the array.