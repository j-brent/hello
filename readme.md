# Conan scm bug

This is a fork of the [conan-io/hello](https://github.com/conan-io/hello) repository, modified to reproduce a [bug](https://github.com/conan-io/conan/issues/10551) I experienced using the [scm attribute](https://docs.conan.io/en/1.19/reference/conanfile/attributes.html#scm-attribute) in my conan recipe.

## Windows Command Shell
When I execute the `conan export` command from a Windows console, the source files are not copied to the `scm_source` directory in my local conan cache.
```console
C:\dev\otro\hello>conan remove -f hello

C:\dev\otro\hello>conan export . issue/10551 --ignore-dirty
Exporting package recipe
Hello/0.1@issue/10551: Repo origin deduced by 'auto': https://github.com/j-brent/hello.git
Hello/0.1@issue/10551: SCM: Getting sources from folder: /c/dev/otro/hello
Hello/0.1@issue/10551: A new conanfile.py version was exported
Hello/0.1@issue/10551: Folder: C:\Users\j-brent\.conan\data\Hello\0.1\issue\10551\export
Hello/0.1@issue/10551: Exported revision: b4348438832c8121e0aeb69e0191c45c0c7d939b

C:\dev\otro\hello>ls .
conanfile.py  LICENSE  readme.md  src

C:\dev\otro\hello>ls C:\Users\j-brent\.conan\data\Hello\0.1\issue\10551\scm_source

C:\dev\otro\hello>
```

## Windows Subsystem for Linux
When I execute the same command on the same files at the same location from the WSL terminal, the source files are copied to the `scm_source` directory in the local conan cache as expected.
```console
j-brent@UTM:/mnt/c/dev/otro/hello$ conan remove -f hello
j-brent@UTM:/mnt/c/dev/otro/hello$ conan export . --ignore-dirty
Exporting package recipe
Hello/0.1: Repo origin deduced by 'auto': https://github.com/j-brent/hello.git
Hello/0.1: SCM: Getting sources from folder: /mnt/c/dev/otro/hello
Hello/0.1: A new conanfile.py version was exported
Hello/0.1: Folder: /home/j-brent/.conan/data/Hello/0.1/_/_/export
Hello/0.1: Exported revision: b4348438832c8121e0aeb69e0191c45c0c7d939b
j-brent@UTM:/mnt/c/dev/otro/hello$ ls .
LICENSE  conanfile.py  readme.md  src
j-brent@UTM:/mnt/c/dev/otro/hello$ ls /home/j-brent/.conan/data/Hello/0.1/_/_/scm_source/
LICENSE  readme.md  src
j-brent@UTM:/mnt/c/dev/otro/hello$ 
```


## License

[MIT](LICENSE)
