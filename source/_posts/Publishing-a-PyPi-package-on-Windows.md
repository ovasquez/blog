---
title: Publishing a PyPi package on Windows
date: 2017-06-09 15:07:43
tags:
- python
- pip
- pypi
- windows
---

I was publishing a Python package to PyPi in my Windows PC and all the information I found worked only on Linux/Mac, almost
nothing about Windows so I decided to post about it for posterity. I was facing two main issues:

1. Couldn't build the distribution packages.
2. Publishing in pypi servers using `setup.py`

Let's see the details:

## 1. Building the dist packages - issues with `.pypirc` file

There was a problem with Python's `setuptools` locating the `.pypirc` file needed with the configuration to register (in
test servers) and upload the package.

The solution was pretty simple, I used the `Git Bash` terminal (any other *NIX terminal should work) and placed the `.pypirc`
file in the home `~` directory. The build was successful from this terminal. 


## 2. Publishing in PyPi
The first result when *Googling* for "pypi publishing" is a very well explained [guide](http://peterdowns.com/posts/first-time-with-pypi.html)
that sums up most what you need to effectively publish a PyPi package.

Unfortunately, the method for publishing to the PyPi Live servers is deprecated, you have to use `twine` instead. The steps
for publishing the PyPi package would be (also from the *NIX terminal):

1. Build the package distribution. In this case I built the source and wheels distribution:
```bash
$ python setup.py sdist bdist_wheel
```

2. Publish using twine
```bash
$ twine upload dist/*
```

That's it. Your python packages should be online already.

## References
- Excellent PyPi publishing guide: http://peterdowns.com/posts/first-time-with-pypi.html
- Uploading distributions: https://packaging.python.org/distributing/#upload-your-distributions