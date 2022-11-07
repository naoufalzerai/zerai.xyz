+++
title = "Go Dart Plugin"
date = 2022-11-06T18:35:52-05:00
lastmod = 2022-11-06T18:35:52-05:00
tags = ["Dart","golang"]
categories = ["Coding","Dart"]
imgs = []
cover = ""  # image show on top
readingTime = true  # show reading time after article date
toc = true
comments = false
justify = false  # text-align: justify;
single = false  # display as a single page, hide navigation on bottom, like as about page.
license = ""  # CC License
draft = false
+++


**Part One** the GO side:
1. We need to make the function exportable, so the name should be capitalized and become `GetKey()` 
2. We need to use `cgo` so that we can create shared library, `cgo` means we need to:
<!--more-->
2.1. Use `import "C"`

2.2. Use comment with the function as `//export GetKey`

2.3. Use `C.type` interface, in this example to instead of `string` use `C.char` and `C.CString` and as working with pointer is the preferable way, use `*C.char`

So, the `Go` function in the question, should be re-written as:
```go
// filename: lib.go
package main

import "C"

//export GetKey
func GetKey() *C.char {
	theKey := "123-456-789"
	return C.CString(theKey)
}

func main() {}  
``` 

3. Compile the above and create the shared library as:
```bash
go build -buildmode=c-shared -o lib.a lib.go
```

**Part Two** the Dart side:

1. Create the `pubspec.yaml` and add to its dependencies the `ffi: ^0.1.3`, so it be as:
```yaml
name: dart_app
description: A new Dart application.

# The following line prevents the package from being accidentally published to
# pub.dev using `pub publish`. This is preferred for private packages.
publish_to: 'none' # Remove this line if you wish to publish to pub.dev
version: 1.0.0+1

environment:
  sdk: ">=2.7.0 <3.0.0"

dependencies:
  ffi: ^0.1.3
```
2. Copy the generated files from GO which are `lib.a` and `lib.h` to the dart projetc folder
3. Create dart file to handle the FFI, where you need to:
3.1. Import the `ffi` and the `utf8`

3.2. Define the FFI funtion signature as `typedef get_key_func = ffi.Pointer<Utf8> Function();`

3.3. Define the Dart funtion signature as `typedef GetKey = ffi.Pointer<Utf8> Function();`

3.4. Load the shared library as `final dylib = ffi.DynamicLibrary.open('lib.a');`

3.5. Map FFI and Dart function signatures as `final GetKey getKey dylib.lookup<ffi.NativeFunction<get_key_func>>('GetKey').asFunction();`

3.6. Define a function todo the execution, and inside this function do the following:

3.6.1. Invoke the Dart function and assign the output to a variabe as `var addressOf = getKey();`

3.6.2. Decode the result, which is the address of the pointer, and get the string from it, as: `print(addressOf.ref.toString());`

So, the Dart code will become:
```dart
//file name fficheck.dart
import 'dart:ffi' as ffi; // For FFI
import 'package:ffi/ffi.dart';
import 'package:ffi/src/utf8.dart';

typedef get_key_func = ffi.Pointer<Utf8> Function(); // FFI fn signature
typedef GetKey = ffi.Pointer<Utf8> Function(); // Dart fn signature
final dylib = ffi.DynamicLibrary.open('lib.a');

final GetKey getKey =
    dylib.lookup<ffi.NativeFunction<get_key_func>>('GetKey').asFunction();

void testffi() {
  print("Hi from dart");
  var addressOf = getKey();
  print(addressOf.ref.toString());
}
```

4. Create the main Dart file, and import the file that is handling the FFI, and call the required function, as:
```dart
// file name lib.dart
import 'fficheck.dart';

main() {
  print("Hello, World!");
  testffi();
}
```

5. Execute the dart file as `dart main.dart`

[![enter image description here][1]][1]  


  [1]: https://i.stack.imgur.com/5UfS2.png

Source : https://stackoverflow.com/questions/63747683/how-to-call-go-lib-from-dart-using-ffi/63747684#63747684 