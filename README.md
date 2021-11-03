# Model-based Testing

Designing and writing test cases is usually a manual process. In model-based testing, these steps are automated and test cases can be generated directly from state models. The objective of this exercise is to experiment with model-based testing using the framework _ModelJUnit_.


## Creating RingBufferModel _(3 points)_

Develop a test model named _RingBufferModel_ for the class _RingBuffer_. Use _ModelJUnit_ to generate sequences exploring your model.

### Prerequisites

The repository already contains a model class _RingBufferSimpleModel_ and a test class _RingBufferSimpleModelTest_. The test uses ModelJUnit to generate sequences from the model.

- [x] Run the test (and the model) by `mvn test`                                      
- [x] Read the code of _RingBufferSimpleModel_ and use it as basis for your test model
- [x] Note: The test model class _RingBufferSimpleModel_ contains a main method; you can also run the model in your IDE without the need of a separate test class

### Instructions

In the previous assignment you have drawn a state diagram for the _RingBuffer_. Implement (the revised version of) this state model as executable test model _RingBufferModel_ using the framework ModelJUnit.

- Create a model class _RingBufferModel_ that implements _nz.ac.waikato.modeljunit.FsmModel_
- The model should reflect the states EMPTY, FILLED and FULL of the _RingBuffer_
- Use counter variables to keep track of how many elements have been added to and removed from the buffer and to determine the current state of the buffer in the function _getState()_. Keep in mind that the model is an abstraction, so avoid using another data structure to reimplement the buffer and do not actually store data elements in the model
- The model should provide action methods annotated with _@Action_ for testing _enqueue()_, _dequeue()_, _peek()_, _isEmpty()_ and _size()_  
- Add guard functions to make sure that the actions are only called if the RingBuffer is in a state where these action are valid
- Add additional actions _dequeueFromEmptyBuffer()_ and _enqueueOnFullBuffer_ as well as matching guard functions for the empty/full buffer scenarios in which exceptions are expected

Add the test class _RingBufferModelTest_ and run the model as part of the maven tests


## Achieving model coverage on RingBufferModel _(1 point)_

ModelJUnit provides different metrics about how the model is covered by the generated test sequences. Experiment with different lengths and algorithms in test generation to optimize coverage. Run the test model and measure following coverage metrics (some are already included in _RingBufferSimpleModelTest_):

- _ActionCoverage_
- _StateCoverage_
- _TransitionCoverage_
- _TransitionPairCoverage_

### Instructions

Optimize the parameter `length` in the test method `randomTestWithSimpleModel()` of _RingBufferModelTest_ for full coverage

- Experiment with different _lenght_ parameters in test generation to find out at what length full coverage is achieved
- Set the aprox. minimum length required to achive full coverage for all metrics in the method `randomTestWithSimpleModel()` of _RingBufferModelTest_ 

Furthermore, currently _RandomTester_ is used as algorithm for generating sequences. Change the algorithm to _GreedyTester_. What is the difference between the two algorithms and how does the change affect the required length to achieve full coverage? 

- Add an additional test method `greedyTestWithSimpleModel()` to _RingBufferModelTest_ that uses _GreedyTester_
- Experiment with different _lenght_ parameters in test generation to find out at what length full coverage is achieved
- Set the aprox. minimum length required to achive full coverage for all metrics in the method `greedyTestWithSimpleModel()` 


## Extending the model to RingBufferModelWithAdapter _(3 points)_

Extend your _RingBufferModel_ with calls to the methods of the class _RingBuffer_ in order to have the code of the class under test executed in test generation.

### Prerequisites

Reuse your test model from the previously written class _RingBufferModel_. Name the resulting model _RingBufferModelWithAdapter_. 

### Instructions

The model should extend the existing actions with calls to the corresponding methods of the class _RingBuffer_ and the resulting response (i.e., returned values, thrown exceptions) should be compared to the expected response  

- Add a call to the corresponding method of the class _RingBuffer_ to every action method
- Check the return value of the method call: Make use of the model's state variables (counters) to assert the correct response using JUnit assert methods
- In case of expected exceptions, make sure that (1) exceptions are actually thrown and (2) they are of the correct type and contain the correct message 

Write a unit test _RingBufferModelWithAdapterTest_ to exercise _RingBufferModelWithAdapter_ as part of the maven tests
 

## Measure code coverage on RingBuffer _(1 point)_

The test model _RingBufferModelWithAdapter_ exercises the class _RingBuffer_ when it is executed. Measure and analyze the code coverage achieved by the model-based test.

### Instructions

- Use the _JaCoCo plugin_ in the corresponding section in the _pom.xml_ 
- Run the _RingBufferModelWithAdapter_ to measure the code coverage

Document the code coverage achieved for different levels of model coverage in the following table:

| Full Model Coverage    | Length     | Code Coverage | 
|:---------------------- | ----------:| -------------:|
| ActionCoverage         | TBD        | TBD           |
| StateCoverage          | TBD        | TBD           |
| TransitionCoverage     | TBD        | TBD           |
| TransitionPairCoverage | TBD        | TBD           | 


## Adventures with Monkey Tests _(2 points)_

In the chapter _Adventures with Monkey Tests_, John Fodeh describes an automated random test approach, which is also known as "monkey testing". The approach aims at testing the reliability of embedded and Windows-based medical applications. 

Reference: _John Fodeh: Adventures with Monkey Tests, In: D. Graham and M. Fewster (Eds.) Experiences of Test Automation: Case Studies of Software Test Automation, Pearson Education, 2012
Instructions_ 

Read the book chapter carefully and answer following questions. Document each of your answers in a short paragraph.
 
- How does (dynamic) monkey testing overcome the typical limitations of (static) automated regression testing? Answer this question by briefly addressing each of the limitations listed in the sections 24.2.1 to 24.2.5.

*TBD: Answer here*

- What does the metric mean number of random operations between failures describe and how is this metric interpreted to support test and release decisions? 

*TBD: Answer here*

- What is (from your point of view) the biggest problem when using monkey testing in a real-world project? Explain your answer. 

*TBD: Answer here*


## Submission

When you're done...

- [x] push your changes to your upstream repository on GitHub
- [x] on GitHub, [create a release][GitHub creating releases] shown as new version
- [x] upload the [link to your release][GitHub linking to releases] on the e-learning platform until the specified date and time before the next lecture

[GitHub creating releases]: https://help.github.com/articles/creating-releases/
[GitHub linking to releases]: https://help.github.com/articles/linking-to-releases/
