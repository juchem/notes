# aptitude
- purge unused packages by default:
```
$ sudo tee /etc/apt/apt.conf.d/99purge-unused <<EOF
Aptitude::Purge-Unused "True";
EOF
```

# debian repositories
- stable:
```
sudo tee /etc/apt/sources.list.d/debian-stable.list <<EOF
deb http://deb.debian.org/debian/ stable main non-free contrib
#deb-src http://deb.debian.org/debian/ stable main non-free contrib

#deb http://deb.debian.org/debian-debug/ stable-debug main non-free contrib
#deb-src http://deb.debian.org/debian-debug/ stable-debug main non-free contrib

deb http://deb.debian.org/debian-security/ stable/updates main non-free contrib
#deb-src http://deb.debian.org/debian-security/ stable/updates main non-free contrib

deb http://deb.debian.org/debian/ stable-updates main non-free contrib
#deb-src http://deb.debian.org/debian/ stable-updates main non-free contrib

deb http://deb.debian.org/debian/ stable-backports main non-free contrib
#deb-src http://deb.debian.org/debian/ stable-backports main non-free contrib
EOF
```
- testing:
```
sudo tee /etc/apt/sources.list.d/debian-testing.list <<EOF
deb http://deb.debian.org/debian/ testing main non-free contrib
#deb-src http://deb.debian.org/debian/ testing main non-free contrib

#deb http://deb.debian.org/debian-debug/ testing-debug main non-free contrib
#deb-src http://deb.debian.org/debian-debug/ testing-debug main non-free contrib

deb http://deb.debian.org/debian-security/ testing-security main non-free contrib
#deb-src http://deb.debian.org/debian-security/ testing-security main non-free contrib

deb http://deb.debian.org/debian/ testing-updates main non-free contrib
#deb-src http://deb.debian.org/debian/ testing-updates main non-free contrib

#deb http://deb.debian.org/debian/ testing-backports main non-free contrib
#deb-src http://deb.debian.org/debian/ testing-backports main non-free contrib
EOF
```
- unstable:
```
sudo tee /etc/apt/sources.list.d/debian-unstable.list <<EOF
deb http://deb.debian.org/debian/ unstable main non-free contrib
#deb-src http://deb.debian.org/debian/ unstable main non-free contrib

#deb http://deb.debian.org/debian-debug/ unstable-debug main non-free contrib
#deb-src http://deb.debian.org/debian-debug/ unstable-debug main non-free contrib

#deb http://deb.debian.org/debian-ports/ unstable main non-free contrib
#deb-src http://deb.debian.org/debian-ports/ unstable main non-free contrib
EOF
```
- experimental:
```
sudo tee /etc/apt/sources.list.d/debian-experimental.list <<EOF
deb http://deb.debian.org/debian/ experimental main non-free contrib
#deb-src http://deb.debian.org/debian/ experimental main non-free contrib

#deb http://deb.debian.org/debian-debug/ experimental-debug main non-free contrib
#deb-src http://deb.debian.org/debian-debug/ experimental-debug main non-free contrib

#deb http://deb.debian.org/debian-ports/ experimental main non-free contrib
#deb-src http://deb.debian.org/debian-ports/ stable main non-free contrib
EOF
```
