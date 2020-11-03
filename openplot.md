# Open Plot 0.0.0

## Data Types

Specifies the format for the data types used in open plot.

- `uint16` - An unsigned 16 bit integer.
- `float32` - A IEEE 754 32 bit floating point number.
- `position` - 2 float32, an x position followed by a y position both represented as millimeters.
- `info code` - uint16

## Operational Modes

- 0 - **Streaming Mode** - The machine is expecting streaming open plot code.
- 1 - **Debug Mode** - The machine is expecting any commands for debugging or setup purposes.

## Info Codes

- 0 - **General** - ASCII text ending in `\0` (a null character).
- 1 - **Mode** - `uint16` specifying an operational mode.
- 2 - **Position** - `position` specifying the current position of the pen.

## File Names

Open plot files use the file extension `.oplot`. It is case sensitive, lower case lettering is required. Upper case lettering may result in undefined behavior.

## Commands

### Start - `sta`

Start commands open communication with an open plot machine. It is comprised of `sta`, the version number in `uint16`s (major minor patch), and 1 uint16 specifying the operational mode.

*Example:*
```
str00000001
```
Starts machine, specifies version 0.0.0, and mode 1 (debug mode).

### Home - `hom`

Will move to home without the pen contacting the surface. Primarily for use in machines with limit switches. The structure consists of `hom`.

### Change Mode - `cmo`

Will change the machine's mode. Structure is `cmo` followed by uint16 that specifies the mode to change to.

### Move - `mov`

Move commands specify moving without the pen contacting the surface. The structure consists of `mov` followed by a position.

### Mark - `mar`

Moves to specified position while the pen is contacting the surface. The structure is `mar` followed by a position.

### Information - `inf`

Get information about the machine. Structure is `inf` followed by a non-zero info code (see above).

**Important** When in streaming mode reply will only be `rec` and not include any information.

## Replies

In streaming mode the machine will reply with a `rec` or `rer` message. In debug mode the machine will reply with an `rin` or `rer` message.

### Received - `rec`

Acknowledgement that command was received and executed. The machine is ready for the next command. Format is simply `rec`.

### Reply Error - `rer`

Reply indicating something went wrong. `sta` command is required to restart the machine after an error occurred. Format is `rer` followed by optionally any number of ASCII characters that end in a `\0` (a null character).

### Reply Information - `rin`

The same as `rec` just with an optional information message. Format is `rin` followed by an info code and the format specified by that info code (see above).
