CXX = g++
CXXFLAGS = -lgtest -lgtest_main -lpthread 
INCS = -I./ -I../../src -I/gtest/include
OBJS = ../../src/Addition.o Addition_Test.o ../../src/Multiply.o Multiply_Test.o

testAll: $(OBJS)
	$(CXX)   $(INCS) -o testAll  Main_TestAll.cpp $(OBJS) $(CXXFLAGS)

.cpp.o:
	$(CXX)  -c $< -o $@ $(INCS) $(CXXFLAGS)

clean:
	rm testAll *.o testAll.xml
