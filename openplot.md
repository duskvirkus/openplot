# Open Plot 0.1.0

## Line Format

A line of open plot code consists of 12 bytes. 4 bytes for the command and 8 bytes for data. The line is padded with null bytes where the data is not needed.

## Data Types

Specifies the format for the data types used in open plot.

- `uint16` - An unsigned 16 bit integer.
- `float32` - A IEEE 754 32 bit floating point number.
- `position` - 2 float32, an x position followed by a y position both represented as millimeters.

### Endian-ness

All numbers are expressed in little endian format. This is because that's how numbers are stored on arduino. Meaning you'll need to convert them before sending on most computers.

## Operational Modes

Only one mode is specified currently but this is leaving room for potential updates to the standard.

- 0 - **Standard Mode**

## File Names

Open plot files use the file extension `.oplot`. It is case sensitive, lower case lettering is required. Upper case lettering may result in undefined behavior.

## Commands

### Start - `star`

Start commands open communication with an open plot machine. It is comprised of `star`, the version number in `uint16`s (major minor patch), and 1 `uint16` specifying the operational mode.

*Example:*
```
star00100000
```
Starts machine, specifies version 0.1.0, and mode 0 (standard mode).

### Home - `home`

Will move to home without the pen contacting the drawing surface. The structure consists of `home` followed by padding bytes.

*Example:*
```
home0000000
```

### Move - `move`

Move commands specify moving without the pen contacting the surface. The structure consists of `move` followed by a position.

### Mark - `mark`

Moves to specified position while the pen is contacting the surface. The structure is `mark` followed by a position.

## Replies

Replies consist of 4 bytes with an optional message of any length that follows.

The machine will respond with a `done` reply once it has completed a line. Indicating that the machine is ready for another line.

`eror` replies will be sent when a problem is detected. `eror` messages will contain messages in ASCII text terminated with a `'\0'` (null character).
