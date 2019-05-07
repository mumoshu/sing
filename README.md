# Single-binary package manager

## Usage

Initializing:

```
eval "$(sing init -)"
```

```
export PATH="$(pwd)/.sing/shims:/Users/mumoshu/.sing/shims:${PATH}"
export SING_SHELL=bash
sing rehash 2>/dev/null
sing() {
 local command
 command="$1"
  if [ "$#" -gt 0 ]; then
    shift
  fi

  case "$command" in
  rehash|shell)
    eval "`sing "sh-$command" "$@"`";;
  *)
    command sing "$command" "$@";;
  esac
}
```

Listing available packages:

```
sing install github.com/rogpeppe/gohack --list
```

Installing specific version of a package:

```
# gobin installs the binary and updates ~/.sing/shims/
sing install github.com/rogpeppe/gohack v1.0.0
```

Switching the version of the binary:

```
sing switch gohack v1.0.0
```

Uninstall a specific version/binary:

```
sing uninstall gohack v1.0.0
```

Installing and immediately running an executable command:

```
# Intalls and runs it
sing run github.com/rogpeppe/gohack v1.0.0 -- --help
```

```
cat <<EOF >Singfile
dependencies:
- name: github.com/rogpeppe/gohack
  version: v1.0.0
EOF

# installs all the dependencies locally under .sing/versions/v1.0.0/bin/gohack and rehash shims at .sing/shims/gohack
sing run install

# reads the Singfile to runs the gohack v1.0.0 installed locally
sing run -- gohack --help
```

# Acknowledgements

This project has been hugely inspired by the following awesome projects.

Thanks a lot for authors!

- https://github.com/myitcv/gobin
- https://github.com/mislav/anyenv
