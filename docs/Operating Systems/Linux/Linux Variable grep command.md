
## Apt List --upgradable

```
sudo apt upgrade $(apt list --upgradable | grep upgradable | cut -d '/' -f1 | tr -d ' ')
```

HERE, Description the code :
-   `apt list --upgradable` lists all the packages that have updates available.
-   `grep upgradable` filters the output of the previous command to only show the lines that contain the word "upgradable".
-   `cut -d '/' -f1` extracts the package name from each line by using the forward slash character (`/`) as the ***[ #delimiter ]*** and taking the first field.
-   `tr -d ' '` removes any spaces from the package name.
-   The resulting list of package names is then passed as arguments to `sudo apt upgrade`, which upgrades those packages to their latest versions.

	***[ #delimiter]*** : In computer science and programming, a delimiter is a character or sequence of characters that marks the beginning or end of a unit of data. Delimiters are used to separate or distinguish different parts of a data stream, such as fields in a file or parameters in a command line.
	
	In the context of the `cut` command used in the previous code example, the delimiter is the forward slash character (`/`) which separates the package name and its version number in the output of `apt list --upgradable`. By using the `-d` option with `cut`, we can specify that the forward slash should be used as the delimiter, and then use the `-f` option to specify which field we want to extract (in this case, the first field which contains only the package name).