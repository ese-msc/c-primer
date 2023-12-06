# Combining C and Python

The standard Python interpretter is written in C, and it's possible to write Python modules in C or C++ to improve performance. This not strictly within the scope of the course, but if you're interested, you can find more information in the [Python documentation](https://docs.python.org/3/extending/extending.html).

## A concrete example

As a (relatively) simple example, let's look at a C++ function which takes a list of numbers and returns the sum of the squares of the numbers. We'll then write a wrapper to call this function from Python.

### The C++ code file

#### The core C++ function

Here's a version of simple a C++ function to calculate the sum of the squares of a bunch of numbers.

```c++



// 
// This is written in C style passing in an array and its length.

int sum_of_squares(int* numbers, int length){
    int sum = 0;
    for(int i=0; i<length; i++){
        sum += numbers[i]*numbers[i];
    }
    return sum;
}

```

#### The Python wrapper

The Python wrapper is a little more complicated, but not much. We need to include the Python header file, and then define a function which takes a Python object as an argument, and returns a Python object back to the interpretter. The cored function itself is very simple, it just converts the Python object into a C array, calls the C function, and then converts the result back into a Python object.

```c++
// These two lines are required to use the Python/C API
#define PY_SSIZE_T_CLEAN
#include <Python.h>

// A Python wrapper for the sum_of_squares function

static PyObject *
pysum_of_squares(PyObject *self, PyObject *args)
{
    PyObject *py_list;
    int length
    int sum;

    // Parse the Python input arguments (assumed to be a list of integers)
    if (!PyArg_ParseTuple(args, "O", &py_list))
        return NULL;

    // Get the length of the list and assign memory for the C array.

    length = PyList_Size(py_list);
    int *input = new int[length];


    // Convert the Python list to a C array

    for(int i=0; i<length; i++){
        input[i] = PyLong_AsLong(PyList_GetItem(py_list, i));
    }


    // Call the C function and get the result

    sum = sum_of_squares(input, length);


    // clean up the memory used by the C array
    delete[] input;

    return PyLong_FromLong(sum);
}

```

#### The method table

The next step is to define a method table which tells Python how to call the function. This is a little more complicated than the previous examples, but not much. We need to define a method table which tells Python the name of the function, the C function to call, the type of the arguments, and a docstring to display when the user asks for help.

```c++
static PyMethodDef SquareSumMethods[] = {
    {"sum_of_squares", // Python name
     pysum_of_squares , // C function
     METH_VARARGS, // Argument type (in Python.h)
     "Sum the squares of the values in an iterable."}, // This is the docstring
    {NULL, NULL, 0, NULL}        // Sentinel
};

```

#### The module definition

Finally, we need to define the module itself. This is mostly boilerplate, but we need to tell Python the name of the module, the docstring, and the method table we just defined.

To do this, we define a `struct` with the required information, and then pass it to the `PyModule_Create` function returned from a `PyMODINIT_FUNC` function. These are both defined inside the Python header file.


```c++
static struct PyModuleDef square_sum_module = {
    PyModuleDef_HEAD_INIT, // struct base from Python.h
    "square_sum",   // module name 
    "A module that sums the squares of the values in an iterable.", // docstring
    -1, // size of per-interpreter state of the module, or -1 if the module keeps state in global variables.
    SquareSumMethods // the array of methods created above
};

PyMODINIT_FUNC PyInit_square_sum(void) {
    Py_Initialize();
    return PyModule_Create(&square_sum_module);
}

```

## The Python Setup File

The most convenient way to build the module is to use a Python setup file. This is a Python script which uses the `setuptools` module to build the module. The setup file for this example is shown below.

```python
from setuptools import Extension, setup

setup(
    ext_modules=[
        Extension(
            name="square_sum",  # as it would be imported
                               # may include packages/namespaces separated by `.`
                               # don't need to use the same name as the module

            sources=["sum_of_squares.cpp"], # all sources are compiled into a single binary file
        ),
    ]
)
```

## Building the module

To build the module, we need to run the `setup.py` script. This can be done using the command

```bash
python setup.py build_ext --inplace
```

This will create a file called something like`square_sum.so`,or `square_sum.pyd` on Windows, which can be directly imported into Python (note that most versions actually include more details on the version of Python the import will work with) . The `--inplace` option tells Python to put the file in the current directory, rather than in a subdirectory.

For this to work, you must have the Python development headers installed. On Ubuntu/WSL, this can be done using the command

```bash
sudo apt install python3-dev
```

## Using the module

Once the module is built, it can be imported into Python in the usual way a regular module file would. For example, if the module is called `square_sum`, then we can use it as follows from a Python script/interpreter window.

```python
>>> import square_sum
>>> square_sum.sum_of_squares([1,2,3,4,5])
55
```


