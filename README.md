# Open Plot

Open plot is a open source specification for communicating with pen plotters.

You can view the current specification by looking at [openplot.md](openplot.md).

## Why not GCode?

GCode is the industry standard for CNCs and 3D printers so you may be asking "why not just use GCode?" The reasons are as follows:

- As far as I tell there isn't a dialect of GCode focused on plotters or similar devices, so there's not really a good standard that is well defined.
- Open plot sacrifices some human readability in favor of making it easier to design devices that use it.
- Smaller and more focused instruction set makes it simpler to write code for while sacrificing compatibility and versatility.

## Versions

Open plot follow the `Major.Minor.Patch` versioning convention. For more information about specific versions read [changelog.md](changelog.md).

## Contributing

Feel welcome to contribute by [opening an issue]() that discusses possible improvements. If you make a pull request without discussion it may not be accepted depending on it's contents.

If you like this standard and want to see it used more, then a great way to contribute is by making tools for using it. Plugins to generate open plot files, machines that use open plot, and applications that work with open plot.
