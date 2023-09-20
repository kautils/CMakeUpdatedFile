### CMakeUpdatedFile
* get the updated files from the given files.

### note
* READ | WRITE : 
    * READ  :  get the updated files from the given files
    * WRITE :  update caches variables for the given files
* FILES : list variable whichi contains files that you limit. 

### example1
```cmake
set(__files a b c )
CMakeUpdatedFile(READ FILES __files) # only updated files remain in __filse 
CMakeUpdatedFile(WRITE FILES __files) #  update remains
```

### example2 : for compile
```cmake
macro(SomeCompilationProcess __res __srcs)
    set(${__res} TRUE)
endmacro()

set(${m}_partial TRUE)
if(${${m}_partial})
    CMakeUpdatedFile(READ FILES __srcs)
endif()

list(LENGTH __srcs __srcs_len )
if(NOT ${__srcs_len} EQUAL 0)
    
    # assume that __srcs are compiled 
    SomeCompilationProcess(is_success ${__srcs})
    
    # if the result of the compilation is successed update caches
    if(${is_success})
        CMakeUpdatedFile(WRITE FILES __srcs)
    endif()
endif()
```