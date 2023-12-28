---
title: "Fall '23: Semester Retrospective"
date: 2023-12-28T10:31:41-06:00
draft: false
---

This semester was a lot of fun for me. I am going to go through some of the highlights and lowlights of this last semester in anticipation of the upcoming semester. I also completed all the requirements for my Bachelors in Computer Science, so from here on out all my coursework will be towards completing my second degree in Computational Math.

## CS5030: High Performance Computing
### Taught by Dr. Steve Patruzza

This class was a blast and goes head first into high performance computing and the best practices when utilizing a computing cluster. When I signed up for this class, I assumed it would be more of a topics class where we approach the topic at a high level, but it ended up being very in-depth and hands on. My favorite part of the class was the allocation our class was given on the University of Utah's high performance computing cluster. This let us get first hand experience with the toolchains we were learning about in class.

**Things I learned & topics discussed**
 - `POSIX` threads/`C-threads`
    - We had to implement a histogram program that
    utilized parallel threads to calculate the histogram
 - `OpenMP`
    - We had several projects that utilized `OpenMP`. I found
    this to be a highlight of the course. It blows my mind
    the easiest multithreading library I have run into utilizes
    `C` and not something more modern like `Java` or `Rust`.
    - We had to reimplement the histogram program using `OpenMP`,
    which showed just convenient `OpenMP` is versus traditional
    `POSIX` threads.
 - `MPI`: Message Passing Interface
    - We did the histogram thing again but with `MPI`. Bleh.
    - `MPI` is my personal hell, but I also love `MPI`. I shed tears
    while trying to complete the homework and final project utilizing
    this paradigm, but the end result was amazing to see. When I was
    finally able to get the code compiled and running on a cluster,
    the gains in performance were unmatched (given the right
    circumstances)
 - `CUDA`
    - This is where things got really interesting. I have always wondered
    exactly how getting code to run on the GPU works, and this portion of
    the class gave me a taste of how that works. 
    - We had a few assignments surrounding GPU programming that demonstrated
    the basics alongside the benefits of adjusting `block` and `tile` sizes
    to better fit the problem.
 - `CUDA + MPI`
    - Putting the things together is easier than expected, besides the build
    stage. My mistake was never really automating the build stage, but I am
    now very familiar with the deployment stage of building an MPI + CUDA
    program.
 - Approaches to parallelism
    - We talked a lot about when you _should_ use parallelism and what a
    problem that can benefit from parallelism looks like. 
 - Analyzing parallel performance
    - A significant portion of the class discussed how to measure the
    performance of a parallel program, including measuring weak vs. strong
    scaling, wall time vs cpu time, and profiling tools that are commonly
    used to evaluate the performance of a parallel program.

**THE Final Project**

The final project for this class is awesome. I was in a group of 3 for the
project. And we ended up creating a program that, given a dataset representing
elevation of terrain, creates a line-of-sight map from every point to every
other point. Basically, "if I stood here, what could I see?". We used this
problem as an opportunity to create multiple implementations:

 - `Serial`
 - `OpenMP`
 - `MPI`
 - `CUDA`
 - `MPI + CUDA`


*Check out my groups submission [here](https://github.com/Drew-Watson-117/HPC_Project)*

## CS5600: Intelligence Systems
### Taught by Dr. Vladimir Kulyukin

I **loved** this class. An AI class is a cornerstone of a computer science
degree, and this class did not disappoint at all. Dr. Kulyukin is a master
lecturer and he never failed to provide an interesting and engaging lecture.
We often discussed questions of morality, and 
frequently addressed the vagueness and work that still needs to be 
done in this field. AI is in a weird -*unsustainable*- place right now,
beyond the politics of companies like OpenAI, we have reached diminishing
returns with scaling the current AI technologies that exist, so it was
fascinating to dive into the history of the field and get a better 
understanding of how we got to where we are today.

**Things I Learned & Topics Discussed**
 - Fundamentals of Artificial Intelligence
    - The axioms of AI, perceptrons, activation functions, etc
    - We had to implement a basic shallow neural network from scratch in
    python by building our own perceptron class and connecting perceptrons
    together to resolve logical statements.
 - Neural Networks
    - We went into a lot of details surrounding `NN`s, read several papers
    that are foundational to `NN`s, and used many popular `NN` libraries
    including `PyTorch` and `TensorFlow`
 - Convolutional Neural Networks
    - We experimented with an implementation of a `ConvNet` to perform
    computer vision.
 - Long Short Term Memory Models
 - Symbolic AI
    - My favorite part of this section of the course was learning about 
    `ELIZA`, a foundational element to modern chat-AIs like `chatGPT`.
 - Automatic Theorem Proving
    - I was not smart enough for most of the content in this section and
    found the syntax very mind boggling. I made myself look stupid *several*
    times in this unit of the course.

**Class Projects**

This class was comprised of two projects. The first project involved using 
several different NN models to predict behavior of a bee 
([Dr. Kulyukin's research](https://www.seattletimes.com/nation-world/utah-professor-hopes-robotic-hives-will-help-honeybees/) 
primarily focuses on bees :) ), alongside using computer vision to determine the
presence or lack of presence of a bee in an image. My results were sub-par, but
within line for the scope of the project.

The second project was self directed and only required the project pertain to
the topics of the course. Some of my classmates ran with this project and
created chess bots and other cool applications of `NN`s, but I decided to go
the symbolic AI route and implemented a lot of new rules for `ELIZA` that 
transformed the chat bot from a therapist into a technical support agent
for Fedora Linux.

_My final project for this class can be downloaded from [my GitHub](https://github.com/chandlerj/cs5600-finalproj)_

## MATH4610: Fundamentals of Numerical Methods
### Taught by Dr. Joe Koebbe

This class was very underwhelming. Dr. Koebbe was unsure what direction 
he wanted to take the class in, so the material we did cover was lackluster.
We would often start class 15 minutes late and then end class 10 minutes early.
The lazy side of me was fine with this, but the other side of me that wanted
to be able to say I was a mathematician without feeling like a poser was upset.
The only reason I took this class was because it is required for the 
Computational Math emphasis, and Dr. Koebbe is currently the only professor
facilitating classes specific to that emphasis. The textbook for this class
was the disorganized [GitHub repository](https://github.com/jvkoebbe/math4610) 
provided by Dr. Koebbe.

*[Here](https://github.com/chandlerj/math4610) is my own disorganized repository for this class, which includes
solutions to homework sets alongside lecture notes*

**Things I Learned & Topics Discussed**
 - Limits of representation using a computer
    - IE, the Maceps value of a floating point representation
 - Calculating various norms algorithmically
 - Approximating derivatives using numerical methods
 - Approximating solutions to a linear equation using numerical methods
 - Approximating eigenvalues and eigenvalues of a system of equations
 - Approximating solutions to systems of equations by utilizing numerical methods
 - Determining critical points and inflection points utilizing numerical methods
 - How little work it takes to be a tenured instructor at a state school.

## MATH2210: Multivariable Calculus
### Taught by Dr. Justin Heavilin

I am going to spare a lot of the details for this class as Calc III is 
pretty universal material for all STEM students. The textbook we used
was the garbage [Openstax Calc III](https://openstax.org/details/books/calculus-volume-3) textbook. I do appreciate that this textbook is free; however,
you get what you pay for. As far as lectures go, at first I absolutely hated
Dr. Heavilin's lecturing style, but as time went on I began to appreciate
why he chooses to do things the way he does. Anyone who has taken a class
From Dr. Heavilin will agree the material he presents in class does not
always line up with the homework material, but I think for a class like 
Calculus III, that is okay. I think Calc III should be a class where the 
student really starts to grasp the why behind mathematics and I think 
Dr. Heavilin does an excellent job presenting compelling questions. He is
also the first professor I have had break the facade that instructors just
know everything, and I really appreciate the humanity he presents. Sometimes
the comments he made were questionable, but I think being questionable is a 
prerequisite for being a faculty member of Utah State's Math/Stats Department.

While this class might be intended to be taken before other 2XXX math classes,
I am happy I took this class after taking Linear Algebra, ODEs, Discrete, etc
as I do not think I would have fully appreciated the content of this course
before this semester. While many people claim this class is light work and
trivial, I found it to be one of the most challenging math classes I have taken.

## Closing Thoughts

I would consider Fall 2023 to be one of the most successful semesters I have 
had in my college career. I passed all my classes with As and Bs, and I
feel like I engaged with the material better than I would normally. Additionally,
in my personal life I found more fulfillment as I was enjoying the time I spent
being productive. I think this was the semester where I began to understand the
work I will need to put in for a successful career.
