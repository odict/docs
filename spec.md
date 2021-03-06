# File Specification

Compiled odict files are relatively straightforward, as they utilize the [ODict FlatBuffer schema](https://github.com/Nickersoft/odict/blob/master/src/schema.fbs). The buffer generated by this schema take up over 90% of the compiled file, however, addition header information still exists. The table below illustrates the full breakdown of a compiled `.odict` file, in the order in which the values are written to the file. All values written in Little Endian byte order.

| Name | Type | Size | Description |
| :--- | :--- | :--- | :--- |
| Signature | `CHAR[6]` | 6 | Signature for the ODict format. Assertions fail if this signature is missing. Should always be `ODICT`. |
| Version | `USHORT` | 2 | Represents the major version of ODict with which the file was created. |
| Content-Size | `ULONG` | 4 or 8 | Size \(in bytes\) of the compressed content to read. Used in assertions to validate file length. |
| Content | `CONST CHAR*` | Variable | Snappy-compressed FlatBuffer object. Must be decompressed by Snappy and converted to `uint8_t` before it can be used. |

