# Valgrind Exercise

## Standard install via command-line
```bash
# Configure the project and generate a native build system:
  # Must re-run this command whenever any CMakeLists.txt file has been changed.
  cmake -S ./ -B build/
# To build with debugging information, do:
  cmake -S ./ -B build/ -D CMAKE_BUILD_TYPE=Debug
# Compile and build the project:
  # rebuild only files that are modified since the last build
  cmake --build build/
  # or rebuild everything from scracth
  cmake --build build/ --clean-first
  # to see verbose output, do:
  cmake --build build/ --verbose
# Run program:
  ./build/app/shell-app
# Clean
  cmake --build build/ --target clean
# Clean and start over:
  rm -rf build/
```

## Commands to run to see valgrind output
```bash
# For Checking valgrind output in terminal
valgrind --leak-check=full ./build/app/shell-app

# For Checking valgrind output in txt file
valgrind --leak-check=full ./build/app/shell-app &> Results/terminal-output-after.txt
```

## Questions

`What happens when the executable is linked statically?  Does Valgrind still detect those same bugs?`

When an executable is linked statically, all the necessary library code is included within the binary itself, making it self-contained. This can simplify deployment and potentially improve startup performance, but it results in a larger binary size.

### Valgrind and Static Linking

Valgrind can still detect memory-related issues in statically linked executables, such as:

- **Memory Leaks**: Identifies allocated memory that is not freed.
- **Invalid Reads/Writes**: Detects attempts to access memory that shouldn't be accessed.
- **Uninitialized Memory**: Reports accesses to uninitialized variables.

`Why Valgrind Works`

Valgrind works with statically linked executables because:

1. **Instrumentation**: It monitors memory usage directly during execution, regardless of linking type.
2. **Direct Calls**: All necessary functions (e.g., `malloc`, `free`) are included in the executable, allowing Valgrind to intercept them.

In summary, Valgrind effectively detects memory issues in both statically and dynamically linked executables due to its instrumentation capabilities.
