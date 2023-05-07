Download Link: https://assignmentchef.com/product/solved-math-551-lab-5
<br>
<strong>Goal: </strong>In this lab, we will consider the “best” way to solve a linear system of the form <strong>Ax </strong>= <strong>b</strong>. Of course, in order to understand what “best” means, we need some means of comparison. For this exercise, we will compare methods based on their <em>accuracy </em>and <em>efficiency</em>.

Accuracy becomes important when we realize that computers cannot possibly represent all real numbers. Instead, in numerical computations, operations on real numbers require rounding to some finite number of digits. The errors caused by rounding propagate through computations and give rise to errors in the output. A more accurate algorithm is one that has smaller output errors for a given set of input data.

Efficiency often refers to the time required for an algorithm to complete, or to the amount of system memory required for the algorithm to run. We’ll focus on the former. For us, a more efficient algorithm will be one that gives us the answer quicker.

In this lab, we will explore three different methods for solving a square linear system <strong>Ax </strong>= <strong>b </strong>in Matlab: the rref function, the inv function, and the backslash operator.

<strong>Getting started: </strong>Download the file m551lab05.m and load it into Matlab’s editor when instructed. Throughout this lab, you will make modifications to this file. You will need to turn in your modified version, so be sure to save your changes.

<strong>What you have to submit: </strong>Submit your modified version of the M-file through Canvas.

<h1>Reminders About the Grading Software</h1>

Remember, the labs are graded with the help of software tools. If you do not follow the instructions, you will lose points. If the instructions ask you to assign a value to a variable, you must <strong>use the variable name given in the instructions</strong>. If the instructions ask you to make a variable named x1 and instead you make a variable named x or X or X1 or any name other than x1, the grading software will not find your variable and you <em>will </em>lose points. Required variables are listed in the lab instructions in a gray box like this:

<h2>Variables: x1, A, q</h2>

At times you will also be asked to answer questions in a comment in your M-file. You must <strong>format your text answers correctly</strong>. Questions that you must answer are shown in gray boxes in the lab. For example, if you see the instruction

Q7: What does the Matlab command lu do? your file must contain a line similar to the following somewhere

% Q7: It computes the LU decomposition of a matrix.

The important points about the formatting are

<ul>

 <li>The answer is on a single line.</li>

 <li>The first characters on the line is the comment character %.</li>

 <li>The answer is labeled in the form Q<em>n</em>:, where <em>n </em>stands for the question number from the gray box.</li>

</ul>

If you do not format your answers correctly, the grading software will not find them and you <em>will </em>lose points.

<h1>Timing Computations in Matlab</h1>

<ol>

 <li>At the Matlab command prompt run the command tic, then wait a few seconds and run the command toc. You should see something like the example output below. Repeat a few times, pausing for different lengths of time between the two commands. What is happening?</li>

</ol>

&gt;&gt; tic

&gt;&gt; toc

Elapsed time is 3.065801 seconds.

<ol start="2">

 <li>Now load the file m into the Matlab editor, and find and run the section labeled “Timing Multiplications in Matlab”. (If you don’t know how to run a single section, look for an appropriate button in Matlab’s toolbar or ask your lab instructor for help.) Matlab’s output should now contain a table similar to this one.</li>

</ol>

|                  n | avg. time |

+——-+———–


|               10 | 1.077e-04 |

|               20 | 1.840e-05 |

|               40 | 8.951e-04 |

|            80 | 1.859e-04 | |              160 | 3.420e-04 |

Don’t worry about understanding all the code. It uses tic and toc to time how long it takes Matlab to multiply two random square matrices of various dimensions. The table column labeled n shows the dimension of the matrices (10 × 10, 20 × 20, and so on) and the avg. time column reports the length of time (in seconds) required to multiply two <em>n </em>× <em>n </em>matrices for this value of <em>n</em>. Unfortunately, these sizes are too small for us to get a good sense of how expensive matrix multiplication is. We’ll fix this in the next step.

<ol start="3">

 <li>Change the definition of mul n so that the table includes the <em>n </em>values 100, 200, 400, 800 and 1600.</li>

</ol>

(You’ll need to run the section again.)

<h2>Variables: mul n</h2>

<ol start="4">

 <li>Look at the bottom two rows of this table. When <em>n </em>is doubled from 800 to 1600, how is the computational time affected? Is the time doubled? Tripled? Multiplied by some other factor? (This method of assessing an algorithm’s behavior is not the best. You’ll probably get a different answer from your classmates, but it should give you a rough idea.)</li>

</ol>

Q1: How does the computational time change when <em>n </em>is doubled from 800 to 1600?

<strong>Methods for Solving Linear Systems </strong>Now let’s consider three different ways for solving <strong>Ax </strong>= <strong>b </strong>when

<strong>A </strong>      and     <strong>b </strong><em> .</em>

(The solution is <strong>x </strong>= [1 2 3]<em><sup>T</sup></em>.)

<ol>

 <li>In the M-file, locate the Matlab comments</li>

</ol>

%%

% Methods for Solving Linear Systems

% define A1 and b1 here

Directly below these lines, define a variable A1 holding the matrix <strong>A </strong>and a variable b1 holding the vector <strong>b</strong>.

<h2>Variables: A1, b1</h2>

<ol start="2">

 <li>This section of the M-file should now look like</li>

</ol>

%%

% Methods for Solving Linear Systems

% define A1 and b1 here A1 = … b1 = …

M1 = [ A1 b1 ]

S1 = rref(M1) x1_rref = S1(:,4)

Run the section and observe that the variable x1 rref is assigned the values from the last column of S1, which contains the computed solution <strong>x</strong>. Beneath this variable definition, define two other variables, x1 inv and x1 div. The first should hold the result of multiplying inv(A1) with b1 and the second should hold the result of A1b1. After running this section, check in the Matlab command window that all three solution variables agree.

<table width="159">

 <tbody>

  <tr>

   <td width="159">Variables: x1 inv, x1 div</td>

  </tr>

 </tbody>

</table>

<h1>Comparing the Methods</h1>

Now let’s compare the methods on a larger matrix. Select and run the section “Comparing the Methods” in the M-file. The output should look something like this:

| method |          time         |         error               | residual |

+——–+———-+———–+———–


| rref | 1.36167 | 9.581e-08 | 9.658e-15 |

| inv(A) |       not yet implemented                 | | Ab               |                  not yet implemented      |

Currently, only the solution method based on rref is implemented. The time column reports the time required to solve a moderately large (200 × 200) linear system. The next two columns report two measures of the error: the solution error and residual error. These two quantities are defined as follows.

Suppose the true solution to the system <strong>Ax </strong>= <strong>b </strong>is the vector <strong>x</strong><em><sub>t</sub></em>. When solving the system in Matlab, we typically won’t get the true solution due to the accumulation of roundoff errors. Instead, we’ll get an approximate solution <strong>x</strong><em><sub>a</sub></em>. One way to measure error is through the difference <strong>x</strong><em><sub>t </sub></em>− <strong>x</strong><em><sub>a</sub></em>, called the <em>solution error vector</em>.

The biggest problem with this measure of error is that we typically won’t know the true solution. In this exercise, the vector <strong>b </strong>was constructed so that the solution is known, but usually we won’t be looking for an answer we already know. If we don’t know the true solution, we can still try to understand the error through the <em>residual error vector</em>, <strong>r</strong>, defined as <strong>r </strong>= <strong>Ax</strong><em><sub>a </sub></em>−<strong>b</strong>. If <strong>x</strong><em><sub>a </sub></em>= <strong>x</strong><em><sub>t</sub></em>, the residual will be the zero vector. If <strong>x</strong><em><sub>a </sub></em>is a good approximation, we expect that <strong>r </strong>should have very small entries.

In either case, the error is a vector. In order to compare methods, we need a way to describe the sizes of these vectors. We’ll discuss methods for assigning size to vectors in more detail in later lectures on <em>vector norms</em>. For now, it is enough to know that the third and fourth columns of the Matlab table describe the sizes of the two error vectors described above. Larger values indicate more error.

<ol>

 <li>Locate the following code.</li>

</ol>

% solve with rref tic;

S = rref([A b]); x_rref=S(:,n+1); rref_time = toc;

This code computes the solution to the system using rref, and stores the result in x rref and the solution time in rref time. Create a similar block of code below this one that computes x inv using multiplication by inv(A) and store the computation time in the variable inv time. Run the section again and compare the top two table rows. If you have completed this step successfully, the inv-based method should be much faster than rref, have similar solution error, but larger residual by several orders of magnitude.

<table width="166">

 <tbody>

  <tr>

   <td width="166">Variables: x inv, inv time</td>

  </tr>

 </tbody>

</table>

<ol start="2">

 <li>Finally, make one more block of code which approximates the solution <strong>x </strong>using the backslash operator. Store the result in x div and the computation time in the variable div time.</li>

</ol>

<table width="166">

 <tbody>

  <tr>

   <td width="166">Variables: x div, div time</td>

  </tr>

 </tbody>

</table>

<ol start="3">

 <li>When you are finished, running the section should print a table comparing computing times and errors among all three methods.</li>

</ol>

<table width="405">

 <tbody>

  <tr>

   <td colspan="2" width="326">Q2: How do the methods compare in computing time?</td>

   <td rowspan="3" width="79"> </td>

  </tr>

  <tr>

   <td width="313">Q3: How do the methods compare in solution error?</td>

   <td rowspan="2" width="13"> </td>

  </tr>

  <tr>

   <td width="313">Q4: How do the methods compare in residual error?</td>

  </tr>

  <tr>

   <td colspan="3" width="405">Q5: Which method do you think is “best” for this system and why?</td>

  </tr>

 </tbody>

</table>


