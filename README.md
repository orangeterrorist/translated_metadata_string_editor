# Partial string modification tool for global-metadata.dat
Not translated by me.

For Android games exported by the Unity-il2cpp script backend, the strings appearing in the code will be compiled into the assets\bin\Data\Managed\Metadata\global-metadata.dat file, as part of the localization work, simple I picked up a tool to modify the strings in it.

## References
- [il2cppdumper](https://github.com/Perfare/Il2CppDumper)<br>
The understanding of the content of the file is learned from the source code of this tool. The tool itself is used to export class definitions from the compiled libil2cpp.so file and global-metadata.dat file. The export form includes IDA available. It is a useful tool for renaming scripts, DLLs available for UABE and AssetStudio, etc.
## Modify the content
&emsp;&emsp;In global-metadata.dat, the way to save the strings in the code is that there is a list in the header to put the offset, length and other information of each string, and then there is an area in the data area that directly Compact all strings, with a list of headers, so no \0 termination is required. <br>
&emsp;&emsp;Because the number of strings does not change before and after the modification, the modification to the list is directly overwritten on the original area. The length of the data area may change. If the length of the data area is less than or equal to the original length after modification, it will be overwritten and written directly. If it is too long, it will be written to the end of the file.