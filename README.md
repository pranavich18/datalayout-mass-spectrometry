## Space- and time-efficient data format for mass spectrometry data (OpenMS) GSOC'22

### Current State of Progress w.r.t. Project after the coding period
Currently I have 2 PRs for the project. 

1. SoA Datalayout [https://github.com/OpenMS/OpenMS/pull/6190]

First one was an attempt to implement normal Structure of Arrays for MSSpectrum without any zero-cost abstraction. It was successfully implemented for a few functions of MSSPectrum like `getBasePeak()` , along with iterators termed as `ProxyIterator`.
But the problem arose in the implementation of MSSpectrum in other classes in the OpenMS Codebase. In the implementation iterator was just an abstraction of index and the could not return a reference to a `Peak1D` object. Here it was a point where we got stuck with the first approach and also the non-const usage of AreaIterator also started throwing build errors at this point.

2. SoA Datalayout with Abstraction [https://github.com/OpenMS/OpenMS/pull/6267]

This time one of my mentors came with an idea to implement it with the abstraction template that we were planning to use before. Earlier the swap() function was a bottleneck for this but its implementation was changed using a custom swap for reference_wrappers.
This PR uses a zero-cost abstraction for a Structure of Array (SoA) data layout for `MSSpectrum`. In this implementation MSSpectrum uses the abstraction datalayout in the form of a `BaseContainer` which stores `Peak1D` as a tupleof values i.e. `Peak1DT<>` with almost all the functionalities of a vector<Peak> like, `insert()`, `empty()`, `erase`, `front`, `back`, `emplace_back`, `push_back`, `pop_back`, etc. all the ones which were being used in the original vector<Peak1D>.

The new data layout support proper iterators which return the reference to the Peak object.
For peaks we used a tuple of values(position and intensities). The new iterator solves the problem that we faced in the first approach. 

This implementation was successfully tested and build with some of the functions changed separately. Now the MSSpectrum inherits from the SoA that was created in the abstraction temoplate.
But due to the entanglement of MSSpectrum with a lot of classes , currently there are build errors getting thrown. Some of the other classes for eg: `AreaIterator` was changed along with its template parameters to support the new changes of MSSpectrum.
Build errors w.r.t some files are already fixed but still there are some yet to be fixed.

### Why the Project could not be completed?

There were several factors for it. This was my very first time working with advanced C++ for development. So I was a slow learner and had a lot of doubts related to the build errors that I was facing. And hence it took me some time to come to terms with it and understand the codebase from the build perspective. 

 Due to the huge dependency of the MSSpectrum class in other classes, the respective template specializations in other classes had to be adapted as well. There was no way I could find of compiling and building MSSpectrum independently from other classes to compare its performance hence, I had to implement everything along with other classes using the changed MSSpectrum class. So even for small changes after a certain period of time, a lot of build errors started to come. And the build errors are still coming up. This is happening maybe because of the vastness of the OpenMS codebase and even if small changes are introduced in a deeply used class, it can lead to a lot of breaking changes.  Since I was a newbie to the codebase it took me time and a lot of help from the mentors to fix the build errors. At times, maybe I became over reliant on my mentor’s input.  I tried my best to fix the errors but I was not able to do so for all of them in the given timeframe because of the exploratory and experimental nature of the project. 
 
But on the other hand, the foundations for the zero cost abstraction have been laid and this can be built upon and extended. Though I found the going challenging at times, I’ve tried my best every week to learn and grasp the components in the codebase and I’ve tried to build upon my learnings.

### Future Plan

The foundation of the abstraction w.r.t MSSpectrum class has been laid.  There are some changes required in the implementation of functions in MSSpectrum. But before moving onto that we need to fix the build errors that are being thrown right now. After the build errors are being fixed, changes w.r.t MSSpectrum member functions needs to be done. This will mark the successful completion and transformation of MSSpectrum to SoA (Structure of Arrays) data layout. I was not able to get an extension before the submission period. But if possible i would still want to contribute to this as an Open-Source contribution to the OBF and OpenMS community and complete it because this was my first step in Open-Source and it made me learn and gain knowledge about a lot of things.

### Coding Period ends after Week 12

### Week 12 - 29th to 4th September

 - Fixing build errors that are generated because of the new inheritance from `BaseContainer` in MSExperiment, also making the AreaIterator code template deductive for `const` and `non-const` usage.

### Week 11 - 22nd to 28th August

 - Successfully removed and fixed build errors for `EmgGradientDescent.cpp` and started with `swap()` implementation for `BaseContainer` in the abstraction template.
 - Fixing build errors for `LinearResampler.h` file along with the necessary changes in MSSpectrum class.

### Week 10 - 15th to 21st August

 - Working on the new design for AreaIterator.
 - Successfully implemented AreaIterator with the new changes in both the `AreaIterator` template and our abstraction template.

### Week 9 - 8th to 14th August

 - Meeting with the mentors on discussing how to tackle the AreaIterator problem related to the newly introduced abstraction template.
 - Came up with an idea of re-designing the AreaIterator template.
 - Changed the inheritance of MSSpectrum class from `vector<Peak1D>` to `BaseContainer<VectorTemplate, Peak1DT<double,double>>`.

### Week 8 - 1st to 7th August

 - Completed the inbuilt functions of vector in SoA data layout like emplace_back, pop_back, empty, front, back, reserve, insert, erase.
 - Tested these functionalities with the abstraction template.
 - Complications related to AreaIterator arises because of the current abstraction template.
 - Brainstorming related to the problem.

### Week 7 - 24th to 31st July

 - Participating in the mid-term evaluation.
 - After improving the abstraction, tried implementing getBasePeak() using the abstraction in MSSpectrum class.
 - Successfully implemented getBasePeak().
 - Started working on incorporating new functions of vector in SoA data layout like insert(), emplace_back(), pop_back(), erase(), etc.

### Week 6 - 18th to 23rd July

 - Starting with the new abstraction.
 - Working on initial build of Peak1DTuple which is in the new abstraction.
 - Working on introducing Iterators and ConstIterators in the abstraction.

### Week 5 - 10th to 17th July

 - Julianus introduced the abstraction with a little tweak which solves the problem of std::sort() and swap() which was problematic before in case of std::tuple.
 - Studying the abstraction introduced and thinking how we can introduce and integrate this with the codebase after the changes.

### Week 4 - 3rd to 9th July

 - Brainstorming about solutions that can be used for problems arising in using a normal SoA data layout in case of range-based for loops.
 - Thinking of switching back to original crosetto's abstraction.

### Week 3 - 27th June to 2nd July

 - Working on the code breakages because of the getBasePeak() POC.
 - getBasePeak() implemented successfully.

### Week 2 - 21st to 26th June

- Worked on the code breakages due to initial build.
- Brainstorming about the idea of introducing new iterators for the changed data layout.
- Started with a POC for getBasePeak() function and introduced ProxyIterator for the new data layout.

### Week 1 - 13th to 20th June

- Start building the MSSpectrum class with SoA datalayout.
- Will use the current MSSPectrum class as inspiration and just work on changing the internal implementations of it's respective member functions based on the data layout policy for SoA.

### Coding Period Begins

### Schedule for 3rd Week 6th to 12th June

- Figuring out how to implement std::sort() in Crosetto's abstraction.
- Also studying and analysing options regarding the possibility of implementing various STL functions, if we use the abstraction.

### Schedule for 2nd Week 30th May to 5th June

- Play around with Crosetto's abstraction with my own self-defined MSSpectrum class.
- Study the details about abstraction.


Will update more in a short while..

### Schedule for 1st Week 23rd May to 29th May

- Setting up a fresh development environment for the project.
- Along with that I will start revising the Zero Cost Abstraction by crosetto ([here](https://github.com/crosetto/SoAvsAoS)).
- I will also be looking in the MS SPectrum class and it's usage to get a more clear understanding and will be posting doubts on the community platform.

### About the Project ([Link to the Project Idea](https://www.open-bio.org/events/gsoc/gsoc-project-ideas/))
In this project, we need to implement a zero-cost abstraction using Modern C++, which can help us to switch between Structure of Arrays (SoA) and Array of Structures (AoS). This abstraction needs to be introduced at MSSpectrum and MSChromatogram levels. These are the 2 classes used in OpenMS, which currently uses vector<Peak1D> i.e. an Array of Structures.

  
### About Me 
I am a 3rd-year Computer Science Undergraduate student at National Institute of Technology, Karnataka. I am a programming enthusiast with a profound interest in programming, software development, and open source contributions. I am passionate about transforming my ideas into code and building new things. Apart from programming, I like playing tennis.
  

  
  
