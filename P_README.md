# havecmd

A template for `bash` scripts, to provide a nicer interface to check for the presence of external commands on the users `$PATH`.

This isn't a dependency, because the whole point of this script is to check for dependencies. So, this is vendorized; whenever I'm writing a substantial bash script that depends on external commands that may or may not be installed, I copy the `./template` script and start from there.

Easiest way to understand the interface is to read it:

```
>>>PMARK
perl -E 'print "`"x3, "shell", "\n"'
cat ./template
perl -E 'print "`"x3, "\n"'
```

