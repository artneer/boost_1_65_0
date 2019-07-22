# boost_1_65_0
for dependency of socket.io-client-cpp

## Build.bat   
reference: http://informilabs.com/building-boost-32-bit-and-64-bit-libraries-on-windows/
#### `b2`
- The build tool you just built. Replacement for `bjam`.   
#### `--build-dir=build/(arch)`
- `b2` caches its configuration. When you build the second library with different settings, it looks like it uses the cached settings from the first build. Specify a distinct build directory for each build, or delete `bin.v2` between runs.
#### `address-model=(bits)`
- Build it this wide. If you thought you saw the Boost documentation claiming that it will build 64-bit by default if you're on a 64 bit host running 64-bit windows, you were clearly mistaken like I was. When you start the 64-bit build, you will see both 32-bit: yes and x86: yes. You can optionally worry about whether these instructions are actually going to work at this point, but the Py_ssize_t to unsigned int cast warnings flying by are your guarantee you've entered 64-bit flavour country.
#### `--build-type=complete`
- Build `[debug,release]x[static,shared]`. That is, build all the variants so we don't have to do this again later.
#### `--stagedir=stage/(arch)`
- By default, boost will build to `stage/` both times, wiping out your first build with your second. Don't do the default thing.
#### `--toolset=(toolset)`
- It seemed to pick up MSVC12 on my system by default, but we've been burned before, haven't we? Specify explicitly. If you want to build for multiple toolsets, you can use the same stage dir -- the lib filenames specify the toolset to which they apply, so they won't collide. You'd probably want a different build-dir though.
