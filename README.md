# Mixmeister-MMP-Parser-to-Tracklist
Self contained HTML Webapp to parse a Mixmeister .mmp Playlist
This HTML file is a client-side web application for parsing Mixmeister Pro (.mmp) files to extract .mp3 filenames and export them as an .m3u8 playlist file.
Here is a summary of its core functionality and how it works:
Core Functionality
 * File Upload (.mmp): It allows a user to upload a binary Mixmeister Pro project file (.mmp).
 * Regex Parsing (Heuristics): It reads the binary file into an ArrayBuffer and uses two text-decoding heuristics combined with Regular Expressions to find filenames:
   * Heuristic 1: Spaced-ASCII (latin1 decoding): It looks for filenames formatted like "S a x y . m p 3" and "de-mangles" them into standard names like "Saxy.mp3".
   * Heuristic 2: UTF-16LE Decoding: It looks for standard filenames like ".mp3" within the UTF-16LE representation of the file.
 * Result Display: The extracted .mp3 filenames are displayed in a numbered list in the web interface.
 * Export to .m3u8: A button allows the user to export the list of extracted filenames into a standard M3U8 playlist file (starting with #EXTM3U and using the original .mmp filename).
 * Copy Functionality:
   * The extracted names are also placed into a hidden text area, but without the .mp3 extension.
   * A "Copy List" button copies this clean list of names (no extension) to the user's clipboard.
Key Technical Details
 * HTML/CSS: The interface is built using basic HTML and styled with Tailwind CSS.
 * JavaScript (Parsing Logic):
   * readFileAsArrayBuffer is an async function used to load the binary file.
   * demangleSpacedASCII implements the logic to convert the spaced-out text into a normal string (e.g., "A. m p 3" becomes "A.mp3").
   * parseButton's logic handles decoding the buffer with different encodings (latin1 and utf-16le) and applying the regex patterns.
 * M3U8 Generation: The exported .m3u8 file content is simple: it starts with the header #EXTM3U\n followed by the list of extracted filenames, each on a new line.
 * 
