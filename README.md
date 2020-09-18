# havecmd

A template for my `bash` scripts, to provide a nicer interface to check for the presence of external commands on the users `$PATH`.

This isn't a dependency, because the whole point of this script is to check for dependencies. So, whenever I'm writing a substantial bash script that depends on external commands that may or may not be installed, I copy the `./template` script and start from there.

Easiest way to understand the interface is to read it:

```shell
#!/bin/bash
# Template from https://github.com/seanbreckenridge/havecmd

# get the name of this script
declare script_name
script_name="$(basename "${BASH_SOURCE[0]}")"

havecmd() {
	local BINARY ERRMSG
	# error if first argument isn't provided
	BINARY="${1:?Must provide command to check}"
	# the commend exists, exit with 0 (success!)
	if command -v "$BINARY" >/dev/null 2>&1; then
		return 0
	else
		# construct error message
		ERRMSG="'$script_name' requires '$BINARY', could not find that on your \$PATH"
		if [[ -n "$2" ]]; then
			ERRMSG="$ERRMSG. $2"
		fi
		printf '%s\n' "$ERRMSG" 1>&2
		return 1
	fi
}

# If the first arguments isn't available on the users $PATH
# print an error and the second argument, if given
# set the -e flag; exits if any of the dependencies aren't satisfied
set -e
# Examples
havecmd python
havecmd fd 'See installation instructions at https://github.com/sharkdp/fd'
havecmd wait-for-internet "Install it with 'cargo install --git https://gitlab.com/seanbreckenridge/wait-for-internet'"
havecmd pmark 'Install by running "sh <(curl -sSL http://git.io/sinister) -u https://raw.githubusercontent.com/seanbreckenridge/pmark/master/pmark"'
set +e

# I commonly have scripts that use files relative to the script itself.
# If thats the case, this part of the script handles changing the
# current directory to the same as the scripts'
#
# uncomment this part to 'cd' to the directory that this script is in

# declare this_dir
# this_dir="$(dirname "${BASH_SOURCE[0]}")"
# if havecmd realpath; then
# 	this_dir="$(realpath "$this_dir")"
# fi
# cd "$this_dir" || {
# 	echo "Couldn't 'cd' to '$this_dir'" 1>&2
# 	exit 1
# }

main() {
	echo "ran '$script_name' with arguments '$*'"
	return 0
}

# exit code of the main function is the exit code of the entire script
main "$@" || exit $?
```

