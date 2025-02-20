<div align="center">

[![preview](https://github.com/moderngl/moderngl/assets/11232402/b314f7af-0c0a-4b7d-b4f5-857f426454ca)](#readme)

</div>

# ModernGL

[![pypi](https://badge.fury.io/py/moderngl.svg)](https://pypi.python.org/pypi/moderngl) [![anaconda](https://anaconda.org/conda-forge/moderngl/badges/version.svg)](https://anaconda.org/conda-forge/moderngl/) <img src="https://raw.githubusercontent.com/moderngl/moderngl/master/.github/python-versions.svg?sanitize=true"> [![rtd](https://readthedocs.org/projects/moderngl/badge/?version=latest)](https://moderngl.readthedocs.io)

ModernGL is a python wrapper over OpenGL 3.3+ core that simplifies the creation of simple graphics applications like scientific simulations, games or user interfaces. Usually, acquiring in-depth knowledge of OpenGL requires a steep learning curve. In contrast, ModernGL is easy to learn and use, moreover it is capable of rendering with high performance and quality, with less code written. The majority of the moderngl
code base is also written in C++ for high performance.

```sh
pip install moderngl
```

- [Documentation](https://moderngl.readthedocs.io/)
- [Examples](https://github.com/moderngl/moderngl/tree/master/examples/#readme)
- [ModernGL on Github](https://github.com/moderngl/moderngl/)
- [ModernGL on PyPI](https://pypi.org/project/ModernGL/)
- [ModernGL Discord Server](https://discord.gg/UEMtW8D)
- [glcontext](https://github.com/moderngl/glcontext)
- [moderngl-window](https://github.com/moderngl/moderngl-window) (Window creation, resource loading, ...)

## Features

- GPU accelerated high quality graphics
- Rendering modern OpenGL scenes with less headache
- Simpler and faster than PyOpenGL
- Can render without a window
- 100% Pythonic

## Sample usage

```py
>>> import moderngl
>>> ctx = moderngl.create_standalone_context()
>>> buf = ctx.buffer(b'Hello World!')  # allocated on the GPU
>>> buf.read()
b'Hello World!'
```

For complete examples please visit the [Examples](https://github.com/moderngl/moderngl/tree/master/examples/#readme).

## Easy to use with Pillow and Numpy

```py
>>> img = Image.open('texture.jpg')
>>> ctx.texture(img.size, 3, img.tobytes())
<Texture: 1>
```

```py
>>> ctx.buffer(np.array([0.0, 0.0, 1.0, 1.0], dtype='f4'))
<Buffer: 1>
```

## Compared to PyOpenGL

With PyOpenGL, using the original OpenGL API, you have to write three lines to
achieve a simple task like binding a VBO:

```py
vbo1 = GL.glGenBuffers(1)
GL.glBindBuffer(GL.GL_ARRAY_BUFFER, vbo1)
GL.glBufferData(GL.GL_ARRAY_BUFFER, b'Hello World!', GL.GL_STATIC_DRAW)

vbo2 = GL.glGenBuffers(1)
GL.glBindBuffer(GL.GL_ARRAY_BUFFER, vbo2)
GL.glBufferData(GL.GL_ARRAY_BUFFER, None, GL.GL_DYNAMIC_DRAW)
```

With ModernGL you need just one simple line per VBO to achieve the same results:

```py
vbo1 = ctx.buffer(b'Hello World!')
vbo2 = ctx.buffer(reserve=1024, dynamic=True)
```

## Build

[![build](https://github.com/moderngl/moderngl/actions/workflows/build.yml/badge.svg)](https://github.com/moderngl/moderngl/actions/workflows/build.yml) [![test](https://github.com/moderngl/moderngl/actions/workflows/test.yml/badge.svg)](https://github.com/moderngl/moderngl/actions/workflows/test.yml)

```sh
python -m build .
```

## FAQ

### Is ModernGL faster than PyOpenGL?

In many cases **yes**, the core functions of ModernGL are written in C++.
We do not call every OpenGL function from Python, we batch them in a single C++ function instead.

### What version of OpenGL is used?

Most of the calls only require **OpenGL 3.3**.
Compute Shaders require **OpenGL 4.3**.
Some functionality relies on their specific extension.

### Is my old PC supported?

OpenGL 3.3 came out in February 2010. With **up to date drivers** you will
be able to use the most of the ModernGL functions, even on integrated
graphics cards.

### Where can I use ModernGL?

**Anywhere where OpenGL is supported.** ModernGL is capable of rendering
using a [standalone_context] as well. Rendering to a window only requires
a valid OpenGL context.

[standalone_context]: https://github.com/moderngl/moderngl/tree/master/examples/old-examples/standalone

### Can ModernGL create a Window?

**NO**, ModernGL is responsible for calling the OpenGL API and providing a Pythonic user-friendly API instead.
We also provide a utility library [moderngl-window](https://github.com/moderngl/moderngl-window)
making window creation and resource loading very simple.

### Limitations using ModernGL over PyOpenGL?

All the necessary calls are (or can be) implemented in ModernGL. However you can interact with the ModernGL objects from PyOpenGL.
If something is missing write an [issue](https://github.com/moderngl/moderngl/issues) or raise a [PR](https://github.com/moderngl/moderngl/pulls).

## Supported platforms

- [x] Windows
- [x] Linux
- [x] Mac

## Installing from source

### Installing on Ubuntu from source

```sh
apt-get install python3-dev libgl1-mesa-dev libx11-dev
python3 -m pip install -e .
```

### Building the sphinx documentation

```sh
pip install -r docs/requirements.txt
python -m sphinx docs build/sphinx
```

### Running tests

```sh
export LIBGL_ALWAYS_SOFTWARE=true
python3 -m pip install glcontext pytest numpy scipy
python3 -X dev -m pytest -s -vvv tests
```

### Headless rendering

```sh
apt-get install xvfb
alias xpy='xvfb-run -s "-screen 0 1x1x24" python3'
xpy -m moderngl
```

## Citation

If you need to cite this repository in academic research:

```txt
@Online{Dombi2020,
  author = {Szabolcs Dombi},
  title = {ModernGL, high performance python bindings for OpenGL 3.3+},
  date = {2020-05-01},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/moderngl/moderngl}},
  commit = {<insert hash if needed>}
}
```

If commit hash is required this can be found per release here:
https://github.com/moderngl/moderngl/releases

## Community

- [Contributors](https://github.com/moderngl/moderngl/graphs/contributors)
- [ModernGL Discord Server](https://discord.gg/UEMtW8D)
- [Code of conduct](https://github.com/moderngl/moderngl/blob/master/.github/CODE_OF_CONDUCT.md)
