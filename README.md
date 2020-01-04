About
=====

pathlib is a Nim module that provides an interface for working with paths that is as similar as possible to Python's pathlib module.

Examples:

    # Create two paths, check if they are equal, and append another directory to the first path.
    var path1 : NimPath = Path("/home/adam/")
    var path2 : NimPath = Path("/home/user")
    echo(path1 == path2) # false
    path1 = path1 / "nim" / "pathlib"
    echo(path1) # "/home/adam/nim/pathlib"

    # Create a path and output the parent directories of the path.
    var path : NimPath = Path("/home/adam/nim/pathlib/pathlib.nim")
    var parents : seq[string] = path.parents
    for i in parents:
        echo(i)
    # output:
    # "/"
    # "home"
    # "adam"
    # "nim"
    # "pathlib"

    # Create a path, get the name and suffix, and then change both.
    var path : NimPath = Path("code/example.nim")
    echo(path.name) # "example.nim"
    echo(path.suffix) # ".nim"
    path = path.with_name("newfile.nim")
    echo(path) # "code/newfile.nim"
    path = path.with_suffix(".py")
    echo(path) # "code/newfile.py"

    # Create a path, check whether the path exists, and then see whether it is a file, directory, or symlink.
    var path : NimPath = Path("/home/adam")
    echo(path.exists()) # true
    echo(path.is_file()) # false
    echo(path.is_dir()) # true
    echo(path.is_symlink()) # false

    # Create a path, rename the path it represents to something else, and then force another rename.
    var path : NimPath = Path("code/example.nim")
    path.rename("code/newexample.nim")
    # path.rename(Path("code/newexample.nim")) also works
    path.replace("code/testing.nim")
    # if "code/testing.nim" already existed, if would be overritten by the last method.
  
    # Create a path and get its representation as a file URI.
    var path : NimPath = Path("/home/adam/nim/code.nim")
    var fileURI : string = path.as_uri()
    echo(fileURI) # "file:///home/adam/nim/code.nim"

    # Create a path and compute a version of this path relative to another.
    var path : NimPath = Path("/home/adam/nim/code.nim")
    echo(path.relative_to("home")) # "adam/nim/code.nim"
    echo(path.relative_to("nim")) # "code.nim"
    echo(path.relative_to("usr")) # can't do, not on path

License
=======

nim-pathlib is released under the MIT open source license.
