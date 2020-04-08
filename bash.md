# variables
- detele a variable: `unset foo`
- default value when null: `${foo-value}`, `${foo-${bar}}`, `${foo-$(some command)}`
- default value when null or empty: `${foo:-value}`, `${foo:-${bar}}`, `${foo:-$(some command)}`

# arrays
- declare hash table: `declare -a foo`
- inline init array: `foo=(value1 value2 "value 3")
- multi-line init array: ```
foo=( \
  value1
  value2
  "value 3"
)
```

# hash tables
- declare hash table: `declare -A foo`
- inline init hash table: `foo=([key1]=value1 [key2]="value 2" ["key 3"]=value3)
- hash table keys as array: `${!foo[@]}`
- iterate over hash table entries: ```
for key in "${!foo[@]}"; do
  echo "value: ${foo[${key}}}"
done
```

# debugging
- enable print commands as they're executed: `set -x`
- disable print commands as they're executed: `set +x`
- print commands as they're executed (she-bang): `#!/bin/bash -x`
- enable print commands as they're executed for single statement: `(set -x; command goes here)`

# error handling
- enable exit on error: `set -e`
- disable exit on error: `set +e`
- exit on error (she-bang): `#!/bin/bash -e`
- enable exit on error for single statement: `(set -e; command goes here)`

# she-bang and options
- with current env (`-S` to `env` means the command has multiple tokens): `#!/usr/bin/env -S bash -xe`

# see also
- manual:
  - variable expansion: https://www.gnu.org/software/bash/manual/bash.html#Shell-Parameter-Expansion
  - features: https://www.gnu.org/software/bash/manual/bash.html#Bash-Features
- advanced bash scripting: http://tldp.org/LDP/abs/html/abs-guide.html
- misc:
  - case conversion: https://stackoverflow.com/a/2264537/1284956
