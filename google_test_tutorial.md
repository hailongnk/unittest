Installation Google Test Guideline
==================================
**IMPORTANT:** This guideline is only tested on Ubuntu 16.04 + Google Test version 1.7.0
- Download Google Test source code 1.7.0 from https://github.com/google/googletest/releases/tag/release-1.7.0

- Decompress, go to source code folder, and compile source by the following commands:
<pre><code>
# Suppose that you downloaded the .zip file
unzip googletest-release-1.7.0.zip
cd googletest-release-1.7.0

# If you don't have cmake, please install it by the command:
# sudo apt-get update
# sudo apt-get install cmake
cmake -DBUILD_SHARED_LIBS=ON .
make
</code></pre>

- After successful compilation, copy headers and libs files (*.so) to system lib and header folders:
<pre><code>
sudo cp -a include/gtest /usr/include
sudo cp -a libgtest_main.so libgtest.so /usr/lib/
</code></pre>

- Finally, reconfigure the library:
<pre><code>
sudo ldconfig -v | grep gtest
</code></pre>

- If the output contains following infomation, then Google Test was installed successfully
<pre><code>
libgtest.so.0 -> libgtest.so.0.0.0
libgtest_main.so.0 -> libgtest_main.so.0.0.0
</code></pre>

Create first Google Test code sample
====================================
Copy following code to a filename **test1.cpp**
<pre><code>
#include "gtest/gtest.h"
TEST(MathTest, TwoPlusTwoEqualsFour) {
    EXPECT_EQ(2 + 2, 4);
    EXPECT_EQ(9, 3*2);
}

int main(int argc, char **argv) {
    ::testing::InitGoogleTest( &argc, argv );
    return RUN_ALL_TESTS();
}
</code></pre>

Open terminal and compile this files
<pre><code>
long@longzone:~/Downloads/sample$ g++ test1.cpp -lgtest -lgtest_main -lpthread
</code></pre>

Execute the binary and see the result:
<pre><code>
long@longzone:~/Downloads/sample$ ./a.out
[==========] Running 1 test from 1 test case.
[----------] Global test environment set-up.
[----------] 1 test from MathTest
[ RUN      ] MathTest.TwoPlusTwoEqualsFour
test1.cpp:4: Failure
Value of: 3*2
  Actual: 6
Expected: 9
[  FAILED  ] MathTest.TwoPlusTwoEqualsFour (0 ms)
[----------] 1 test from MathTest (0 ms total)

[----------] Global test environment tear-down
[==========] 1 test from 1 test case ran. (0 ms total)
[  PASSED  ] 0 tests.
[  FAILED  ] 1 test, listed below:
[  FAILED  ] MathTest.TwoPlusTwoEqualsFour

 1 FAILED TEST
</code></pre>


Reference
=========
- http://stackoverflow.com/questions/26232237/google-testing-missing-dso
- http://stackoverflow.com/questions/27091412/how-to-compile-a-gtest-cpp-file