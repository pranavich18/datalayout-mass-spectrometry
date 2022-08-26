## Space- and time-efficient data format for mass spectrometry data (OpenMS) GSOC'22

### Week 11 - 22nd to 28th August

 - Successfully removed and fixed build errors for `EmgGradientDescent.cpp` and started with `swap()` implementation for `BaseContainer` in the abstraction template.
 - Fixing build errors for `LinearResampler` file along with the necessary changes in MSSpectrum class.

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
  

  
  
